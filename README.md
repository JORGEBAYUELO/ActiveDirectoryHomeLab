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

## Overview of The Active Directory Home Lab

This home lab simulates a real-world **Windows Active Directory environment** using **VMware** **Workstation**. It consists of **two Windows Server VMs** (a **primary domain controller** and a backup for **failover scenarios**) plus **two client machines**. Through this setup, I gained hands-on experience with **Active Directory management,** **Group Policy configurations,** **Remote Desktop Protocol (RDP),** **user role management,** **and troubleshooting scenarios**.

The lab also features **osTicket,** an **open-source** **ticketing system,** which simulates **IT support and Help Desk workflows** while incorporating **PHP, MySQL, and IIS web server configurations.**

This environment provided valuable practical experience in **user support, ticketing management, software troubleshooting, and database administration.**

## You'll need the following:

To complete this lab setup, the following software and tools are required:

- **VMware Workstation** For creating virtual machines (You could also use VirtualBox)
- **Windows Server 2022** For Domain Controllers and Failover setup
- **Windows 11** For client machines
- **Active Directory Domain Services (AD DS)** Role for the domain controller
- **PHP 8.2**, **MySQL**, and **osTicket** For the ticketing system

## Step-by-Step Setup

### 1. Prepare VMware Workstation
- **Objective**: Set up VMware Workstation and create the VMs for primary server, secondary server (failover), and two client machines.
1. Open VMware Workstation
2. Verify that bridged networking is enabled. This ensures all VMs can communicate with each other and your host machine.
   - Go to Edit > Virtual Network Editor
   - Select the network adapter you want to use for bridged networking (by default vmnet0) and ensure it’s connected to the correct physical network.
     
     ![Screenshot From 2025-01-30 18-10-00](https://github.com/user-attachments/assets/7cfe2977-de17-4cc0-afe1-58f5afadf828)

### 2. Create the Virtual Machines
We’ll now create four virtual machines:
1. Windows Server (Domain Controller)
2. Windows Server (Failover Setup)
3. Client Machine 1
4. Client Machine 2

### 3. Create the First Virtual Machine (Windows Server)
1. Open VMware Workstation and click on File > New Virtual Machine.
2. Select Custom (advanced) and click Next.
   
![Screenshot From 2025-01-30 18-12-28](https://github.com/user-attachments/assets/38e536a1-ab55-4203-93dc-2fff0f454480)

3. For the hardware compatibility, choose the latest version supported by your VMware Workstation and click Next.

![Screenshot From 2025-01-30 18-18-30](https://github.com/user-attachments/assets/13d8b1b4-8a6b-4fe5-9b62-04f03cb3d68e)

4. Choose Install Operating System Later and click Next.

![Screenshot From 2025-01-30 18-18-38](https://github.com/user-attachments/assets/7e775530-d985-440f-8133-f2880ed88e00)

5. Select Microsoft Windows, and from the dropdown, select Windows Server 2022, then click Next.

![Screenshot From 2025-01-30 18-18-46](https://github.com/user-attachments/assets/3edfbdbb-a3a8-47cf-b0e2-187b383ed678)

6. Name your VM as “AD Home Lab - DC” (or similar) and choose a location for its files.

![Screenshot From 2025-01-30 18-19-52](https://github.com/user-attachments/assets/38e19d35-fd14-4bef-b104-bb3543b5c7ca)

7. Assign the VM:
   - 4 GB RAM
   - 2 Processors with 2 cores per processor

![Screenshot From 2025-01-30 18-20-15](https://github.com/user-attachments/assets/cb032b7c-09bb-4c8c-8537-18dd5710d2b0)

![Screenshot From 2025-01-30 18-20-26](https://github.com/user-attachments/assets/5568ef8b-f6fc-4920-bddc-87e7dcdeaaeb)

8. Select Use Bridged Networking for the network type.

![Screenshot From 2025-01-30 18-20-53](https://github.com/user-attachments/assets/62eced16-846f-45f9-81bf-c5869ff4dae5)

9. Create a new virtual disk with at least 60GB of storage and click Finish.

![Screenshot From 2025-01-30 18-21-06](https://github.com/user-attachments/assets/a5e81b75-9321-459e-a61b-18d90f9b7d60)

![Screenshot From 2025-01-30 18-21-18](https://github.com/user-attachments/assets/3f2d836a-2baf-4c79-8faf-de1b7e5a0a74)

![Screenshot From 2025-01-30 18-21-44](https://github.com/user-attachments/assets/7d2a5612-5c89-41f5-803f-410586eea6da)

### 4. Install Windows Server
1. Mount your Windows Server ISO to the VM’s CD/DVD drive.

![Screenshot From 2025-01-30 18-42-12](https://github.com/user-attachments/assets/cfc6e71e-9ba7-4df1-ab7e-08992b85e628)

2. Power on the VM and proceed with the Windows installation.

![Screenshot From 2025-01-30 18-43-09](https://github.com/user-attachments/assets/d371a694-315b-4219-aecd-d487f1b180b5)

3. During setup, choose a Custom Installation, create a partition, select Windows Server 2022 Standard Evaluation (Desktop Experience) which includes the GUI and complete the installation.

![Screenshot From 2025-01-30 18-43-18](https://github.com/user-attachments/assets/549ba836-6e63-46e0-8b0a-ca08fac7bc68)

![Screenshot From 2025-01-30 18-43-48](https://github.com/user-attachments/assets/3c5d62d9-cf5c-45c7-9212-5573d8a6fb75)

![Screenshot From 2025-01-30 18-44-07](https://github.com/user-attachments/assets/e794d526-aeda-405d-b822-7a3dbd633309)

![Screenshot From 2025-01-30 18-44-21](https://github.com/user-attachments/assets/375dde8d-0c89-4564-8f27-4449aa3a59e6)

![Screenshot From 2025-01-30 18-44-32](https://github.com/user-attachments/assets/7cdb6f35-1e5f-4d64-81e3-bc4b276b2027)

![Screenshot From 2025-01-30 18-44-40](https://github.com/user-attachments/assets/82c8e909-081e-4616-b417-a968e53572ff)

![Screenshot From 2025-01-30 18-47-44](https://github.com/user-attachments/assets/c6f92ef3-aa0e-4164-a71f-2909d1b49711)

![Screenshot From 2025-01-30 18-48-13](https://github.com/user-attachments/assets/68e4da8c-e794-4856-b388-9c371b064df4)

### 5. Configure the Domain Controller
We’ll now install the Active Directory Domain Services (AD DS) role and promote this server to a Domain Controller.
1. Open Server Manager

![Screenshot From 2025-01-30 18-48-40](https://github.com/user-attachments/assets/0c016ca3-f73f-49ec-8093-d82f89471a2f)

2. Click on “Add roles and features” from the dashboard.
3. In the wizard:
  - Click Next on the “Before You Begin” screen.

  ![Screenshot From 2025-01-30 18-50-11](https://github.com/user-attachments/assets/b9f7e1a3-dc6e-47d0-ae1e-6f3ac522183c)

  - Select Role-based or feature-based installation and click Next.

  ![Screenshot From 2025-01-30 18-50-26](https://github.com/user-attachments/assets/f69dea53-a199-44db-bdcd-100009974aad)

  - Confirm the local server is selected and click Next.

  ![Screenshot From 2025-01-30 18-50-47](https://github.com/user-attachments/assets/82d439e0-a7d6-4ab6-b96d-c01805e61058)

4. In the “Server Roles” section:
  - Check Active Directory Domain Services.
  - Click Add Features when prompted, then click Next.

  ![Screenshot From 2025-01-30 18-51-46](https://github.com/user-attachments/assets/eff8fdf9-02cb-4328-9753-625e028ea986)

5. Click Next on the “Features” screen.

![Screenshot From 2025-01-30 18-58-46](https://github.com/user-attachments/assets/796c4ead-fbf8-4640-8fc6-0ab16ae394f3)

6. On the “AD DS” screen, read the description and click Next.

![Screenshot From 2025-01-30 18-59-36](https://github.com/user-attachments/assets/c46ddd11-2ee9-4102-b34e-d39fa707129c)

7. Click Install on the confirmation screen (no need to restart yet).

![Screenshot From 2025-01-30 19-00-09](https://github.com/user-attachments/assets/6eafbacf-0507-4b4f-8742-94de7ebcc772)

### 6. Promote the Server to a Domain Controller
1. After Installation, a notification will appear in the top-right corner of Server Manager.
  - Click Promote this server to a domain controller.
    
  ![Screenshot From 2025-01-30 19-03-41](https://github.com/user-attachments/assets/960531b5-2092-4a2d-b362-d039d4b951e5)

2. In the Active Directory Domain Services Configuration Wizard:
  - Choose Add a new forest.
  - Enter a domain name (e.g., adlab.local) and click Next.
  
  ![Screenshot From 2025-01-30 19-05-01](https://github.com/user-attachments/assets/9ccbc45d-312a-49bf-8b4b-29722a204abe)

3. Set a Directory Services Restore Mode (DSRM) password, make sure Domain Name System (DNS) server and Global Catalog (GC) are checked and click Next.

![Screenshot From 2025-01-30 19-05-59](https://github.com/user-attachments/assets/85e70eb1-cee1-4549-9e6b-aa6a5d356244)

4. Proceed through the rest of the wizard with default settings (click Next until you reach the Install button).
5. Click Install to promote the server. The system will reboot when the installation is complete.

![Screenshot From 2025-01-30 19-08-01](https://github.com/user-attachments/assets/b6d99170-fe71-4e99-82e4-7a4313dbd940)

### 7. Verify and Configure Active Directory
Let’s verify the domain setup setup and configure additional features:
**Check Domain configuration**
1. Open Server Manager.
2. Click on Tools in the top-right corner and select Active Directory Users and Computers.

![Screenshot From 2025-01-30 19-13-27](https://github.com/user-attachments/assets/b0e9871d-53e5-41be-92fe-8c2d0fbf8352)

3. in the left pane:
  - Expand your domain (e.g., adlab.local or the name you choose).

  ![Screenshot From 2025-01-30 19-15-27](https://github.com/user-attachments/assets/f588f7ff-31cb-42f2-baa6-86e4801d1334)

**Create a Test User**
1. In Active Directory Users and Computers:
  - Right-click on Users (or create a new Organizational Unit [OU] for better organization).
  - Select New > Users.

  ![Screenshot From 2025-01-30 19-17-01](https://github.com/user-attachments/assets/601863c1-5313-4577-81f2-d3787576b5c0)

2. Fill in the user details:
  - Example: First Name: John, Last  Name: Doe, User logon name: jdoe.

  ![Screenshot From 2025-01-30 19-17-55](https://github.com/user-attachments/assets/991b9da0-9cbe-482e-b4f3-ed626e8a1fe1)\

3. Set a password and uncheck User must change password at next logon (optional for testing purposes).

![Screenshot From 2025-01-30 19-18-34](https://github.com/user-attachments/assets/1c1b2a36-a9f9-412d-bc97-df011c78468b)

4. Complete the wizard.

### 8. Enable Remote Desktop Protocol (RDP)
1. Open Server Manager and click Local Server on the left panel.
2. Find Remote Desktop, click Disabled, and enable it:
  - Check Allow remote connection to this computer.
  - (Optional) Uncheck Allow connections only from computers running Remote Desktop with Network Level Authentication for testing flexibility.

  ![Screenshot From 2025-01-30 19-21-33](https://github.com/user-attachments/assets/c565f6f5-6dda-404f-a95a-af3d9ea35bd8)

  ![Screenshot From 2025-01-30 19-22-29](https://github.com/user-attachments/assets/5a35cd08-dbad-4ddc-8302-a6e3abb7679b)

3. Apply the changes.

**Test RDP Connections**
Prepare the Server for RDP:
1. Ensure the John Doe user (or any test user you created) has permission to use Remote Desktop:
  - Open System Properties (right-click “This PC” > Properties > Remote Settings).

  ![Screenshot From 2025-01-30 19-24-12](https://github.com/user-attachments/assets/125c98bc-6c00-451f-9e09-28080feca02d)

2. In the Remote Desktop section, click Select Users.

  ![Screenshot From 2025-01-30 19-24-47](https://github.com/user-attachments/assets/255108cd-af40-4cab-ba27-85db67d04f65)

3. Add the John Doe user to the list of allowed users.

  ![Screenshot From 2025-01-30 19-25-08](https://github.com/user-attachments/assets/a50e96c3-d43d-440b-a3fc-19ad374f9a2b)

  ![Screenshot From 2025-01-30 19-25-21](https://github.com/user-attachments/assets/c6290db2-e6b9-4406-97e3-d600086cbf60)

  ![Screenshot From 2025-01-30 19-26-28](https://github.com/user-attachments/assets/06a4700f-38f7-4c84-a911-8892ddb9b7b4)

**Use RDP from Another Device**
Let’s now connect to the server using RDP from one of the client machines and the host machine:
1. Since I’m using Linux as host OS, I’ll be using an RDP client called Remmina.
  - Open Remmina

  ![Screenshot From 2025-01-30 19-28-16](https://github.com/user-attachments/assets/d82517e4-8dbb-4e95-bc36-8f253507abbe)

  - Enter the IP address of the server

  ![Screenshot From 2025-01-30 19-29-15](https://github.com/user-attachments/assets/306f99ef-f623-4e68-9bfb-3de449faef41)

  ![Screenshot From 2025-01-30 19-29-36](https://github.com/user-attachments/assets/ce4e7b09-24b1-46c7-b88f-3a2043d21e56)

  - User the John Doe account credentials (e.g., adlab\jdoe if your domain is adlab.local).

  ![Screenshot From 2025-01-30 19-31-07](https://github.com/user-attachments/assets/99179b29-bfcb-4053-b63c-187d20e2ccc9)

2. Test the connection.

![Screenshot From 2025-01-30 19-33-42](https://github.com/user-attachments/assets/b8befa9c-85a4-48ad-936a-6ee0a35f8cc1)

### 9. Create the Windows Clients VMs



































### 10. Final Validation and Verification
- **Objective**: Verify all configurations and ensure proper system functionality.
- **Action**: 
   - Test **Active Directory replication** and domain join functionality.
   - Test **osTicket** by submitting and resolving tickets.
   - Validate **failover** scenarios by simulating a Domain Controller failure.

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

