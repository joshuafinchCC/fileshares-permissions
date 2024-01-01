<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/db2225be-e303-4d4e-98a7-ff3ee9cbdffd" height = 20% width = 40%/>
</p>

<h1 align = "center">Network Fileshare and Permissions Within Active Directory</h1>
File sharing and permissions is an essential in almost any business structure. This allows us to organize resources and make sure users have the appropriate permissions and access to files they need, while also preventing users from accessing/editing files they shouldn't. This guide demonstrates how file sharing and permissions work within an Active Directory domain. Here is a complete guide to <a href = "https://github.com/joshuafinchCC/Activedirectory-config">Active Directory Setup</a>.

<br />

<h2>Environments and Technologies Used</h2>
<ul>
  <li>Microsoft Azure (Virtual Machines/Compute)</li>
  <li>Remote Desktop</li>
  <li>Active Directory Domain Services</li>
</ul>

<br />

<h2>Operating Systems Used</h2>
<ul>
  <li>Windows Server 2022</li>
  <li>Windows 10 Pro (21H2)</li>
</ul>

<br />

<h2>Steps</h2>

<h3>Creating Sample Fileshares with Various Permissions</h3>

<p>
  <ul>
    <li>Log into <b>DC1</b>as an administrator account. Log into <b>Client1</b> as any newly created user (in this case myportfolio.com\employee)</li>
    <li>Within the Domain Controller VM, create the four folders below in the C:\ Drive and set the <b>Permissions</b> (right click ->Properties-> Share->Domain Users/Domain Admins->Add) in these folders as follows:</li>
    <ul>
      <li><b>read_access</b> - add the group Domain Users and set Permissions to Read</li>
      <li><b>write_access</b> - add the group Domain Users and set Permissions to Read/Write</li>
      <li><b>no_access</b> - add the group Domain Admins and set Permissions to Read/Write</li>
      <li><b>accounting</b> - skipped for now</li>
    
 <p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/8e38a3f2-884c-435d-84fe-79bb31781c29" height = 40% width = 80%/>
</p>

<br/>

<h3>Attempting to Access Fileshares</h3>

<p>
  <ul>
    <li>Now if we go to the Client VM and navigate to the shared folder through <b>File Explorer</b> and typing <b>\\dc1</b> we should see all the files we shared while connected to DC1</li>

<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/68afc6f0-640b-4e57-be9e-42ecec749d1f" height = 40% width = 60%/>
</p>
    
<li>Attempt to access all the folders through the Client VM; the only one that should be inaccessible right now based on our permissions is the <b>no_access</b> folder</li>
  
<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/a4be932d-5af0-4fd3-93d5-ed4c908e500b" height = 40% width = 60%/>
</p>
    
<br/>

<h3>Creating the "ACCOUNTANTS" Security Group</h3>

<p>
  <ul>
    <li>Head back to DC1, navigate to <b>Active Directory Users and Computers</b> and create a new <b>Organizational Unit (OU)</b>. name it "_SECURITY_GROUP"</li>
    <li>Inside the OU, create a <b>Group</b> and name it "ACCOUNTANTS"</li>

<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/82d7b8a9-9572-46eb-b48c-79c8a7c2b879" height = 40% width = 60%/>
</p>
   
<li>Locate the <b>accounting</b> folder created in C:\ Drive and add the ACCOUNTANTS group and set its permissions to Read/Write</li>

<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/c47942c1-dba6-4520-8c68-1f801a615c47" height = 460% width = 80%/>
</p>
    
  <li>Our employee logged in the Client VM should not have access to the accounting folder since they are not part of the ACCOUNTANTS group yet</li>
  <li>In the Domain Controller VM, go to the _SECURITYGROUP OU,  right click on the ACCOUNTANTS to open up <b>Properites</b>, go to the <b>Members</b> tab and add the user you created as a member of the ACCOUNTANTS group</li>

<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/9430ccbc-aad9-4d3a-8e93-b7dffdc2e3e8" height = 50% width = 60%/>
</p>
      
<li>Sign back into the Client VM with our employee now in the ACCOUNTANTS group and it should now have access to the accounting folder</li>
<p align="center">
<img src="https://github.com/joshuafinchCC/fileshares-permissions/assets/155266044/a4e49a72-c3a6-44a1-bac6-f021515c3720" height = 40% width = 70%/>
</p>
    

<br/>
