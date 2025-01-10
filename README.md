
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
  <img height="80%" width="80%" alt="Screenshot 2025-01-10 at 11 09 35 AM" src="https://github.com/user-attachments/assets/467fabbc-f917-4879-89b2-a9938178dc86" />

</p>
<p>
Create two VMs in Azure ensuring that they are in the SAME VIRTUAL NETWORK and SUBNET MASK (see networking tab when creating VM). </p>
<p>Name one DC-1 (Domain Controller) and set the image to Windows Server 2022.</p>
<p>Name second VM Client-1 and set the image to Windows 10.</p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 14 11 AM" src="https://github.com/user-attachments/assets/b2d7a15b-576c-486b-829f-b449b141273f" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 14 26 AM" src="https://github.com/user-attachments/assets/580bf4f9-9c8e-4bb9-a3fa-d71325a23fa3" />
    </td>
  </tr>
</table>
<p>
Click into DC-1 -> Network Settings -> Network Interface. We will configure DC-1 to have a static IP address.</p>
<p>Navigate to ipconfig1 -> select Static </p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 23 51 AM" src="https://github.com/user-attachments/assets/f81418b6-41f2-4fd0-9ff0-042e55bf1bf6" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 24 51 AM" src="https://github.com/user-attachments/assets/dd92ce13-731b-4197-b02c-34dc4d22797d" />
    </td>
  </tr>
</table>
<p>
Using DC-1's public IP address, remote desktop into DC-1. Navigate to the start menu -> run -> search for wf.msc</p>
<p>This will open up the firewall settings for DC-1. Go to Windows Defender Firewall Properties and turn off the firewall for each tab. Be sure to click apply when finished. </p>
<br />

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 34 17 AM" src="https://github.com/user-attachments/assets/53eb5cb6-d07c-4e10-87b9-89c814ac8fdc" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 35 19 AM" src="https://github.com/user-attachments/assets/6f661ef1-26d3-4711-bfdd-71e5a051e6cf" />
    </td>
  </tr>
