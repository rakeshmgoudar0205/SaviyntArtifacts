# Saviynt Performance Analytics

This document outlines a set of performance-focused analytics designed to monitor and evaluate key operational components within the Saviynt platform. Each entry includes a unique analytic name, category, and the corresponding SQL query used to extract insights from the platform’s database.
---

## 1. **User Import Success Rate**

**Category:** Admin
**Description:** Tracks the success or failure of user import jobs over the past 30 days.

```sql
SELECT DISTINCT
  JOBNAME AS JOB_NAME,
  IFNULL(TRIGGERNAME, 'User Upload From UI') AS TRIGGER_NAME,
  IFNULL(EXTERNALCONNECTION, '') AS JOB_TRIGGER,
  CASE SAVRESPONSE WHEN 'Success' THEN 'Success' ELSE 'Failed' END AS STATUS_OF_JOB,
  JOBSTARTDATE AS STARTDATE_OF_JOB,
  JOBENDDATE AS ENDDATE_OF_JOB
FROM ecmimportjob
WHERE JOBNAME IN ('UserImportJob', 'UserImportFullJob', 'SchemaUserJob')
  AND JOBSTARTDATE >= (UTC_DATE() - INTERVAL 30 DAY)
```

---

## 2. **Rule Run Evaluation Success Rate**

**Category:** Admin
**Description:** Displays the execution status of rule evaluation jobs run within the last 30 days.

```sql
SELECT DISTINCT
  JOBNAME AS JOB_NAME,
  SAVRESPONSE AS STATUS_OF_JOB,
  JOBSTARTDATE AS STARTDATE_OF_JOB,
  JOBENDDATE AS ENDDATE_OF_JOB
FROM ecmimportjob
WHERE JOBNAME LIKE 'RuleRunJob'
  AND JOBSTARTDATE >= (UTC_DATE() - INTERVAL 30 DAY)
```

---

## 3. **SOD Evaluation Job Success Rate**

**Category:** SOD
**Description:** Evaluates the success rate of SOD (Segregation of Duties) risk evaluation jobs over the past month.

```sql
SELECT DISTINCT
  JOBNAME AS JOB_NAME,
  TRIGGERNAME AS TRIGGER_NAME,
  EXTERNALCONNECTION AS CONNECTION_NAME,
  SAVRESPONSE AS STATUS_OF_JOB,
  JOBSTARTDATE AS STARTDATE_OF_JOB,
  JOBENDDATE AS ENDDATE_OF_JOB
FROM ecmimportjob
WHERE JOBNAME LIKE 'RiskSODEvaluationJob'
  AND JOBSTARTDATE >= (UTC_DATE() - INTERVAL 30 DAY)
```

---

## 4. **Top 5 Applications by Provisioning Tasks**

**Category:** Admin
**Description:** Identifies the five applications with the highest number of provisioning tasks.

```sql
SELECT a.TASKKEY, a.TASKTYPE, e.endpointname AS APPLICATION
FROM arstasks a
JOIN endpoints e ON a.endpoint = e.endpointkey AND e.displayname IS NOT NULL
JOIN (
  SELECT COUNT(*) AS totalCount, a.endpoint AS EP
  FROM arstasks a
  GROUP BY a.endpoint
  ORDER BY totalCount DESC
  LIMIT 5
) AS TEMP ON TEMP.EP = a.endpoint
```

---

## 5. **Pending Provisioning Tasks**

**Category:** Admin
**Description:** Reports pending tasks and categorizes them based on how long they’ve been in queue.

```sql
SELECT 'Pending' AS STATUS_OF_TASK,
  CASE
    WHEN (UTC_TIMESTAMP() - INTERVAL 12 HOUR) >= TASKDATE THEN 'More than 12 Hours'
    WHEN (UTC_TIMESTAMP() - INTERVAL 8 HOUR) >= TASKDATE THEN 'More than 8 Hours'
    WHEN (UTC_TIMESTAMP() - INTERVAL 4 HOUR) >= TASKDATE THEN 'More than 4 Hours'
    ELSE 'Less than 4 hours'
  END AS TASK_PENDING_FOR,
  endpoints.DISPLAYNAME AS APPLICATION
FROM arstasks
JOIN endpoints ON arstasks.endpoint = endpoints.endpointkey
WHERE arstasks.STATUS = 1
  AND arstasks.TASKTYPE IN (1, 2, 3, 4, 6, 8, 12, 14, 31)
```

---

**Note:** Additional analytics are available in the source repository. Let me know if you'd like them formatted in a similar structure or presented in a table-based layout for easier comparison. ✅

---