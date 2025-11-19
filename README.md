# Configuring Users and Groups in Active Directory

## Overview
In this repository, we configure user accounts, groups, and Organizational Units (OUs) in Active Directory within Azure VMs.

## Environments and Technologies Used
- Microsoft Azure VMs
- Windows Server
- Remote Desktop

## Operating Systems Used
- Windows Server 2019/2022
- Windows 10 (client)

## High-Level Steps
1.Set up Azure environment
Created a resource group, virtual network, and two virtual machines—one for the domain controller and one for a client system.

2.Configure networking for Active Directory
Assigned a static IP to the domain controller and updated the client’s DNS settings to point to the DC to enable domain communication.

3.Install and configure Active Directory
Installed Active Directory Domain Services, promoted the server to a domain controller, and created the domain structure.

4.Organize users using Organizational Units (OUs)
Created OUs for Employees, Admins, and Clients to organize user accounts and apply proper management policies.

5.Create and assign admin accounts
Added an administrative user (ken_admin) and assigned Domain Admin permissions to manage the environment securely.

6.Join the client machine to the domain
Connected the Windows 10 client VM to the new domain, enabling centralized authentication.

7.Enable remote access for domain users
Configured Remote Desktop access on the client machine for authorized domain users.

8.Automate user creation with PowerShell
Used a PowerShell script to automatically generate and create multiple user accounts in the Employees OU.

9.Verify successful Active Directory setup
Confirmed that users, groups, and OUs were created properly and ensured a script-generated user could log in from the client machine.

## Actions and Observations
<p>
<img width="2479" height="1108" alt="Screenshot 2025-11-18 171800" src="https://github.com/user-attachments/assets/dd907ef8-f978-4d08-8101-3f73f765843a" />
 
First, we will create a resource group in Microsoft Azure called "Active-Directory-Lab" where we will create two virtual machines inside the resource group.
</p>

<img width="2495" height="1095" alt="Screenshot 2025-11-18 171926" src="https://github.com/user-attachments/assets/f895a105-a497-4d2c-85ba-151c3f759789" />

Next, we will create a virtual network that is associated with the resource group "Active-Directory-Lab" and we will call the virtual network "Active-Directory-VNet".
</p>

<img width="2493" height="1158" alt="Screenshot 2025-11-18 172058" src="https://github.com/user-attachments/assets/66f7a836-71d9-4e8a-ad79-f29e6a9e60a7" />

Then, we will create a Virtual Machine and name it "dc-1" since this will be acting as the domain controller for our lab. The domain controller will be where we will install active directory on an admin account.
</p>

<img width="2504" height="1136" alt="Screenshot 2025-11-18 172628" src="https://github.com/user-attachments/assets/133ad37b-2dd3-4160-883c-7c103571138b" />
</p>
After that, we will create another virtual machine and name it "client-1" and this will be our user account. The user account will be a random user account created by powershell automation when we create organization units in the Active Directory Users and Computers.
</p>

<img width="2503" height="1289" alt="Screenshot 2025-11-18 175442" src="https://github.com/user-attachments/assets/6d2c28d4-29fe-4620-badd-6ca4831f0b55" />
</p>

Before we begin opening up the virtual machines, we need to configure the private address Ip settings for the dc-1 virtual machine from dynamic to static. This ensures the client machine can join the domain and use DC-1 as its DNS server. 
<p>
 
</p>
<img width="2505" height="1307" alt="Screenshot 2025-11-06 150541" src="https://github.com/user-attachments/assets/7f491ee1-c9d3-44b1-94dc-bab84cd997c8" />

</p>
<p>
In this step, we logged into the Windows Server VM that is acting as the domain controller using Remote Desktop. The screenshot shows the desktop environment after logging in. Ensure that you are logged in with administrative privileges to perform Active Directory tasks.
</p>
<br />
<img width="2558" height="1268" alt="Screenshot 2025-11-18 184747" src="https://github.com/user-attachments/assets/6ad2a323-c08b-4347-8fa6-9992643c9003" />

<p>
</p>

 Next, we'll RDP into the domain controller and disable the firewall for the domain, private, and public profiles. To do this, right-click the Windows symbol, select "Run," and type wf.msc. In the Windows Defender Firewall window, ensure the firewall is turned off for all profiles.
<p>
<img width="1333" height="690" alt="AD Portfolio 1" src="https://github.com/user-attachments/assets/8af0a4e4-7bb8-4790-bd9d-772efb384470" />

</p>
<p>
</p>

Next, we'll change the DNS server on Client1 to the static private IP address of DC-1 in the networking settings within the Azure portal. After making this change, restart the virtual machines to apply the new DNS configuration.



<img width="893" height="365" alt="AD Portfolio 2" src="https://github.com/user-attachments/assets/da0f64df-2f2a-4366-8138-c5e8a28a9cdf" />

