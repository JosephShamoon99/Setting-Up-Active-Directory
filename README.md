<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

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
<img width="100%" height="100%" alt="screenshot 5" src="https://github.com/user-attachments/assets/1a28f0c1-2395-4e79-8821-5d3cadd50776"/>
</p>
<p>
Once we have our domain controller created, we can go ahead and create a client VM to connect to our domain controller. Like always, make sure it is in the same resource group, virtual network and region as everything else. 
</p>
<br /> 

<p>
<img width="100%" height="100%" alt="screenshot 3" src="https://github.com/user-attachments/assets/1a28f0c1-2395-4e79-8821-5d3cadd50776"/>
</p>
<p>
Once we have our domain controller created, we can go ahead and create a client VM to connect to our domain controller. Like always, make sure it is in the same resource group, virtual network and region as everything else. 
</p>
<br /> 

