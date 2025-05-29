<p align="center">
<img src="https://i.imgur.com/AeiqMDZ.png" alt="Traffic Examination"/>
</p>

<h1>Network-File-Shares-and-Permissions</h1>
In this walkthrough, we will set up shared network files & permissions. We will create folders in the DC-1 VM and share them on the network. Certain files will have certain permissions. Only designated people will be able to view certain files. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Domain Controller/Client Machine)
- Remote Desktop
- Shared Network Files

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Walkthrough Steps</h2>

</p>
<p>
Connect/log into DC-1 as your domain admin account (mydomain.com\jane_admin).
Connect/log into Client-1 as a normal user (mydomain\<someuser>). On DC-1, go to the C:/ drive on the DC-1 machine and create 4 folders: "read-access", "read/write-access", "no-access", and "accounting".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/f4325414-4a37-4950-9e4d-8460e4d9da10" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Set the following permissions (share the folder)
Folder: “read-access”, Group: “Domain Users”, Permission: “Read”
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write”
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write”
(Skip accounting for now)

</p>
<br />

<p> 

<img src="https://github.com/user-attachments/assets/65444e72-cfdd-4155-886b-2d5455891094" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://github.com/user-attachments/assets/4b6e1c58-7713-4d7e-ae78-33c5c2ba4638" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>

</p>
<br />
<p>Attempt to access file shares as a normal user
On Client-1, navigate to the shared folder (start, run, \\dc-1)
Try to access the folders you just created. Which folders can you access? Which folders can you create stuff in? Does it make sense?
  
<img src="https://github.com/user-attachments/assets/3e69e3ee-84e1-440f-aa2e-d1ea8f14843d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<img src="https://github.com/user-attachments/assets/5e97cf21-859d-45e8-9f6a-97d73634f94b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/9e7f0586-e8ba-4a28-90ec-ea5f6e144821" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://github.com/user-attachments/assets/e8c54afe-9507-4f0a-b0ae-141f39c56d71" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p>
</p>
Go back to DC-1, in Active Directory, create a security group called “ACCOUNTANTS”
On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”.

</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/d91488f6-8531-4059-84a9-897fdce157b7" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
On Client-1, as  <someuser>, try to access the accountants folder. It should fail.

</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/f27b6cba-455a-4e85-836e-ced988fd823b" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
Log out of Client-1 as  <someuser>
On DC-1, make <someuser> a member of the “ACCOUNTANTS”  Security Group


</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/3e1390c1-8e8a-4d38-8fa7-806e3d08292d" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
</p>
Sign back into Client-1 as <someuser> and try to access the “accounting” share in \\DC-1\ - Does it work now?


</p>
<br />
<p>
<img src="https://github.com/user-attachments/assets/eedfccb0-6472-479c-85ad-1736d5259745" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>