<img width="858" height="736" alt="AD Portfolio 3" src="https://github.com/user-attachments/assets/3486039a-aa40-4f58-87d8-dc3978f4a076" />
<p>
 

Following that, we'll RDP into the Client1 virtual machine and attempt to ping DC-1's IP address using PowerShell. This should be successful since we disabled DC-1's firewall, allowing the machine to respond to the ping. We'll use the ipconfig /all command on Client1 to confirm that DC-1 is configured as the DNS server for the virtual machine.
<p>
 
<img width="789" height="562" alt="AD Portfolio 4" src="https://github.com/user-attachments/assets/e9a857cd-daeb-4cf4-9ab3-52325970eea0" />
<p>
 
Next, we'll install Active Directory Domain Services (AD DS) using the Server Manager on the domain controller. 
</p>

<img width="762" height="555" alt="AD Portfolio 5" src="https://github.com/user-attachments/assets/b159512b-51ca-4167-b3b2-846fb128ff88" />
<p>
 
We'll promote DC-1 to a Domain Controller and set up a new forest with the domain name mydomain.com. 
<p>
 
</p>
<img width="765" height="531" alt="AD Portfolio 6" src="https://github.com/user-attachments/assets/218d1020-7181-4c69-b78b-81b2e316d3d7" />
<p>
 
</p>
Next, we'll open Active Directory Users and Computers and create two organizational units, _EMPLOYEES and _ADMINS, by right-clicking mydomain.com, selecting New, and then choosing Organizational Unit.


</p>
<img width="438" height="377" alt="AD Portfolio 7" src="https://github.com/user-attachments/assets/88cb89d1-5b66-424a-b6b0-f87dca8abfe5" />
<p>
 
</p>
In the Admins OU, we'll create a new user named Ken Doe with the username ken_admin. 
<P>
 
</P>
<img width="827" height="724" alt="AD portfolio 8" src="https://github.com/user-attachments/assets/df6b7dac-dd41-43bc-ad5f-0c31aa19491e" />

</p>

 Next, we'll add Ken Doe as a Domain Admin. Right-click the user, select Properties, navigate to the Member Of tab, and click Add. In the "Enter object names" field, type Domain Admins and press Enter to complete the process.

<img width="455" height="557" alt="AD Portfolio 9" src="https://github.com/user-attachments/assets/835481a9-e810-417d-b79b-a4447e089873" />

<p>
 
</p>

Now, log out of DC-1 and reconnect using RDP with the credentials mydomain.com\ken_admin and the assigned password. This account will be used for all future logins to DC-1. 


<img width="1201" height="656" alt="AD Portfolio 10" src="https://github.com/user-attachments/assets/312d4b32-591e-4ae9-9ac7-88a8f3485e0f" />
<p>
 
</p>

Now, we'll join the domain from the Client1 VM. RDP into the system, right-click the Windows logo, select System, then click Rename this PC (Advanced). Next, click Change, select Domain, and enter the domain name mydomain.com. The VM will restart to apply the changes. 


<img width="757" height="530" alt="AD Portfolio 11" src="https://github.com/user-attachments/assets/08ff45dd-2ed9-46e6-837b-0a96107ab6d9" />
<p>
 
</p>

Go back to DC-1 and open Active Directory Users and Computers. Create another organizational unit named _CLIENTS under mydomain.com.
 
<img width="1226" height="930" alt="AD Portfolio 12" src="https://github.com/user-attachments/assets/f44ebe13-22f5-4d03-b4ee-41f3a24bdd8a" />
<p>
 
</p>

Next, log into the Client1 VM as ken_admin. Right-click the Windows logo, select System, then choose Remote Desktop. Click Select users that can remotely access this PC and add Domain Users to allow them RDP access to the VM.

<img width="1309" height="855" alt="AD Portfolio 13" src="https://github.com/user-attachments/assets/062c3dad-51d5-4172-a17a-ca6c7b9c2c1a" />
<p>

 https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1 Log in to DC-1 as ken_admin and open PowerShell ISE as an administrator. Create a new file, paste the script into it, and execute it. Observe as the accounts are created automatically.
 <p>
 
 </p>
<img width="431" height="370" alt="AD Portfolio 14" src="https://github.com/user-attachments/assets/40398af5-c139-4942-a292-37155d4b7edc" />
<P>
 
</P>

After running the script, open Active Directory Users and Computers (ADUC) and verify that the accounts have been created in the appropriate _EMPLOYEES organizational unit.

<img width="869" height="734" alt="AD Portfolio 15" src="https://github.com/user-attachments/assets/9eaea62c-c850-49b8-bafa-13cb4098e634" />
<p>

</p>

Lastly, log in to the Client1 VM using one of the user accounts created by the PowerShell script, with the username and default password Password1. After logging in, open PowerShell to verify that you are logged in as one of the script-created users.




