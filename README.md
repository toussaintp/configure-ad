<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2025
- Windows 10 (21H2)

  <h2>Project Objectives</h2>

- Create Azure Virtual Machines for a Domain Controller and Client Computer
- Configure networking and DNS settings between virtual machines
- Install and configure Active Directory Domain Services (AD DS)
- Promote a Windows Server to a Domain Controller
- Join a Windows 10 client computer to the domain
- Verify domain connectivity and authentication
- Prepare the environment for user and group management

<h2>High-Level Deployment and Configuration Steps</h2>

- Create Azure Resource Group and Virtual Network
- Deploy Windows Server and Windows 10 Virtual Machines
- Configure the Domain Controller and install Active Directory Domain Services
- Join the Client Computer to the Domain and verify connectivity

<h2>Deployment and Configuration Steps</h2>

<p>
Step 1: Create Azure Resource Group and Virtual Network
</p>
<p>
<img width="1364" height="286" alt="1-resource group" src="https://github.com/user-attachments/assets/4b9a2b2f-f8f5-4afa-a7fc-2e3259cf0561" />
</p>
<p>
<img width="1195" height="372" alt="2- virtual network" src="https://github.com/user-attachments/assets/b2414c3e-b8ac-4e7f-94b4-cc3ebef25276" />
</p>

<p>
What was done:
Created a Resource Group and Virtual Network in Azure to host all resources required for the Active Directory environment.
  
Why it matters:
The Virtual Network provides secure communication between virtual machines, while the Resource Group helps organize and manage cloud resources efficiently.
</p>
<br />

<p>
Step 2: Create the Domain Controller VM (DC-1)
</p>
<p>
<img width="1178" height="499" alt="3- dc1" src="https://github.com/user-attachments/assets/cbf200bb-1f3f-4f62-8e2b-ab17647d6791" />
</p>

<p>
What was done:
Deployed a Windows Server 2022 virtual machine and configured a static private IP address to serve as the Domain Controller.

Why it matters:
A Domain Controller provides centralized authentication, authorization, and directory services. A static IP address ensures clients can consistently locate domain and DNS services.
</p>
<br />

<p>
Step 3: Create the Client VM (Client-1)
</p>
<p>
<img width="1199" height="458" alt="4 - client 1" src="https://github.com/user-attachments/assets/7db93827-3316-4fb6-9ee3-d899416b5a87" />
</p>
<p>
  
What was done:
Deployed a Windows 10 virtual machine within the same Virtual Network as the Domain Controller.

Why it matters:
This machine simulates a workstation in a corporate environment and will later be joined to the Active Directory domain for centralized management.
</p>
<br />

<p>
Step 4: Set DC-1 NIC Private address to be static
</p>
<p>
<img width="573" height="668" alt="5 - dc1 Nic static" src="https://github.com/user-attachments/assets/03a20566-17b5-4e2b-9587-9caea8618c0d" />
</p>

<p>
What was done:
The Network Interface Card (NIC) of the Domain Controller (DC-1) was configured with a static private IP address within Azure. This ensures that the server always uses the same internal network address.

Why it matters:
Domain Controllers provide critical services such as Active Directory and DNS. If the server's IP address changes, client computers may be unable to locate the Domain Controller, causing authentication, DNS resolution, and domain-related services to fail. Assigning a static IP address ensures reliable communication and consistent access to network services throughout the environment.
</p>
<br />

<p>
Step 5: Disable DC-1  windows Firewall
</p>
<p>
<img width="912" height="731" alt="6 - firewall off" src="https://github.com/user-attachments/assets/67308905-8bb1-4fdc-8f5e-af42294242d5" />
</p>

<p>
What was done:
Logged into the Domain Controller (DC-1) and temporarily disabled the Windows Defender Firewall on all network profiles (Domain, Private, and Public) to test network communication between virtual machines.

Why it matters:
Disabling the firewall during initial setup helps determine whether connectivity issues are being caused by firewall rules or by network configuration problems. This allows administrators to verify that Client-1 can successfully communicate with DC-1 before implementing more restrictive security settings. In a production environment, the firewall would typically remain enabled with properly configured rules rather than being permanently disabled.
</p>
<br />

<p>
Step 6: Configure DNS Settings
</p>
<p>
<img width="737" height="622" alt="7 - client 1 to dc 1 dns" src="https://github.com/user-attachments/assets/317e5729-e551-4e39-9646-0acab99cc6de" />
</p>

<p>
What was done:
Configured the client machine to use the Domain Controller's private IP address as its primary DNS server.
  
Why it matters:
Active Directory relies heavily on DNS to locate domain resources and services. Without proper DNS configuration, domain joins and authentication will fail.
</p>
<br />

<p>
Step 7: Restart Client-1
</p>
<p>
<img width="956" height="326" alt="8 - client1 restart" src="https://github.com/user-attachments/assets/dab8ca97-b0a3-4522-8ab9-8b17cba7c0c2" />
</p>

<p>
What was done:
Restarted the Client-1 virtual machine through the Azure Portal after completing network and Domain Controller configuration changes.
  
Why it matters:
Restarting the client ensures that any recent network configuration changes, such as DNS settings or connectivity updates, are fully applied. This helps guarantee that the client machine can properly communicate with the Domain Controller and accurately recognize Active Directory services before proceeding with domain-related tasks.
</p>
<br />

<p>
Step 8: Verify Network Connectivity
</p>
<p>
<img width="630" height="705" alt="9 - client 1 connectivity " src="https://github.com/user-attachments/assets/25bbc140-40f8-49fd-99b7-0d33121e5210" />
</p>

<p>
What was done:
Used Remote Desktop and network testing tools to confirm communication between the client and server machines.

Why it matters:
Verifying connectivity ensures that domain services, DNS resolution, and authentication requests can successfully travel across the network.
</p>
<br />

<h2>Final Result</h2>

<p>
A fully functional on-premises Active Directory environment was successfully deployed within Microsoft Azure. A Windows Server 2025 virtual machine was configured as a Domain Controller, Active Directory Domain Services were installed, and a Windows 10 client machine was successfully joined to the domain. 
</p>

<h2>Skills Demonstrated</h2>

- Microsoft Azure Virtual Machine Deployment
- Virtual Network Configuration
- Windows Server Administration
- Active Directory Domain Services (AD DS)
- Domain Controller Deployment
- DNS Configuration and Troubleshooting
