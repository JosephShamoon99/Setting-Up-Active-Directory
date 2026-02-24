<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Setting Up Active Directory (Azure)</h1>
Active Directory is a service that allows you to manage thoundas of users, computers and resources on a Windows Domain Network from one central loaction. 
This is a very important tool for IT professionals to know how to use. In this tutorial, I will show you how to set up an Active Directory Domain in Mircosoft Azure.
<br /> 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 11

<h2>High-Level Deployment and Configuration Steps</h2>

- Create a virtual machine to act as our domain controller with Windows server 2022 
- Deploy Active Directory on the domain controller
- Create anohter virtual machine as a client to connect to the domain controller we created

<h2>Deployment and Configuration Steps</h2>

<p>
<img width="100%" height="100%"alt="screenshot 1" src="https://github.com/user-attachments/assets/f5caae3e-f2f6-4225-8311-7f4632c5e09d"/>
</p>
<p>
The first thing that we will have to do is create a resource group and create a virtual network inside of it. It is important for all the resources we create to be placed in the same region.
</p>
<br />

<p>
<img width="100%" height="100%" alt="screenshot 2" src="https://github.com/user-attachments/assets/8a9d14e4-221a-432d-881e-4baa25bb31c8"/>
</p>
<p>
Next, we will need a domain controller. The domain controller is where we will actually deploy 
Active Directory. Other computers will connect to this to join our domain. To create a domain controller we will need to create a virtual machine for it. We will need to place the virtual machine in the resource group that we created and place it on the network we created. We also have to use windows server 2022 for its image. 
</p>
<br />

<p>
<img width="100%" height="100%" alt="screenshot 3" src="https://github.com/user-attachments/assets/1a28f0c1-2395-4e79-8821-5d3cadd50776"/>
</p>
<p>
Once we have our domain controller created, we can go ahead and create a client VM to connect to our domain controller. Like always, make sure it is in the same resource group, virtual network and region as everything else. 
</p>
<br /> 

<p>
<img width="100%" height="100%" alt="screenshot 4" src="https://github.com/user-attachments/assets/709bcfde-b78b-485b-9983-9050c3bf350b"/>
</p>
<p>
Next, we will have to make the private IP address of our domain controller static. 
This is because our client will use the domain controller as its DNS server as well. To change the IP address of the domain controller to static, click on the domain controller VM > networking > networking settings > click on the link to the VM's NIC settings > click on the VM's IP > select static and save. 
</p>
<br /> 

<p>
<img width="401" height="456" alt="snapshot 5" src="https://github.com/user-attachments/assets/b8473e71-a0b8-4985-841a-95f73fb262f8" />
</p>
<p>
For testing purposes, we will need to disable the firewall on the domain controller VM. To disable the firewall, log in to the domain controller VM using RDP. Once you are logged in, right click the windows icon > select start >  type wf.msc > windows firewall defender properties > turn all firewall states to off on all tabs > select okay.  
</p>
<br /> 

<p>
<img width="100%" height="100%" alt="snapshot 6" src="https://github.com/user-attachments/assets/3574ae1e-b3e1-4a84-bb19-69917d902d71"/>
</p>
<p>
Next, We will have to set our client VM's DNS server to our domain controller's private IP 
address. First, get the private IP address of the domain controller. Then click on the client  
VM > networking > networking settings > click on the link to the VM's NIC settings > DNS servers > select custom > enter the domain controllers private IP address and click save. 
</p>
<br />  

<p>
<img width="100%" height="100%" alt="snapshot 7" src="https://github.com/user-attachments/assets/1585dbd8-244d-4787-8fbd-aa52ce735bb3"/>
</p>
<p>
Next, we will have to make sure the client can connect to the domain controller. Restart the client then login to it. Open up powershell and ping the private IP address of the domain controller 
</p>
<br />  

<p>
<img width="1106" height="626" alt="Snapshot 8" src="https://github.com/user-attachments/assets/412281dc-0b3d-4bb4-abb9-befbd19280a8" />
</p>
<p>
Once we confirm we are able to connect to the domain controller run ipconfig /all to confirm 
The DNS server is the private IP address of the domain controller. 
</p>
<br />  

<p>
<img width="1425" height="751" alt="Snapshot 9" src="https://github.com/user-attachments/assets/c731b5ec-eadf-40d8-8e9c-668f6c8c0cd5" />
</p>
<p>
Now we will have to deploy Active Directory on our domain controller. Go to the virtual machine with Windows Server 2022 and go to the server manager. 
</p>
<br />  

