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
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Resource Group, VM, VNet
- Connect Client 1's DNS to Private IP of Domain Controller VM
- Install Active Directory
- Create a domain user along with additional users
- Observe Active Directory by setting up Group Policy, enabling lock out, enabling and disabling, etc. 

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="1440" alt="Screenshot 2025-03-13 at 7 18 20 PM" src="https://github.com/user-attachments/assets/38055cd6-8e64-4d4a-9211-e4c25657b29e" />
</p>
<p>
  <img width="1440" alt="Screenshot 2025-03-13 at 7 18 29 PM" src="https://github.com/user-attachments/assets/8a0e0475-4878-4953-823d-df3abdbb96e1" />
</p>
<p>
 <img width="1440" alt="Screenshot 2025-03-13 at 7 19 46 PM" src="https://github.com/user-attachments/assets/4de42e33-fa84-41a4-be4e-5dab463ea9c0" />
  <img width="587" alt="Screenshot 2025-03-13 at 7 27 04 PM" src="https://github.com/user-attachments/assets/94b83e17-9293-4058-a845-a8bba9e473ec" />
  <img width="470" alt="Screenshot 2025-03-13 at 7 27 42 PM" src="https://github.com/user-attachments/assets/509e077b-51d9-4cb2-acff-4c9c3807832a" />
</p>
<p>
First, create a Resource Group in Microsoft Azure and name it "Active-Directory-Lab". Then, create a virtual network with the same name. Then, create a virtual machine and name it "DC-1". This will be our domain controller for this lab. Make sure that before you create DC-1, the VNet is the one that you created prior. After this, go to "Network Settings" within DC-1, go to ip-config, edit this and make the IP address static. Final step here is to log in to the VM in Remote Desktop and disable the firewall. 
</p>
<br />
<p>
  Once you are logged in to your VM, right-click the Start menu and click on "System", this will verify that you are running Windows Server on this DC-1. Next, right-click the Start menu and click "Run". Then, type "wf.msc". This will open up Windows Firewall. Then click on the circled portion of the picture below. This will take you to the "Properties" menu, be sure to turn off all of the firewall states in each of profile tabs. Then click "Apply" and "Okay". Congrats, you have disabled the firewall. 
</p>
<p>
  <img width="412" alt="Screenshot 2025-03-13 at 7 35 26 PM" src="https://github.com/user-attachments/assets/08c05293-30e2-4b95-8eac-e33603c358ee" />
  <img width="1040" alt="Screenshot 2025-03-13 at 7 36 37 PM" src="https://github.com/user-attachments/assets/36b0eb70-8550-4fe3-a44f-833b50aac81a" />
  <img width="399" alt="Screenshot 2025-03-13 at 7 50 49 PM" src="https://github.com/user-attachments/assets/37ac5937-dbe5-4384-b627-d87251747728" />
</p>
<br/>
<p>
  Next, create client-1. This will be a Windows 10 VM that we will use as an end-user. So, create a 2vcpu Windows 10 VM in Azure. Make sure that your region is the same as DC-1. Once client-1 is running, copy dc-1's private IP address to the DNS server of client-1. To do this, go to client-1, then to "Network Settings", and click on the virtual "NIC", then "DNS Servers", click "Custom" and copy and paste in the private IP address and click save. You will then need to restart the client-1 VM. Then, login to client-1 for the first time and attempt to ping dc-1 from client-1 in Powershell. 
</p>
<p>
  <img width="847" alt="Screenshot 2025-03-13 at 7 54 20 PM" src="https://github.com/user-attachments/assets/45ccc958-a702-4719-abfb-b5ce87fb7236" />
  <img width="661" alt="Screenshot 2025-03-13 at 7 59 29 PM" src="https://github.com/user-attachments/assets/7502109c-899b-49ce-a10b-831096b41b86" />
  <img width="727" alt="Screenshot 2025-03-13 at 8 00 46 PM" src="https://github.com/user-attachments/assets/88786595-40f6-4169-b1d0-1930b67fadb9" />
<img width="858" alt="Screenshot 2025-03-13 at 8 20 08 PM" src="https://github.com/user-attachments/assets/ef3e34cb-2b4a-4379-b2bb-b62c687ed9d0" />
</p>
<p>
  If you see something like this in Powershell, then you have completed these steps correctly!
</p>
<br/>
<p>
  In Powershell, type "ipconfig /all. This command should show the DNS setting set to DC-1's private IP address!
</p>
<p>
  <img width="672" alt="Screenshot 2025-03-13 at 8 28 08 PM copy" src="https://github.com/user-attachments/assets/bf533a2b-90a6-4bef-885c-6c44666e9b8b" />
</p>
<br/>

