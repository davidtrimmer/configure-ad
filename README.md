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
<p>
  Next, we will install Active Directory Domain Services in our DC-1. Since we are using Windows Server, we can click on Server Manager, and click "Add roles and features". This will open a window, go down to "Active Directory Domain Services" and make sure the dot is filled in. Then click "Next" until AD installs. 
</p>
<p>
  <img width="454" alt="Screenshot 2025-03-16 at 6 11 36 PM" src="https://github.com/user-attachments/assets/6e475af1-fc5c-4db2-9db3-8fc97a099f54" />
  <img width="782" alt="Screenshot 2025-03-16 at 6 12 53 PM" src="https://github.com/user-attachments/assets/d204ecac-ca80-4fcd-9aaf-f0c356bf426d" />
  <img width="786" alt="Screenshot 2025-03-16 at 6 13 22 PM" src="https://github.com/user-attachments/assets/fbaa4d9a-c49f-4883-aaea-be79a220c502" />
<img width="789" alt="Screenshot 2025-03-16 at 6 17 06 PM" src="https://github.com/user-attachments/assets/b747d5b9-725e-4f7d-bf4f-2608c2af49c3" />
</p>
<br/>
<p>
  Next, we will turn the dc-1 VM into a domain controller. While you are in Server Manager, go to the flag on the top right hand side. Click on "Promote to domain controller". Then click "Create new forest" and name the domain. Then set a password. Then all it to run. It should restart your VM. 
</p>
<p>
  <img width="343" alt="Screenshot 2025-03-16 at 6 18 08 PM" src="https://github.com/user-attachments/assets/4903a698-fca5-4260-8bea-363182eeda1b" />
<img width="759" alt="Screenshot 2025-03-16 at 6 18 19 PM" src="https://github.com/user-attachments/assets/1b9c1217-e5d4-4936-be9f-e328488ec9fd" />
<img width="444" alt="Screenshot 2025-03-16 at 6 18 30 PM" src="https://github.com/user-attachments/assets/2a86aef3-189c-4b47-a6cd-16687c47143b" />
<img width="753" alt="Screenshot 2025-03-16 at 6 19 54 PM" src="https://github.com/user-attachments/assets/d7080e6d-7915-44d6-b7e1-5b678ce7962f" />
</p>
<br/>
<p>
  Next, we will create a domain admin user within the domain. To do this, first create a Organizational Unit called ""_EMPLOYEES" in Active Directory Users and Computers. Next, create another OU and name it "_Admins". Make sure you right click on the "mydomain" area on the left-hand side of the ADUC window.
</p>
<p>
  <img width="361" alt="Screenshot 2025-03-16 at 6 33 01 PM" src="https://github.com/user-attachments/assets/8186e84d-eef9-4401-99ab-ac9c3bbae9e0" />
<img width="749" alt="Screenshot 2025-03-16 at 6 34 20 PM" src="https://github.com/user-attachments/assets/05efcafe-8f12-4bfb-969f-a9ba71fbf5f5" />
<img width="200" alt="Screenshot 2025-03-16 at 6 35 14 PM" src="https://github.com/user-attachments/assets/b064435c-de37-4110-8210-79b386242247" />
<img width="748" alt="Screenshot 2025-03-16 at 6 36 18 PM" src="https://github.com/user-attachments/assets/08903abe-1d06-4f2b-9685-c6c0f2fa0f21" />
</p>
<br/>
<p>
  Next, we will create our first user. We will name her Jane Doe. To do this, go to the admins OU that was made, right click and hit "New". It will open a window where you can add credentials. Create a username and password. Your user should be created. However, we need to add Jane to the "Domain Admins" Security Group to make Jane an Admin. Right click on Jane Doe, go to Properties, click on Member of, click Add, type Domain Users, and apply and save. Now log out and log in as Jane Doe. 
</p>
<p>
  <img width="750" alt="Screenshot 2025-03-16 at 6 37 07 PM" src="https://github.com/user-attachments/assets/7caf0255-1028-4aad-b54b-94aac99ace94" />
  <img width="750" alt="Screenshot 2025-03-16 at 6 37 07 PM" src="https://github.com/user-attachments/assets/6fa5dc46-01a7-48ac-9fc5-b7659a7d8721" />
  <img width="378" alt="Screenshot 2025-03-16 at 6 38 03 PM" src="https://github.com/user-attachments/assets/fdc55686-2c49-4b69-9cc6-5651b73e0a06" />
  <img width="367" alt="Screenshot 2025-03-16 at 6 38 48 PM" src="https://github.com/user-attachments/assets/d5459987-a763-449b-a47b-42091c16e0a1" />
  <img width="398" alt="Screenshot 2025-03-16 at 6 38 57 PM" src="https://github.com/user-attachments/assets/2cbcf11f-2121-444a-b446-58c77813aae6" />
<img width="264" alt="Screenshot 2025-03-16 at 6 39 14 PM" src="https://github.com/user-attachments/assets/79e93bf8-725c-406c-9790-c49e67e6bd17" />
</p>
<br/>
<p>
 Next, we need to join client-1 to the domain. To do this, go to client-1. Right Click on the Start menu. Go to System. Then, scroll down to "rename this PC" click on "Change" and click on "domain" button and type in "mydomain.com" This should join the two together. Since we already configured the DNS settings earlier, we have less to do now. Be sure to go into DC-1, add an OU and name it "_Clients" and move the "client-1" from "Computers" to the new "Clients folder you made.  