<p>
<img width="789" height="560" alt="Snapshot 10" src="https://github.com/user-attachments/assets/c6c60911-101b-4bf8-8a3b-56867d0a7dda" />
</p>
<p>
Click "add roles and features". Click next on everything until you get to "server roles" and select 
Active Directory Domain Services  
</p>
<br /> 

<p>
<img width="786" height="561" alt="Snapshot 11" src="https://github.com/user-attachments/assets/253fdd35-9758-4899-b327-a266c472b8fd" />
</p>
<p>
Continue to click next on everything until Active directory is installed 
</p>
<br />  

<p>
<img width="1513" height="800" alt="Snapshot 12" src="https://github.com/user-attachments/assets/17d2e392-d666-4711-b8e3-2254b3972fc5" />
</p>
<p>
Now that we have Active Directory installed on our virtual machine, now we must promote 
the virtual machine to an actual domain controller. Go to the server manager and click on 
the flag and then click "promote this server to domain controller" 
</p>
<br />  

<p>
<img width="1430" height="755" alt="Snapshot 13" src="https://github.com/user-attachments/assets/078f7bea-d068-4f37-8a8b-3fb06fd12567" />
</p>
<p>
Select "add new forest" and name this domain controller, "mydomain.com". You can leave everything else at default settings and click install. This will restart our domain controller. 
</p>
<br />  

<p>
<img width="747" height="679" alt="Snapshot 14" src="https://github.com/user-attachments/assets/06e46f7e-75bc-46a2-b9e5-b0a105148717" />
</p>
<p>
When we log back in to our domain controller, we have to specify the domain we want to login to 
and the account within that domain. Our domain name is mydomain.com, so we will login as such "mydomain.com\labuser". It is important to use "\" instead of "/". 
</p>
<br />  

<p>
<img width="747" height="679" alt="Snapshot 15" src="https://github.com/user-attachments/assets/7a7dd114-0062-4de0-b99e-ef64d91df895" />
</p>
<p>
We will now create a domain admin for our domain. We will allow this account to run administrative  task 
on our domain. This is a huge deal, as an admin can effect hundreds of computers on a domain  
To do this we will first need to create an organizational unit for employees and admins. Think of OU's as a folder that holds data in our domain. Go to the Windows start menu > "Windows administrative tools" and  select "Active Directory Users and Computers" 
</p>
<br />  

<p>
<img width="774" height="655" alt="Snapshot 16" src="https://github.com/user-attachments/assets/591d170e-c675-4f2a-b134-218b182c9d85" /> 
<img width="777" height="649" alt="Snapshot 17" src="https://github.com/user-attachments/assets/a0b7d390-b54a-475e-a762-46074e8d9cf0" />
</p>
<p>
Right click on your domain > new > Organizational unit. Create an OU named _EMPLOYEES. Create another OU called _ADMINS  
</p>
<br />  

<p>
<img width="790" height="659" alt="Snapshot 18" src="https://github.com/user-attachments/assets/ed1502d9-7a09-4d22-befa-9c610705b91f" /> 
<img width="774" height="658" alt="Snapshot 19" src="https://github.com/user-attachments/assets/bc47fbdd-aa07-4170-95a2-5f63b9148688" />
<img width="765" height="635" alt="Snapshot 20" src="https://github.com/user-attachments/assets/58913c33-1760-44b1-9469-cd9a546fdd70" />
<img width="780" height="648" alt="Snapshot 21" src="https://github.com/user-attachments/assets/7b945c2c-decc-47e5-a8e2-caebf2715dba" />
</p>
<p>
We can now create our admin account in the _ADMINS OU. Right click _ADMINS > new > user. 
Feel out the info. Our admins name will be Jane Doe. At the end you see Jane Doe in the Admin OU. 
</p>
<br />  

<p> 
<img width="774" height="646" alt="Snapshot 22" src="https://github.com/user-attachments/assets/697e3fff-8fb3-4aa5-ab91-2529a056d31a" /> 
<img width="429" height="564" alt="Snapshot 23" src="https://github.com/user-attachments/assets/d4e814ba-bd9f-4a5c-a1a7-a72e71a29175" /> 
<img width="484" height="577" alt="Snapshot 24" src="https://github.com/user-attachments/assets/803bc292-064d-49fa-ac76-7235523681a4" />
<img width="424" height="577" alt="Snapshot 25" src="https://github.com/user-attachments/assets/432dc400-d8a2-492e-bccb-33e483c808fa" />
</p>
<p>
Just because we put jane doe in the _ADMINS OU, doesn't mean she has admin permissions. We will have to add her to the built in domain admin group for her to have admin permissions. To do that, we will right click on her account and select properties. Click the member of the tab and click add. From there we will type in the domain admins group and add her to it. Jane Doe is now an admin for our domain. 
</p>
<br />  

