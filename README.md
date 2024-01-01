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
    <li>Go to the Client VM and navigate to the shared folder through <b>File Explorer</b> and typing <b>\\dc-1</b></li>
    <ul>
      <li><img src ="https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/3144b792-b6bf-4f27-b798-d2d8256308ff" width = 80% height = 80%/></li>
    </ul>
    <li>Attempt to access the folders through the Client VM; the only one that should be inaccessible by how the permissions are set should be <b>no_access</b></li>
    <ul>
      <li><img src ="https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/bbc34c03-d505-43b9-aadc-9b3b73db65be" width = 80% height = 80%/></li>
    </ul>
  </ul>
</p>
<p align="center">
<img src="" height = 20% width = 40%/>
</p>
    
<br/>

<h3>Creating the "ACCOUNTANTS" Security Group</h3>

<p>
  <ul>
    <li>Head back to the Domain Controller VM, go to the Server Manager Board and go to <b>Active Directory Users and Computers</b> and create a new <b>Organizational Unit (OU)</b> and name it "_SECURITY_GROUP."</li>
    <ul>
      <li><img src = "https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/af27e138-36de-44b0-85e9-a2b37088d496" width = 80% height = 80%/></li>
    </ul>
    <li>Inside the OU, create a <b>Group</b> and name it "ACCOUNTANTS"</li>
    <ul>
      <li><img src = "https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/12e4bde2-5aad-4981-b1b9-4fe847355b1c" width = 80% height = 80%/></li>
    </ul>
    <li>Locate the <b>accounting</b> folder created in C:\ Drive and add the ACCOUNTANTS group and set its permissions to Read/Write</li>
    <ul>
      <li><img src = "https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/567b094a-da96-49aa-ba2f-9f70d9c26844" width = 80% height = 80%/></li>
    </ul>
    <li>The user logged in the Client VM should not have access to the accounting folder since it's not part of the Group. Log off the Client VM and remember the username you used to log in to the Client as it's going to be set as part of the ACCOUNTANTS group</li>
    <li>In the Domain Controller VM, go to the _SECURITY_GROUP OU,  right click on the ACCOUNTANTS to open up <b>Properites</b>, go to the <b>Members</b> tab and add the user as a member of the Group</li>
    <ul>
      <li>In this example, the user "ban.doh" is used</li>
      <li><img src = "https://github.com/ColtonTrauCC/network-fileshare/assets/147654000/9ccc7a04-e3eb-4145-8485-2431280b86e7" width = 80% height = 80%/></li>
    </ul>
    <li>Sign back into the Client VM with user you made part of the ACCOUNTANTS group and it should now have access to the accounting folder</li>
  </ul>
</p>

<p align="center">
<img src="" height = 20% width = 40%/>
</p>
    

<br/>
