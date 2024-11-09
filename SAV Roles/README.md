# Saviynt SAV Roles Overview

In Saviynt, **SAV roles** (Saviynt Access Viewer roles) are predefined access roles that determine the permissions and capabilities of users within the Saviynt platform. These roles govern what users can view, edit, or administer within the system, allowing organizations to implement precise access controls over identity and access management (IAM) tasks. SAV roles are essential for securing sensitive information, delegating administrative tasks, and ensuring that users have only the permissions necessary for their roles. Saviynt provides default SAV roles to cover a broad range of user personas, but organizations often require custom roles to address specific needs. This document provides an overview of how SAV roles work and examples of custom roles for common IT functions.

## How SAV Roles Work

### Role Definitions
SAV roles are preconfigured with specific permissions to support various functions within the Saviynt ecosystem, such as managing users, applications, policies, and reports. Each role has a set of permissions that define what users can see (view permissions) and do (action permissions) within Saviynt, including creating, modifying, or viewing reports, access requests, and user attributes. Roles are assigned based on organizational needs, allowing certain users to perform administrative functions while limiting access for others.

### Types of SAV Roles
Saviynt provides various SAV roles for identity and access management functions. Common SAV roles include:
- **Admin Roles**: Full administrative access to Saviynt modules, including user management, system configurations, and access policies.
- **Access Approver**: Permissions to review and approve access requests within a defined scope.
- **Audit Viewer**: Read-only access to audit logs and reports, typically for compliance personnel.
- **Identity Manager**: Permissions to manage user identities, including creating, updating, and de-provisioning users.
- **Report Viewer**: Access to view, generate, and export reports without modification permissions.
- **Requestor Role**: Basic permissions to submit and view access requests, for users needing resource access.

### Role Assignment
Roles are assigned based on the **principle of least privilege**, ensuring users receive only the access they need to perform their tasks. Users can be assigned one or multiple roles, combining permissions as needed. Assignments can be manual, automated, or rule-based, depending on an organization’s IAM strategy.

### Segregation of Duties (SoD)
Saviynt incorporates **SoD controls** to prevent conflicts of interest, particularly in sensitive functions. SoD policies prevent users with conflicting roles (e.g., access requestor and approver) from having both roles simultaneously, reducing fraud risk and ensuring regulatory compliance.

### Access and Permissions Management
SAV roles include granular permissions for module, data, and action levels, enabling fine-tuned control so users perform only permitted actions (e.g., read-only access). Permissions are reviewed and updated as roles evolve, aligning with new modules or features.

### Audit and Reporting
All changes related to SAV roles (e.g., assignments, permission changes) are logged in Saviynt’s audit trail, supporting compliance and traceability. Reports on role assignments, usage statistics, and SoD conflicts aid in audit and compliance functions.

## Benefits of Using SAV Roles
- **Enhanced Security**: Precise access control ensures users have only the permissions they need.
- **Compliance Support**: SoD and audit trails support regulatory compliance.
- **Efficiency**: Predefined roles streamline provisioning, role assignments, and access requests.
- **Scalability**: SAV roles provide scalable access control as organizations grow.

## Example SAV Roles

### 1. IT Administrator Role
- **Purpose**: Fo
