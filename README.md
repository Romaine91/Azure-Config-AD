# Azure-Config-AD
Tutorial Setting up Active Directory in Azure
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

- Windows Server 2022
- Windows 10 (Pro)

<h2> Deployment and Configuration Steps</h2>

- Step 1: Create Two VMs and Make sure VMs are on the same subnet
- Step 2: Test VMs Online Connectivity
- Step 3: Allow Permissions on DC-1's Firewall
- Step 4: Test Communication between VMs
- Step 5: Set up Domain
- Step 6: Created Organizational Units (OU) in Active Directory 
- Step 7: Join Client-1 to Domain
- Step 8: Setup Remote Desktop for Non-Admin Users on Client-1
- Step 9: Create Additional Users via Powershell ISE 
- Step 10: Test New User Accounts 

<h2>Deployment and Configuration Steps</h2>

Step 1: Log into Azure --> search "virtual machines" --> click "create Azure virtual machine" to create VM#1. Name this first virtual machine "DC-1" using your current region --> Set the image type as "Windows Server 2022" (effectively making it a domain for the lab) --> Set username and password --> Create VM #2 --> Title it "Client-1" (repeat the same steps used to create VM#1 except for the image type select "Windows 10 pro" since this VM will be the employees'/client's computer).

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/03ec6392-3e26-41d1-9327-844d8cc30293)



  
Step 2: Go to DC-1's network settings --> select networking --> click the hyperlink next to "network interface" --> "IP Configurations" --> "ipconfig1" --> change the assignment from dynamic to static (this ensures DC-1's IP address will not change) --> check the NIC settings to make sure both VMs are on the same "Vnet". This will ensure both VMs can communicate & connect with each other later in this lab.

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/8a21e37c-d8d9-4884-96d6-061c86a28d41)



  
Step 3: Remote Desktop into DC-1 via Windows firewall security settings -> Advanced settings --> inbound/outbound rules to allow "IPV4 permissions" on DC-1's Firewall. This will open the firewall for connectivity after DC-1 is converted into a domain. 

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/d58571a2-65b5-4308-912a-5088ac49a86e)



  
Step 4: Ensure communication between both VMs via perpetual ping using     
  cmd:ping -t (IP Address).
  

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/fc4839c0-3819-4c8c-b29e-fa3678af22f1)



  
Step 5: Install "Active Directory" on DC-1. Set up DC-1 as a new domain.

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/84b1ca6c-6ed7-4ed9-b8d8-9064a3add382)



  
Step 6: Remote Desktop into DC-1 to create two "Organizational Units" (OU), one titled "_Admins" and another titled "_Employees" within Active Directory.

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/951a15b9-c011-4980-b931-1c3925d9c3d1)


  
Step 7: Change Client-1's "DNS settings" in Azure to match the same private IP Address as DC-1 via network settings in DC-1. Go into Client-1's network settings -> Network Interface (NIC) --> DNS server -> Custom DNS settings -> Add DC-1's private IP Address as the DNS server to connect to for Client-1. Restart Client-1 to flush the DNS cache -> change Client-1 to the same domain as DC-1 via "about PC" -> rename this PC advanced -> type DC-1's domain name under the "domain section" -> create a new OU named "_clients".

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/5e341020-7593-4eaa-b2f5-80dfa18ccc99)


![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/b59f3323-655d-4cf6-af3c-b92d8d1550ae)




Step 8: Use Remote Desktop in the system settings to allow domain users access for all non-admin users on Client-1 VM under "user accounts" -> "select users that can remotely access this PC" -> click "add" and type in "domain users". 


![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/e21547c5-4213-494d-952f-b5c64bd5a760)




Step 9: Use a random account-generating script to create at least 100 users for this lab. Upload script via "Powershell ISE" (run as administrator) to Client-1. This will create 100 new users with random names. This is done to simulate employees within the company.

  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/4e6fb124-3d1d-4217-bc77-490a4381134d)


  
Step 10: Log into any newly generated user account on Client-1 VM. The login attempt with the user's name & generic password should be successful. That is the conclusion of this lab.
  
  ![image](https://github.com/Romaine91/Azure-Config-AD/assets/173863740/e8fbe9e3-dc8f-4107-b278-b030dc281b1c)

