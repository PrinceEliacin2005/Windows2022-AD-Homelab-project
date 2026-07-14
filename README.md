# Active Directory Home Lab
### Enterprise IT Environment Simulation — Help Desk / IT Support Practice Project

This project simulates a small enterprise IT environment using Active Directory Domain Services (AD DS) on Windows Server. It was built to practice the core skills used by help desk and IT support technicians — from initial infrastructure setup through day-to-day account administration and policy configuration.

**Tech stack:** VirtualBox · Windows Server 2022 (Evaluation) · Active Directory Domain Services · Active Directory Administrative Center · Group Policy Management

**Skills demonstrated:** Domain controller deployment · OU design · User account lifecycle management · Password resets · Account enabling/disabling · Account unlocking · Fine-grained password policy configuration · Group Policy navigation · Security group management

---

## Part 1: Environment Setup — From Download to Domain Controller

### 1.1 Software & VM Setup
Downloaded and installed VirtualBox, downloaded the Windows Server 2022 Evaluation ISO, and created a new virtual machine (DC01) with 4096 MB RAM, 2 CPU cores, and a 60 GB dynamically allocated virtual disk.

![Oracle VirtualBox Manager](screenshots/01-virtualbox-manager.png)
![DC01 VM details, powering up](screenshots/02-vm-details-powering-up.png)
![Virtual hardware settings — 4096 MB base memory, 2 CPUs](screenshots/03-vm-hardware-settings.png)
![60 GB dynamically allocated virtual hard disk (VDI)](screenshots/04-vm-disk-60gb.png)

### 1.2 Windows Server Installation
Performed a manual install of Windows Server 2022 (Standard Evaluation, Desktop Experience) onto the VM — selecting "I don't have a product key," choosing the Desktop Experience edition, and installing to the unallocated 60 GB disk.

![Windows Setup — setting the built-in Administrator password](screenshots/05-windows-setup-admin-password.png)
![Server Manager dashboard on first launch](screenshots/06-server-manager-first-launch.png)

### 1.3 Installing the AD DS Role
Added the Active Directory Domain Services role via Server Manager's "Add Roles and Features" wizard.

![Add Roles and Features Wizard — Active Directory Domain Services selected](screenshots/07-addds-role-selected.png)

### 1.4 Promoting to a Domain Controller
Promoted the server to a domain controller, creating a new forest and domain (`homelab.local`), and set the Directory Services Restore Mode (DSRM) password.

![Post-deployment configuration notification — prompt to promote this server to a domain controller](screenshots/08-postdeploy-notification.png)
![Domain Controller Options — DNS server and Global Catalog enabled, DSRM password set](screenshots/09-dc-options-wizard.png)
![Server Manager confirms promotion succeeded — AD DS and DNS roles now installed](screenshots/10-dc-promotion-confirmed.png)
![Post-reboot login screen showing HOMELAB\Administrator — confirms the new domain is active](screenshots/11-domain-login-screen.png)

---

## Part 2: Organizational Unit (OU) Structure

Designed and built an OU structure to reflect a small business layout (HR, IT, Sales, Service Accounts, with an IT Managers sub-OU), used as the foundation for all user, group, and policy management below.

![OU tree in Active Directory Users and Computers — USA Branch with HR, IT, Sales, and Service Accounts sub-OUs (homelab.local)](screenshots/12-ou-tree.png)

---

## Part 3: User Account Management

### 3.1 Creating User Accounts
Created new user accounts within their appropriate OUs (e.g., "Prince IT" inside IT → IT Managers), setting logon names and initial account properties.

![New Object – User wizard, creating the "Prince IT" account in the IT Managers OU](screenshots/13-new-user-wizard.png)

### 3.2 Resetting Passwords
Practiced resetting user passwords via Active Directory Users and Computers — the most common Tier 1 help desk ticket type.

![Right-click → Reset Password on a user account](screenshots/14-reset-password-menu.png)

### 3.3 Enabling / Disabling Accounts
Practiced disabling and re-enabling accounts to simulate employee offboarding/onboarding scenarios.

![Right-click → Enable Account, re-activating a disabled user](screenshots/15-enable-account-menu.png)

### 3.4 Unlocking Locked-Out Accounts
Simulated an account lockout and practiced unlocking it via the Account tab — another frequent real-world help desk scenario.

![Unlock account checkbox on the Account tab of user properties](screenshots/16-unlock-account-checkbox.png)

### 3.5 Testing: New User Domain Login
Verified the new account actually works by logging in as "prince.IT" at the Windows login screen, confirming authentication against the homelab.local domain and the mandatory password change on first logon.

![Logging in as a new domain user (prince.IT) — prompted to set a new password at first logon](screenshots/17-new-user-domain-login-test.png)

---

## Part 4: Group Policy (GPO)

### 4.1 Navigation into GPO
Opened the Group Policy Management console from Server Manager's Tools menu and reviewed the default Group Policy Object for the homelab.local domain.

![Server Manager → Tools menu, where Group Policy Management and other AD tools are launched from](screenshots/18-gpo-tools-menu.png)
![Group Policy Management console — homelab.local Group Policy Object scope and security filtering](screenshots/19-gpo-console-scope.png)

### 4.2 Building a Password Policy
Created a Fine-Grained Password Policy (Password Settings Object) via the Active Directory Administrative Center, configuring minimum password length, password history, complexity requirements, and password age settings.

![Active Directory Administrative Center — Password Settings Container](screenshots/20-password-settings-container.png)
![Create Password Settings dialog — minimum length, password history, complexity, and password age configured](screenshots/21-password-settings-dialog.png)

---

## Part 5: Security Groups & Computers

Created a security group (IT MANAGERS) within the IT Managers OU to begin practicing role-based access management following least-privilege principles, along with a computer object for the group.

![IT Managers OU showing the IT MANAGERS security group alongside its member computer and users](screenshots/22-security-group-list.png)


## Troubleshooting

Hit a "Windows cannot find the Microsoft Software License Terms" error when using VirtualBox's unattended installation feature with the Windows Server 2022 ISO.

![Unattended installation error encountered mid-setup](screenshots/23-license-terms-error.png)

**Fix:** recreated the VM and, on the unattended install screen, selected the option to skip unattended installation entirely. This dropped into the standard graphical Windows Setup flow, which installed cleanly without further issues.

---

## Learning Materials

- [Active Directory at Work](https://www.youtube.com/watch?v=Yb__4XttW7g)
- [Creating Fine-Grained Password Policy in Windows Server 2012 R2](https://www.youtube.com/watch?v=JWsRbeeddfM&t=173s)
- [YouTube tutorial](https://www.youtube.com/watch?v=FsVuZ__vr2g)
- Claude AI

---

*This is a self-directed learning project built to practice real-world IT support and systems administration skills.*