<p> 
<img width="776" height="643" alt="Snapshot 26" src="https://github.com/user-attachments/assets/015359ad-484f-4f66-a376-fbf580de4595" /> 
</p>
<p>
We will use Jane Doe to login back in. Jane Doe does not yet have permission to sign into the Domain Controller remotely yet. This is how we'll fix that. 
</p>
<br />  

<p> 
<img width="776" height="643" alt="Snapshot 27" src="https://github.com/user-attachments/assets/eee84ce0-c258-414b-8a59-806bea1301fc" /> 
<img width="779" height="634" alt="Snapshot 28" src="https://github.com/user-attachments/assets/c0b0d8fe-983b-40f0-a2ef-9ff6a3d6f046" /> 
<img width="786" height="655" alt="Snapshot 29" src="https://github.com/user-attachments/assets/c4caa52d-a07a-4adc-aafe-eb6112a83b99" /> 
<img width="713" height="796" alt="Snapshot 30" src="https://github.com/user-attachments/assets/bcc5eeb9-ca69-468e-baf0-44fd8b1e65a1" /> 
<img width="436" height="493" alt="Snapshot 31" src="https://github.com/user-attachments/assets/ab15ed48-ed3b-43a9-ac7e-f2159319681a" />
</p>
<p>
Log back in the domain controller with our default account of labuser. Open up Active Directory 
users and computers again. Click on the built in OU and click remote desktop users. Click Add > Advance >find now and scroll down until you see the Jane Doe account and click it. Click and apply and Ok. 
</p>
<br />  

<p> 
<img width="1213" height="951" alt="Snapshot 32" src="https://github.com/user-attachments/assets/cb65d340-570f-4b0d-97ef-0c01017c887d" />
</p>
<p>
Restart your domain controller and login with the Jane Doe account. We are login to the domain controller account remotely with the jane doe account  
</p>
<br />  

<p> 
<img width="1239" height="956" alt="Snapshot 33" src="https://github.com/user-attachments/assets/e9ffc185-2333-47ee-aa01-75ea617036c7" /> 
<img width="438" height="494" alt="Snapshot 34" src="https://github.com/user-attachments/assets/135dfc99-f738-44d6-80ae-40f3ac4e7cd1" />
<img width="426" height="482" alt="Snapshot 35" src="https://github.com/user-attachments/assets/e9d3fc4c-2f50-4509-87d2-28300ff38e68" />
<img width="498" height="400" alt="Snapshot 36" src="https://github.com/user-attachments/assets/ec88085a-d662-477e-be43-5794996311ef" />
<img width="350" height="212" alt="Snapshot 37" src="https://github.com/user-attachments/assets/b3304739-8bde-4a87-96d0-60c6f605a04c" />
</p>
<p>
The next thing we will do is login client 1 and join it to our domain. Right click the start menu and select system > rename this pc advance > computer change tab > change > select domain and type the name of our domain. Client 1 is able to find the domain because the domain controller is its DNS server. You connect client 1 to the domain using the jane doe account.  
You have to restart client 1 for the changes to apply  
</p>
<br />  

<p> 
<img width="772" height="553" alt="Snapshot 38" src="https://github.com/user-attachments/assets/6d06f482-8933-4f57-a4d5-5e74a53d3350" />
</p>
<p>
We will check on the domain controller if client 1 was added to active directory computers and 
users. Under the computer OU, you should see client 1. 
</p>
<br />  

<p> 
<img width="473" height="536" alt="Snapshot 39" src="https://github.com/user-attachments/assets/974bd0f8-a0ff-4873-8ed9-6d51f691b1e3" />
</p>
<p>
You can double click client 1 and see info about it 
</p>
<br />  

<p> 
<img width="766" height="542" alt="Snapshot 40" src="https://github.com/user-attachments/assets/df8bff44-1afa-4687-8af7-bdd01315d40f" />
</p>
<p>
For this lab, we create an OU called _CLINETS and place Client 1 in there.
</p>
<br />  

<p>
There you have it. We have our Active Direcorty Domain up and running on Azure. To see how we can actually manage accounts using this 
Active Diretory Domain, go to this tutorial next:  
  
[Active Directory: Managing Accounts With Active Directory](https://github.com/JosephShamoon99/Managing-Accounts-With-Active-Directory-)
</p>
<br />  








