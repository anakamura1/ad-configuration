
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
    <Td>
      <img width="1000" alt="Screenshot 2025-01-10 at 11 14 26 AM" src="https://github.com/user-attachments/assets/580bf4f9-9c8e-4bb9-a3fa-d71325a23fa3" />

    </Td>
  </tr>
</table>
<p>
Click into DC-1 -> Network Settings -> Network Interface. We will configure DC-1 to have a static IP address.</p>
<p>Navigate to ipconfig1 -> select Static </p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
