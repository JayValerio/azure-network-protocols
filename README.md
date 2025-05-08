<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
  
<h2>Objectives </h2>

- Set up network file shares and permissions on DC.

<h2>Create Some Sample File Shares</h2>

<p>
On our DC-1 VM lets go into the C drive and create some folders, “read-access”, “write-access”, “no-access”, “accounting”.
</p>
<p>
  Set the following permissions (share the folder) <br/>


Folder: “read-access”, Group: “Domain Users”, Permission: “Read” <br/>
  <p>

  ![image](https://github.com/user-attachments/assets/9b04027d-8c38-4c57-8bdc-3c817bbc1f3b)

</p>
Folder: “write-access”,  Group: “Domain Users”, Permissions: “Read/Write” <br/>
<p>

  ![image](https://github.com/user-attachments/assets/cc6c5934-f30f-42ef-9525-fd7d4008476b)

</p>
Folder: “no-access”, Group: “Domain Admins”, “Permissions: “Read/Write” <br/>
<p>

  ![image](https://github.com/user-attachments/assets/f3e1087d-afa4-4ab1-bd26-06f687fc1af2)

</p>
(Skip accounting for now) <br/>


</p>

<p>
  Now that we have set the permissions on our DC-1 VM, lets move over to our Client-1 VM and attempt to access the files we created. To access them on client-1 we open file explorer, in the search bar type in '\\dc-1' to access the shared files.
</p>
<p>
  
 ![image](https://github.com/user-attachments/assets/97968d7a-ba8d-4854-88d3-2a873f327cf6)
</p>

<p>
  Lets interact with the 'read-access' folder first, as you will see you can access the folder, but lets say you attempted to create a new file/folder you would get an access denied message.

</p>
<p>
  
 ![image](https://github.com/user-attachments/assets/d1a4a1fe-8081-48bd-8ce9-af37d02c79c3)

</p>
<p>
  In the 'write-access' file we can create new text files and folders as normal since we have permissions to do so there.

</p>
<p>
  
 ![image](https://github.com/user-attachments/assets/1932748f-6515-4c73-978c-905f53a097b7)

</p>


<p>
  In the 'no-access' folder you will not be able to access it at all, you will get a network error message.


</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/df2fd94c-9a70-4996-bef6-f26870d2ed78)


</p>
<p>
  If you havent noticed already, we cant even see the accounting folder at this point because we have not configured any network sharing permissions on that folder.

</p>
<p>
  Now lets create an "ACCOUNTANTS" security group in our DC-1 VM. For this we need to open up 'Active Directory Users And Computers'

</p>
<p>
  
  ![image](https://github.com/user-attachments/assets/34517dab-c638-4f05-980f-fe63f07e8534)



</p>

<p>
  
 On the “accounting” folder you created earlier, set the following permissions:
Folder: “accounting”, Group: “ACCOUNTANTS”, Permissions: “Read/Write”


</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/288320cc-33db-45f3-9346-227176d9600e)


</p>
<p>
  When we try to access the folder on client-1 we still do not get access to this folder because the access is only available to the users under the "ACCOUNTANTS" security group.
</p>

<p>

![image](https://github.com/user-attachments/assets/ad8c57fc-1dc6-4671-86d2-5a8c2d91a2c7)

  
</p>

<p>
Now we must log out of client-1 and go back to DC-1 and add this user to the "ACCOUNTANTS" securtity group.
  
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/5a817e2c-8614-419a-8be2-88b0f524d7cf)

</p>
<p>
  Now that our user on client-1 is a part of the "ACCOUNTANTS" security group, we can log back in and attempt to gain access to the folder.
</p>
<p>

![image](https://github.com/user-attachments/assets/d3aa1a5c-f7b8-4a29-a983-e8a203d9eed6)

  
</p>
<p>
  With this we can provide access to certain users for specific items. You can also give entire groups permissions through AD, allowing entire departments to have access to certain items on the computer.
</p>

<p>
  
  ![image](https://github.com/user-attachments/assets/ec0b7db8-faa4-4b84-a106-e46dfd4b4040)

![image](https://github.com/user-attachments/assets/da27e32a-ff47-449d-b485-ca1972ebf810)

![image](https://github.com/user-attachments/assets/92082708-617f-427d-80fe-0484d89b5395)

</p>

<p>
  Now all "Employees" in the "SECURITY" group will have access to the aaccounting folder. </br>
  </br>
  </br>
  Network file sharing, combined with proper permissions, enables efficient collaboration by allowing users to access and manage files over a network. However, it is crucial to implement strict access controls and permissions to ensure data security, privacy, and prevent unauthorized access or modifications.

</p>
