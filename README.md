<p align="center">

  ![image](https://github.com/user-attachments/assets/0693c1dd-f224-4ef3-aaee-9197485cf973)

</p>


<h1>Preparing Active Directory Infrastructure in Azure</h1>
This guide walks through setting up an Active Directory environment in Azure. We'll use this foundational setup later to deploy and configure AD for upcoming projects.<br />


<h2>Prerequisites</h2>

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

![1](https://github.com/user-attachments/assets/fec1d9cc-f229-408a-af4c-c58c602da480)

</p>
<p>
- We start by making a Resource Group and creating two Virtual Machines. Make sure both VM's are in the same Virtual Network and Region.


  + *If you are new to creating Resource Groups and Virtual Machines in Azure, refer to the prerequisites outlined above for step-by-step guidance*.
</p>
<p>
- When deploying the first virtual machine, ensure it is named DC-1 to designate its role as the Domain Controller. Configure the VM using the Windows Server 2022 image and allocate a minimum of 2 vCPUs to meet the system requirements for optimal performance
</p>
- Name the second VM "Client-1" but make sure the image is set to Windows 10 and 2vcpus, just like DC-1.
<p>
<br />
<p>

![2](https://github.com/user-attachments/assets/ea4f06d6-4bcc-4a34-afa7-696deb2b9ff9)

</p>
<p>
- Let's configure DC-1's network settings. Go to the VM in Azure, then head to Network settings → Network interface/IP configuration.
</p>
<br />

<p>

![3](https://github.com/user-attachments/assets/f4f4a611-9efb-4063-a172-4db90059d6b3)

</p>
<p>
- Make sure you're in IP configurations, and click on "ipconfig1". Change Dynamic to Static under Private IP address settings. (We don't want our IP to change)
</p>
- Now click Save.
<br />

<p>

![5](https://github.com/user-attachments/assets/cbda2330-f2dd-4440-9e21-10f9fd456289)

</p>
<p>
- To access the Domain Controller, establish a Remote Desktop connection to DC-1 using its public IP address (refer to the network diagram provided in Figure 1 for this information).
</p>
- Now, click the start menu and type in run, open it. Type wf.msc and click OK.
</p>
<br />

<p>

![6](https://github.com/user-attachments/assets/36df4e12-d450-466f-a4f1-8bafb1d4fe23)
![7](https://github.com/user-attachments/assets/810946c4-40f4-4f99-8c9e-11c75b07106a)

</p>
<p>
- This brings you to "Windows Defender Firewall with Advanced Security". Select Windows Defender firewall Properties. 
</p>
- Turn Firewall state from on(recommended) to off for Domain Profile, Private Profile, and Public Profile. Leave the last tab as is.
</p>
- Click Apply and then OK.
</p>
<br />


<p>

![8](https://github.com/user-attachments/assets/12e1b5cd-88ad-4df9-bde5-dedd167306ce)
![9](https://github.com/user-attachments/assets/443063a6-5678-40e8-851a-d2a11052238f)

</p>
<p>
- Navigate back to your VM in Azure. Note our Private IP for DC-1. We will need it.
</p>
- Now go to Client-1 > Networking Settings > Networking interface/IP confirguration.
</p>
<br />


<p>

![10](https://github.com/user-attachments/assets/ff7d1f5f-561d-4074-81bb-a3af18cdee5e)
![11](https://github.com/user-attachments/assets/bcad0de5-9ee8-4e46-a422-c5e0001756b9)

</p>
<p>
- In DNS Servers, click Custom because we want to paste the DC-1 Private IP Address.
</p>
- Doing this will allow us to join the Domain. Click Save.
</p>
- Now navigate yourself back to your Virtual Machines. For our DNS settings to become active, we need to restart Client-1. Check the Box for Client-1 and hit Restart, click yes.
</p>
<br />

<p>

![12](https://github.com/user-attachments/assets/5796eb6b-2113-4f20-b7b8-ad0aba15e28b)

</p>
<p>
-⏲️ Now we wait for Client-1 to restart. Once it restarts, grab your public IP addresses and log back into Client-1.
</p>
- Go to the Start Menu and type in Powershell, open up Powershell.
<br />

<p>

![13](https://github.com/user-attachments/assets/249999e6-a052-4e46-8bbc-1194f9b85afe)

</p>
<p>
- Now we type in ping 10.0.0.4 ( this is the DC-1 Private IP Address). We want to test the connection between Client-1 to DC-1 so that is the command. Hit Enter. 
</p>
- The ping results will display response times and packet loss statistics, allowing you to confirm proper network configuration between these systems
<br />

<p>

![14](https://github.com/user-attachments/assets/14a1fb33-c99a-4fa9-aee8-786ce77f95f7)

</p>
<p>
- The finish line is here. The output for the DNS settings should show DC-1’s private IP Address. In PowerShell, type in ipconfig /all and hit Enter.
</p>
- And there it is, it shows us the DC-1 Static IP Address. We did it, quick and harmless, right? 😎
<br />


<h2>Final Thoughts</h2>
</p>
- Are you loving Active Directory like I am? Completing this lab gave me a solid hands-on understanding of how to build an Active Directory environment in Azure, from spinning up the VMs to configuring the domain controller and testing connectivity. Are you ready to deploy and configure in AD? I am. Let's head to our next project!
<br/>
