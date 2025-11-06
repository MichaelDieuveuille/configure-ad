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
