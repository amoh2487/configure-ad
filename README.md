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

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
</p>
<p>

  ![image](https://github.com/amoh2487/configure-ad/assets/148664179/c074ff12-acc3-4f4c-a40e-0770b0325335)
  

As always, whenever we want to create a new project for IT, we have to create virtual machines from Azure Studios in order to do the work correctly and Active Directory is no different. Here, we created one virtual machine for the domain controller in order to transfer our data from place to place. Also, for this virtual machine, we use the Windows Server 2022 for the image to differentiate it from our other virtual machine. We also need to create a username and password for both of the virtual machines in order to connect to Remote Desktop Connection later on. Once the domain controller virtual machine has been installed successfully, we then create another virtual machine for Customer-1 following the same steps except that for this virtual machine, we use Windows 10 Pro. The reason why we create another virtual machine is that because we will use the domain controller virtual machines databses and sets of services to connect to Customer-1 so that Customer-1 connects with the network resources they need to get their work done. Lastly, we want to make sure that both of the virtual machines have the same virtual network/subnet in order to not have any issues further down the line when we try to connect the two virtual machines together.
</p>
<br />

<p>
</p>
<p>
  
![image](https://github.com/amoh2487/configure-ad/assets/148664179/5629cb31-0fbc-4340-91e3-d0a15637a873)

  
After the Customer-1 virtual machine is ready to go, we open Remote Desktop Connection and login with our credentials we made for the virtual machine and open the remote desktop by copying and pasting whatever the public IP address is for the Customer-1 virtual machine. Once we are logged in, we open the command line and type "ping -t" followed by copying pasting the private IP address for the domain controller virtual machine.
</p>
<br />

<p>
</p>
<p>
  
![image](https://github.com/amoh2487/configure-ad/assets/148664179/a28f4f0f-324e-458c-8c81-f94c94d9da7a)

  
Once the previous step of pinging the Private Ip address for the domain controller has been done, we then go back and open Remote Desktop again and this time we are logging in with the domain controller virtual machine by typing our username and password and also typing in the public Ip address to log in. Once are logged in inside Remote Desktop Connection, we then go to "Windown Defender Firewall with Advanced Security". Once we do that, we then click "Inbound Rules" and under "Protocols", we then find ICMPv4 and right click on two of them and click the "Enable Rule" option. Once we do all of this, there will be connectivity happening between the client and domain controller virtual machine.
</p>
<br />

<p>
</p>
<p>

![image](https://github.com/amoh2487/configure-ad/assets/148664179/81e8d2c5-aa46-4300-9ca3-e239c4d0f6e5)


Once the previous step is done, we go back to the domain controller Remote Desktop and open Server Manager. Once we are there, we click under "Add Roles and features" and then we click next on all the steps so that they are in their default features, until we get to the "Server Roles" page. Once we are there, we check the box that says "Active Directory Domain Services" and click next until the "Results" page and click the "Install" button. The reason for why installed active directory domain services in the first place is because it lets us set up our domain such as our domain name in order to manage the users and computers and allow system administrators to organize the data into logical hierarchies.
</p>
<br />

<p>
</p>
<p>

![image](https://github.com/amoh2487/configure-ad/assets/148664179/40e61928-8835-4504-aa30-11d97b1022f9)



After the Active Directory Domain Services software has been installed, we then go ahead and create our domain such our root domain name, setup pur password for the new domain, and we click next on the pages to be on their default mode until we get to the results page. Our device then will automatically restart which will take a couple of minutes. Once our device has restarted successfully and everything looks good, we then login with our domain credentials, and at this point, our domain has been sucescessfully created which in return will allow us to create other materials such as organizational units and so on.
</p>
</p>

<p>
</p>
<p>

![image](https://github.com/amoh2487/configure-ad/assets/148664179/79549ff9-fa22-4c33-9ea5-b14f92f307b2)


Once the previous step is done and successfull, we then login to Customer-1 virtual machine, but this time we login with the credentials we had created for our domain name user before. Once that is completed, we then go to the start button and search "PowerShell ISE" and be right click on the "Run as Administrator" option. Once that is done, we go and look for the script that we created before the start of the Active Directory Project and copy and paste it into PowerShell ISE. We know that our script has been successfull here because it is creating 10,000 accounts like we said in the script, and I say this because if our script wasn't successfull, it would say in red, "New-Aduser : Access is denied". This means that there was something wrong when we created the script in the firstplace.
</p>
</p>

<p>
</p>
<p>

![image](https://github.com/amoh2487/configure-ad/assets/148664179/46d0ee21-5ad2-4129-9804-afd9ffdda89b)


Once we know for sure that the last step has been done successfully, then we should next be able to see our accounts being created from the script in the form of a green color. This means that we should be able to see all of the 10,000 accounts being created that we made from the script and the accounts don't follow a specific name since we didn't make actual names for each account that is being created such as "James" or "Connor" but instead made raondom names that are weird like "Neren" for instance.
</p>
</p>

<p>
</p>
<p>

![image](https://github.com/amoh2487/configure-ad/assets/148664179/834b6a57-6a3f-4658-91f5-62ef1f680a44)


After all our 10,000 accounts have been created on Powershell ISE, if we go back to the "Employees" folder that we made earlier, all of our employees should be there as users so they have access to our Active Directory. Also, if we click on any user, we should be able to login to our Client 1 virtual machine by closing Remore Desktop Connection and opening it again, but this time we will login with one of our user's credentials such as "Kavo.Wuk" for the username and password.
