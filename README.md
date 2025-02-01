# Windows Active Directory Home Lab Setup

This repository contains detailed instructions for setting up a **Windows Active Directory Home Lab** using VMware Workstation. The lab includes a primary domain controller, a secondary domain controller for failover scenarios, and two client machines. Additionally, we set up **osTicket**, a web-based ticketing system, integrated into the Active Directory environment.

## Table of Contents

- [Overview](#overview)
- [Requirements](#requirements)
- [Step-by-Step Setup](#step-by-step-setup)
  - [VMware Configuration](#1-vmware-configuration)
  - [Installing Windows Server](#2-installing-windows-server)
  - [Configuring Active Directory (Primary Server)](#3-configuring-active-directory-primary-server)
  - [Configuring Failover Scenarios (Secondary Server)](#4-configuring-failover-scenarios-secondary-server)
  - [Configuring Client Machines](#5-configuring-client-machines)
  - [Group Policy Configuration](#6-group-policy-configuration)
  - [Simulating Failover Scenarios](#7-simulating-failover-scenarios)
  - [Installing osTicket](#8-installing-osticket-ticketing-system)
  - [Testing Ticketing System](#9-testing-ticketing-system)
  - [Final Validation and Verification](#10-final-validation-and-verification)
- [Contributing](#contributing)
- [License](#license)

## Overview

This home lab setup uses **VMware Workstation** to simulate a Windows Server 2022 environment with **Active Directory**. We’ve included multiple VMs, one for the primary domain controller (DC) and another for the secondary DC, simulating a failover setup. Additionally, two client machines are used to test Active Directory functionalities, and **osTicket** is installed to simulate a ticketing workflow.

## Requirements

To complete this lab setup, the following software and tools are required:

- **VMware Workstation** (for creating virtual machines)
- **Windows Server 2022** (for Domain Controllers and Failover setup)
- **Windows 10** (for client machines)
- **Active Directory Domain Services (AD DS)** role for the domain controller
- **PHP 8.2**, **MySQL**, and **osTicket** for the ticketing system

## Step-by-Step Setup

### 1. VMware Configuration
- **Objective**: Set up VMware Workstation and create the VMs for primary server, secondary server (failover), and two client machines.
- **Action**: 
   - Install VMware Workstation.
   - Create 4 VMs:
     - **Primary Server VM** (Windows Server 2022).
     - **Secondary Server VM** (Windows Server 2022).
     - **Two Client VMs** (Windows 10).

### 2. Installing Windows Server
- **Objective**: Install **Windows Server 2022** on both server VMs.
- **Action**: 
   - Follow installation procedures for Windows Server 2022.
   - Set up basic configurations for both server VMs.

### 3. Configuring Active Directory (Primary Server)
- **Objective**: Set up **Active Directory Domain Services (AD DS)** on the primary server.
- **Action**: 
   - Promote the **Primary Server VM** to a Domain Controller.
   - Create the domain `lab.local` and configure DNS.

### 4. Configuring Failover Scenarios (Secondary Server)
- **Objective**: Set up the **Secondary Server VM** to handle failovers.
- **Action**: 
   - Install **AD DS** on the Secondary Server VM and configure it as a **Read-Only Domain Controller (RODC)**.
   - Set up replication between the Primary and Secondary Domain Controllers.
   - Simulate failover scenarios to ensure backup functionality.

### 5. Configuring Client Machines
- **Objective**: Add two client VMs to the domain.
- **Action**: 
   - Join **two Windows 10 client VMs** to the `lab.local` domain.
   - Test user login and domain communication.

### 6. Group Policy Configuration
- **Objective**: Implement **Group Policies** to manage client machines.
- **Action**: 
   - Create Organizational Units (OUs) for users and groups.
   - Implement **Group Policy Objects (GPOs)** to enforce domain policies like password complexity and user restrictions.

### 7. Simulating Failover Scenarios
- **Objective**: Test the failover setup between the primary and secondary domain controllers.
- **Action**: 
   - Simulate a server failure on the Primary Domain Controller.
   - Verify that the Secondary Domain Controller takes over successfully and that Active Directory replication is intact.

### 8. Installing osTicket (Ticketing System)
- **Objective**: Set up **osTicket** for handling IT support tickets.
- **Action**: 
   - Install **IIS** on the Secondary Server VM.
   - Configure **PHP 8.2** for IIS and enable necessary extensions.
   - Set up **MySQL** and create a database for **osTicket**.
   - Install **osTicket** and configure it for use in the environment.

### 9. Testing Ticketing System
- **Objective**: Test the functionality of **osTicket** in a domain-joined environment.
- **Action**: 
   - Submit test tickets via **osTicket** (e.g., password reset request).
   - Resolve tickets by performing corresponding actions in **Active Directory**.
   - Test the entire workflow to ensure smooth integration with the domain environment.

### 10. Final Validation and Verification
- **Objective**: Verify all configurations and ensure proper system functionality.
- **Action**: 
   - Test **Active Directory replication** and domain join functionality.
   - Test **osTicket** by submitting and resolving tickets.
   - Validate **failover** scenarios by simulating a Domain Controller failure.

## Contributing

If you'd like to contribute to this project or suggest improvements, feel free to fork the repository and submit a pull request with your changes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

Feel free to copy and paste this README.md into your GitHub repository! Let me know if you need further adjustments.
