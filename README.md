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
- Users were successfully created and grouped.
- Verified access control using test client VM.
- Observed Group Policy inheritance and security permissions.
