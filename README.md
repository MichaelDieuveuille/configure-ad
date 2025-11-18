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
1. Log into the domain controller VM.
2. Create Organizational Units for departments.
3. Add users to respective OUs.
4. Create security groups and assign users.

## Actions and Observations
<p>
<img width="2479" height="1108" alt="Screenshot 2025-11-18 171800" src="https://github.com/user-attachments/assets/dd907ef8-f978-4d08-8101-3f73f765843a" />
First, we will create a resource group in Microsoft Azure called "Active-Directory-Lab" where we will create two virtual machines inside the resource group.
</p>

<img width="2495" height="1095" alt="Screenshot 2025-11-18 171926" src="https://github.com/user-attachments/assets/f895a105-a497-4d2c-85ba-151c3f759789" />

Next, we will create a virtual network that is associated with the resource group "Active-Directory-Lab" and we will call the virtual network "Active-Directory-VNet".
</p>

<img width="2493" height="1158" alt="Screenshot 2025-11-18 172058" src="https://github.com/user-attachments/assets/66f7a836-71d9-4e8a-ad79-f29e6a9e60a7" />
</p>
Then, we will create a Virtual Machine and name it "dc-1" since this will be acting as the domain controller for our lab. The domain controller will be where we will install active directory on an admin account.


<img width="2504" height="1136" alt="Screenshot 2025-11-18 172628" src="https://github.com/user-attachments/assets/133ad37b-2dd3-4160-883c-7c103571138b" />
</p>
After that, we will create another virtual machine and name it "client-1" and this will be our user account. The user account will be a random user account created by powershell automation when we create organization units in the Active Directory Users and Computers.
</p>

<img width="2503" height="1289" alt="Screenshot 2025-11-18 175442" src="https://github.com/user-attachments/assets/6d2c28d4-29fe-4620-badd-6ca4831f0b55" />
</p>
Before we begin opening up the virtual machines, we need to configure the private address Ip settings for the dc-1 virtual machine from dynamic to static. This ensures the client machine can join the domain and use DC-1 as its DNS server. 
<img width="2505" height="1307" alt="Screenshot 2025-11-06 150541" src="https://github.com/user-attachments/assets/9f22098a-024b-45ff-bf71-e16f98e3f25e" />

</p>
<p>
In this step, we logged into the Windows Server VM that is acting as the domain controller using Remote Desktop. The screenshot shows the desktop environment after logging in. Ensure that you are logged in with administrative privileges to perform Active Directory tasks.
</p>
<br />

<p>
<img width="2559" height="1282" alt="Screenshot 2025-11-06 152223" src="https://github.com/user-attachments/assets/6ec73874-9376-460b-8cc4-b83675e56fdc" />

</p>
<p>
This screenshot shows the Active Directory Users and Computers (ADUC) console. We created Organizational Units (OUs) to organize users based on departments (e.g., Admins, Clients, Employees). OUs help manage permissions and group policies efficiently.
</p>
<br />

<p>
<img width="2559" height="1282" alt="Screenshot 2025-11-06 152428" src="https://github.com/user-attachments/assets/b248abc5-69d8-41e5-839f-6613badf4e9f" />

</p>
<p>
After creating OUs, we added individual user accounts to their respective OUs. The screenshot displays the “New User” dialog where we specify the username, full name, and password. This ensures that each user is correctly associated with the proper department OU.
</p>
<br />
