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
<img width="1033" alt="Screenshot 2025-03-03 at 5 54 46 PM" src="https://github.com/user-attachments/assets/fe61e967-79b0-4040-8795-10069bf0d491" />
<img width="1440" alt="Screenshot 2025-03-03 at 6 06 06 PM" src="https://github.com/user-attachments/assets/e415ad5d-2d8c-4097-aeb5-bfeab6a3c227" />
</p>
<p>
First begin by creating your VMs. One will be our client and the next will be our Domain Controller. We will then connect the DNS of the Domain Controller to our Client-1. 
</p>
<br />

<p><img width="1013" alt="Screenshot 2025-03-03 at 8 30 49 PM" src="https://github.com/user-attachments/assets/65c788cd-2942-49cc-8131-e9cf1b2f233f" />
<img width="1440" alt="Screenshot 2025-03-03 at 6 59 35 PM" src="https://github.com/user-attachments/assets/f5ae425c-9cc2-448c-9b3a-3d2f3e0e60dd" />

</p>
<p>
Next, we will get logged in to our VMs. Once logged in, we will install Active Directory into our DC. After that, we will create our own admin user, which we named Jane Doe. 
</p>
<br />

<p><img width="1440" alt="Screenshot 2025-03-03 at 7 28 04 PM" src="https://github.com/user-attachments/assets/0c7aab3e-0275-4a15-97df-8999c02cb79b" />
<img width="1440" alt="Screenshot 2025-03-03 at 7 30 30 PM" src="https://github.com/user-attachments/assets/b274d32d-9d2b-4fb2-8095-69ee445f4875" />
</p>
<p>
Next, we ran a script that will create 10,000 users within our Active Directory. These users we will use to acknowledge what can be done with AD.  
</p>
<br />

<p><img width="1440" alt="Screenshot 2025-03-03 at 7 57 32 PM" src="https://github.com/user-attachments/assets/3546a436-6af2-4b5b-863f-b4b6082c7371" />
<img width="384" alt="Screenshot 2025-03-03 at 8 06 01 PM" src="https://github.com/user-attachments/assets/eb261a72-16a8-4dd7-b5c5-341d9611adc2" />
<img width="949" alt="Screenshot 2025-03-03 at 8 08 22 PM" src="https://github.com/user-attachments/assets/ea2eea5c-8fe6-4cf5-bad9-caae6e162695" />
<img width="720" alt="Screenshot 2025-03-03 at 8 09 45 PM" src="https://github.com/user-attachments/assets/b7e4efe1-f4e2-4089-b7d2-31a52a1e40a5" />
<img width="616" alt="Screenshot 2025-03-03 at 8 10 48 PM" src="https://github.com/user-attachments/assets/3d28dd8f-aa30-40fd-9e78-2993ef88300e" />
</p>
<p>
  Now that we have created our users, we can begin to look at what features are offered in AD. We can set password lockouts, disable accounts, reset passwords, and unlock accounts that have been locked out due to a user forgetting their password. 
</p>
