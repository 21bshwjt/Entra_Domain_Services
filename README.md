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


###	Complete Steps to Set Up Entra ID Domain Services (AADDS) 
Configuration has been completed with the Entra ID Free license

###	Create a Virtual Network (VNet)
- Ensure its regional and not peered with existing VNets where DNS conflicts might occur.
  
###	Deploy Entra ID Domain Services
- From Entra Portal → Search "Azure AD Domain Services" → Create
- Select the correct VNet and subnet.
- Provide a domain name (e.g., corp.contoso.com).
- Wait until provisioning completes (takes ~30–45 mins).
  
###	Update VNet DNS Settings
- After AADDS deployment, copy the IP addresses of the domain controllers shown in the AADDS overview.
- Go to your VNet > DNS settings and replace "Default" with those two IPs.
- Save and wait a few minutes.
  
### Create a Windows VM (Management Server)
- Place it in the same subnet/VNet as AADDS.
- Make sure NSG/firewall rules allow RDP and domain join traffic.
  
###	Reboot the VM
- Required so that it picks up the updated DNS settings from the VNet.
  
### Enable Password Hash Sync (if not already enabled)
Need to validate (During testing that has been automatically done)
- In Entra ID > Azure AD Connect, ensure password hash sync is enabled.
- This is required for users to log in to AADDS.
  
### Reset Password for Admin Users (Important)
- Even if password hash sync is on, users must reset their password after AADDS is enabled for the hashes to sync into AADDS.
- Do this for the account you plan to use to join the domain.

### Join the VM to the AADDS domain
- Use: corp.contoso.com
- Credentials: username@yourtenant.onmicrosoft.com (or a synced UPN)
- Should be a member of the AAD DC Administrators group for management tasks.
 
### Optional but Recommended:
- Create an OU and Group Policy if needed in the domain using RSAT tools.
- Install DNS and AD tools on your management server if you need them.
- Check Time Sync (VM must sync with the domain’s time to avoid auth issues).
 
### Common Mistakes to Avoid:
- Forgetting to set custom DNS on the VNet.
- Not resetting the user password after enabling AADDS.
- Trying to join with an account not in the AADDC domain or not synced.
- Trying to use regular Entra ID — remember, AADDS is not full Active Directory, it's a managed replica.

### Screenshots from Management Server (Default Settings of Entra DS)

#### Active Directory Users & Computers
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/f48f2ea2d1fbfced8e5fb0a862a5e9e057d774a7/screenshots/dsa.png?raw=true" width="800" height="400">

#### DNS Console
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/8c1ec91e730d1238f7f763c21221bd86eebc6a67/screenshots/dns.png?raw=true" width="800" height="400">

#### Default GPOs
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/54b57cdd8047414f325f77d38df96a19de4f40ec/screenshots/gpmc.png?raw=true" width="800" height="400">

#### Domain & Functional Lebel
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/54b57cdd8047414f325f77d38df96a19de4f40ec/screenshots/fl.png?raw=true" width="800" height="400">

#### Active Directory Administrative Center
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/cd3e37d06abeefeeb2758c7bbce34b00050d0049/screenshots/adac.png?raw=true" width="800" height="400">

#### Repadmin 
<img src="https://github.com/21bshwjt/Entra_Domain_Services/blob/e055eeb0e4c4b1473593da0edeb4c7310208df67/screenshots/Repadmin.png?raw=true" width="800" height="400">






          



