# Entra Domain Services

### Microsoft Entra Domain Services provides managed domain services in the cloud, such as:
- Domain join
- Group Policy
- LDAP
- Kerberos/NTLM authentication
- These services are fully compatible with traditional Active Directory, but without the need to deploy, manage, or patch domain controllers.

| **Feature**              | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| **Managed Domain**       | Provides a domain controller–like environment, managed by Microsoft.           |
| **Domain Join**          | Azure VMs and supported services can be domain-joined without deploying on-prem DCs. |
| **LDAP/Kerberos Support**| Enables legacy apps that require LDAP or Kerberos authentication.              |
| **Group Policy**         | Built-in GPO support allows applying policies to domain-joined machines.       |
| **NTLM Authentication**  | Supports traditional AD-based apps using NTLM.                                 |
| **User Sync**            | Syncs users, groups, and credentials from Entra ID.                            |
| **Secure & Highly Available** | Microsoft handles replication, patching, and availability of the domain controllers. |