</table>
<p>Go to Client-1's Network Settings -> Network Interface -> DNS settings. Enter in DC-1's private IP address (this can be found in DC-1's network settings or overview tab). Be sure to click save. </p>

<p>
  <img height="80%" width="80%" alt="Screenshot 2025-01-10 at 11 41 49 AM" src="https://github.com/user-attachments/assets/1efc5abb-aba5-44df-bae8-ff4f9890ce68" />
</p>
Once the settings are saved navigate back to the virtual machines homepage and give Client-1 a restart by checking its box and clicking "Restart"
<p>When Client-1 has restarted, remote desktop into Client-1 using its public IP address.</p>
<br>

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 46 33 AM" src="https://github.com/user-attachments/assets/bd19e712-bedc-4b66-b022-30ee84c5c440" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 47 00 AM" src="https://github.com/user-attachments/assets/dc16543f-fad1-418e-85ed-c7b64b230496" />
    </td>
  </tr>
</table>
<P>Within Client-1 open up PowerShell and ping DC-1 to ensure that both VMs are on the same virtual network and that DC-1's firewall is disabled.</P>
<p>Next, type "ipconfig /all and look to make sure the DNS server of Client-1 is set to DC-1's private IP address.</p>

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 55 49 AM" src="https://github.com/user-attachments/assets/31d7050b-49bc-401a-8ac9-7c8302e1fd6b" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 12 00 15 PM" src="https://github.com/user-attachments/assets/7428a488-ab52-4818-af69-44d77e946222" />
    </td>
  </tr>
</table>
<p>Log in to DC-1 and in server manager click "Add role and features". From here add a feature to install Active Directory Domain Services. Click through next to install AD DS. </p>
<p>Once AD DS is installed, go to the top right flag in the server manager and promote the server to become a domain controller. Add a new forest named mydomain.com and continue through the setup wizard. (Be sure to uncheck DNS delegation as you progress through the setup </p>
<p>Once the setup is finished, the VM will reboot.</p>

<p>
  <img height="50%" width="50%" alt="Screenshot 2025-01-10 at 12 13 39 PM" src="https://github.com/user-attachments/assets/da2a27f4-7efe-4751-b072-d49b9c586f9b" />
</p>
<p>Remote desktop back into DC-1 but this time with a domain specific user. Enter "mydomain.com\anakamura1" (mydomain.com\username)</p>
<p>This will log in as a specific user within the domain.</p>

<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 12 20 56 PM" src="https://github.com/user-attachments/assets/2cf2301e-9cbc-439b-b1f3-1d6a3d9da1e9" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 12 22 39 PM" src="https://github.com/user-attachments/assets/b0fc2b04-0071-45a0-9bdb-0d61de52d517" />
    </td>
  </tr>
</table>
<p>
Open Active Directory Users & Computers from within the start menu. By right clicking on mydomain, create a new Organizational Unit (OU).
</p>
<p>Create one named _EMPLOYEES and create another named _ADMINS</p>
<p> Once both OUs are created, within _ADMINS right click to create a new user. We will name this user Jane Admin and configure her login credentials.</p>
<p>Something like jane.admin and a password we can remember will suffice.</p>
<br>
<p>
  <img height="80%"  width="80%" alt="Screenshot 2025-01-10 at 12 24 26 PM" src="https://github.com/user-attachments/assets/d7ab9ddf-10b3-4c57-b6ee-cf5af9e25c58" />
</p>
<p>Once she is created, right click on her to access Properties -> Members of, and add her to "Domain Admins". Be sure to click "Check Names" and apply when finished.</p>
<p>Log out of DC-1 and log back in as “mydomain.com\jane.admin”</p>
 <p>We can use jane.admin as the admin account from now on
</p>
<table>
  <tr>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 12 48 48 PM" src="https://github.com/user-attachments/assets/bdbe01e6-be63-4e4d-b1f9-43fb08c579f7" />
    </td>
    <td>
      <img width="1000" alt="Screenshot 2025-01-10 at 12 49 59 PM" src="https://github.com/user-attachments/assets/95d36f94-6435-48dd-9539-aaaf8ef2ced8" />
    </td>
  </tr>
</table>
<p>Login to Client-1 as the original local admin (anakamura1)</p>
<p>From the start menu -> System -> Rename this PC Advanced -> Change, and enter mydomain.com</p>
<p>This will prompt a login screen where we can login as mydomain.com\jane.admin and join Client-1 to the domain controller DC-1</p>
<br>
<p>
  <img height="70%" width="70%" alt="Screenshot 2025-01-10 at 12 51 14 PM" src="https://github.com/user-attachments/assets/879e5f17-fff9-49c3-a64e-ff894bae6e4c" />

</p>
<p>We can verify the join was successful by going back into DC-1 and Active Directory Users and Computers (ADUS) and finding Client-1 within the Computer tab.</p>
<p>Create a new OU named _CLIENTS and drag Client-1 into it.</p>
<br>

<p><img height="70%" width="70%" alt="Screenshot 2025-01-10 at 1 57 16 PM" src="https://github.com/user-attachments/assets/fb4e131a-3403-4312-8de2-c888ccba6edc" />
</p>
<p>Log into Client-1 as Jane.Admin -> System -> Remote Desktop -> Select users that can remotely access this PC -> Add -> Domain Users -> Check names -> OK</p>
<p>This will allow any user under the Domain Users group in the domain controller to be able to log into Client-1. We will create users in the User Creation lab. </p>
<p><img height="70%" width="70%" alt="Screenshot 2025-01-10 at 2 04 29 PM" src="https://github.com/user-attachments/assets/a82987f7-3213-46ec-854c-c7fcfe1bdfcf" />
</p>

Within DC-1 as Jane.Admin, open PowerShell ISE as ADMINISTRATOR and paste the following [script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)

<p>Be sure to edit the password you want the users to have at the top of the script text.</p>

<table>
  <tr>
    <td>
      <img width="800" alt="Screenshot 2025-01-10 at 2 06 42 PM" src="https://github.com/user-attachments/assets/efe9998e-9049-4264-ac02-4e3973800ad3" />
    </td>
    <td>
      <img width="436" alt="Screenshot 2025-01-10 at 2 08 30 PM" src="https://github.com/user-attachments/assets/c15e853d-0426-47f8-bc40-2104ded6c39c" />
    </td>
  </tr>
</table>
<p>Check within ADUC and under _EMPLOYEES to see all the created users. Select any user and log into Client-1 to test access</p>
<p>All the created users should have access because we gave domain users access to remote desktop in Client-1</p>