</p>
<p>
  <img width="214" alt="Screenshot 2025-03-16 at 7 01 44 PM" src="https://github.com/user-attachments/assets/17d7aebe-4038-402c-8477-655b41fc96e9" />
  <img width="306" alt="Screenshot 2025-03-16 at 7 03 32 PM" src="https://github.com/user-attachments/assets/c144f6fb-3dcf-46d1-937f-9ee4ef6e3d0c" />
<img width="298" alt="Screenshot 2025-03-16 at 7 05 25 PM" src="https://github.com/user-attachments/assets/7ff4dd53-dd35-41e4-b719-6bad52bce79c" />
<img width="408" alt="Screenshot 2025-03-16 at 7 05 36 PM" src="https://github.com/user-attachments/assets/d1389098-a8d7-44d6-a4e8-89403a3e42cb" />
<img width="414" alt="Screenshot 2025-03-16 at 7 06 29 PM" src="https://github.com/user-attachments/assets/2cd8b4dc-14b1-4c94-bcae-b8f159fa49c8" />
</p>
<br/>
<p>
  Next, we need to setup Remote Desktop for non-admin users on client-1. Login in to client-1 as Jane_admin. Open System Properties by right clicking the start menu. Click on "Remote Desktop". From here, allow "domain users" access to remote desktop. You can now log into Client-1 as a normal, non-administrative user now
</p>
<p>
 <img width="225" alt="Screenshot 2025-03-16 at 7 35 51 PM" src="https://github.com/user-attachments/assets/27e2a9bb-a760-4821-8852-7f7f823f7ae9" />
<img width="338" alt="Screenshot 2025-03-16 at 7 36 05 PM" src="https://github.com/user-attachments/assets/a1b5d5bc-753d-4549-b469-379e36ddf9ad" />
<img width="456" alt="Screenshot 2025-03-16 at 7 37 02 PM" src="https://github.com/user-attachments/assets/f1e298e4-7e2e-48c8-ba59-7e0cf91a387f" />
</p>
<br/>
<p>
  Next, we will create a bunch of additional users and log in to client one as one of the users. Log in to jane_admin. Open Powershell_ise as an admin. Create a new file, and post in a your script. Run the script and observe the users being created. When that finishes, open ADUC and observe the created accounts in the OU "_EMPLOYEES". Then, attempt to log in to client-1 with the account. 
</p>
<p>
  <img width="1" alt="Screenshot 2025-03-16 at 7 46 45 PM" src="https://github.com/user-attachments/assets/6b7b49c6-4ec4-411c-ad60-5295a26ea30a" />
<img width="957" alt="Screenshot 2025-03-16 at 7 47 45 PM" src="https://github.com/user-attachments/assets/3861bb78-088d-423d-9f9c-16109549b0f1" />
<img width="1284" alt="Screenshot 2025-03-16 at 7 50 25 PM" src="https://github.com/user-attachments/assets/9a42c25d-23f4-46d8-97bc-0b4b40f97dfa" />
</p>
<br/>
<p>
  Now that we have created our users. We can begin observing how we can use Active Directory in a real-world setting. Here we will deal with Account Lockouts. Log in to dc-1. Randomly pick a user that you generated. Attempt to log in with it 10 times with a bad password. We will then configure a Group Policy to lock out after 5 attempts. Once it locks out, go into your dc-1 and unlock the account in ADUC. You will see the last screenshot in the user's account. 
</p>
<p>
  <img width="754" alt="Screenshot 2025-03-16 at 8 10 14 PM" src="https://github.com/user-attachments/assets/e7e7e73f-2430-4e24-868e-75a8dc51a413" />
  <img width="397" alt="Screenshot 2025-03-16 at 8 10 25 PM" src="https://github.com/user-attachments/assets/097f5cfb-ed2e-4230-8fcf-834267602dcc" />
  <img width="250" alt="Screenshot 2025-03-16 at 8 11 55 PM" src="https://github.com/user-attachments/assets/fc40eebc-b396-4cfb-b608-d13e16b408e9" />
<img width="783" alt="Screenshot 2025-03-16 at 8 13 52 PM" src="https://github.com/user-attachments/assets/12750884-20e1-49e9-a471-a69f0de85e55" />
<img width="372" alt="Screenshot 2025-03-16 at 8 22 40 PM" src="https://github.com/user-attachments/assets/d6216d8a-ad58-4b16-a4a3-a5323a0122c0" />
</p>
<br/>
<p>
  Lastly, we will practice enabling and disabling accounts. In ADUC in dc-1. you can right click on a user's account, scroll down and click "disable account". You can do the same to enable the account.
</p>
<p>
  <img width="516" alt="Screenshot 2025-03-16 at 8 33 08 PM" src="https://github.com/user-attachments/assets/4fd88aca-0966-404b-a79c-8977c207e553" />
</p>
<br/>
<p>Congrats! We have finished the lab! :)</p>

