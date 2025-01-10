
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
