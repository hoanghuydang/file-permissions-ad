<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>File Permissions and Security Groups in  Azure Active Directory</h1>
In this tutorial, we observe file permissions from from Client-1 and DC-1 attempting to access as normal users and then allow them to have access to specific files. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows Server 2022

<h2>High-Level Steps</h2>

- Create some sample file shares with various permissions
- Attempt to access file shares as a normal user
- Create an "Accountants" Security Group, assign permissions, and test access


<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/JAlZ4HN.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/5qGEw01.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/XXap3QV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/30CaAbb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/9o9gevq.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/8hxh1Bw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>

</h2>STEP 1: CREATE SOME SAMPLE FILE SHARES WITH VARIOUS PERMISSIONS</h2>

  - Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin)
  - Connect/log into Client-1 as a normal user (mydomain\buju.mabe)
  - On DC-1, on the C:\ drive, create 4 folders: “read-access”, “write-access”, “no-access”, “accounting”
  - Set the following permissions (share the folder) for the “Domain Users” group:
  - Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
  - Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
  - Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
  - (Skip accounting for now)
</p>
<br />

<p>
<img src="https://i.imgur.com/BMw00wL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</h2>STEP 2: ATTEMPT TO ACCESS FILE SHARES AS A NORMAL USER</h2>

  - On Client-1, navigate to the shared folder (start, run, \\dc-1)
  - Try to access the folders you just created. Settings should make sense according to each configuration.
</p>
<br />

<p>
<img src="https://i.imgur.com/uX9brGA.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/H7Ub2XV.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/mtFmVcC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  <p>
<img src="https://i.imgur.com/Qkz8q5D.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</h2>STEP 3: CREATE AN "ACCOUNTANTS" SECURITY GROUP, ASSIGN PERMISSIONS, AND TEST ACCESS</h2>

  - Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
  - On the “accounting” folder you created earlier, set the following permissions:
  - Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write
  - On Client-1, as  buju.mabe, try to access the accountants folder. It should fail.
  - Log out of Client-1 as buju.mabe
  - On DC-1, make buju.mabe a member of the “ACCOUNTANTS”  Security Group
  - Sign back into Client-1 as buju.mabe and try to access the “accounting” share in \\DC-1\ 

</p>
<br />

