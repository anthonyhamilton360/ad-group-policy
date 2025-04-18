
![Screenshot 2025-03-15 190857](https://github.com/user-attachments/assets/5ac6045a-86bf-4b1a-b068-d695f4e7820e)


</p>

<h1>Group Policy and Managing Accounts</h1>
This tutorial explores deploying an Active Directory environment, from creation and management to deactivation and removal.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory
- Powershell
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
- Windows Server 2022

<h2>High-Level Configuration Steps</h2>

- Dealing with Account Lockouts 
- Enabling and Disabling Accounts
- Configure Domain Password Lockout Policy
- Observing Logs

<h2>Configuration Steps</h2>

<p>
  
![Screenshot 2025-03-11 002655](https://github.com/user-attachments/assets/26794961-4914-4763-858f-ffcf11e30773)

</p>
<p>
Go to virtual machines in Azure, choose client-1 and dc-1, and then launch the virtual machines.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 002725](https://github.com/user-attachments/assets/c72a84bd-1985-4136-b7cb-c6b6dc317ead)

</p>
<p>
After copying and pasting client-1's IP address into Remote Desktop, click Connect.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 002938](https://github.com/user-attachments/assets/6b5d337d-a86c-45e9-a48e-b3c2c5c1a0fa)


</p>
<p>
Attempt to lock out the account by entering the wrong password 10 times or more while trying to gain access to client-1.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003334](https://github.com/user-attachments/assets/6293b6a4-5fb4-4b5e-a5ad-22c689352f59)

</p>
<p> In order to apply the lockout policy it has to be configured within Group Policy Management. Once in dc-1 logged in as admin, right-click on the start menu and select Run.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003348](https://github.com/user-attachments/assets/59d39426-4c3e-4ca7-bd06-e24fe5a89084)

</p>
<p>
In Run, type gpmc.msc to open up Group Policy Management.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003356](https://github.com/user-attachments/assets/2c4991b8-fa6d-433e-881b-67683b46db60)

</p>
<p>
Once in Group Policy Management, click the drop down arrow on Forest:mydomain.com.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003550](https://github.com/user-attachments/assets/a9635409-2c56-4f0f-8967-42a08284f929)

</p>
<p>
Click OK.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003605](https://github.com/user-attachments/assets/78c9a5ba-0483-4bef-9a88-58041b7eab98)

</p>
<p>
Navigate to the Default Domain Policy within the drop down under mydomain.com.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 003956](https://github.com/user-attachments/assets/4492427e-c26e-498c-ac08-136ada89ef28)

</p>
<p>
Right-click on the Default Domain Policy and select Edit.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004135](https://github.com/user-attachments/assets/621b64f2-e8d2-4850-80ea-904aa7d574f7)

</p>
<p>
In the Group Policy Management Editor, expand Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy.

</p>
<br />

<p>
  
![Screenshot 2025-03-11 004258](https://github.com/user-attachments/assets/e17c3446-417b-48d9-92f9-7e8924b99648)

</p>
<p>
Set the Account lockout duration to 30 minutes and check the box on "Define this policy setting."
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004423](https://github.com/user-attachments/assets/fc3419cb-889e-446c-94fd-0c4cc4e3d1b6)

</p>
<p>
Select Ok.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004457](https://github.com/user-attachments/assets/21837b74-d9ef-4015-8fab-f66c473aed4f)

</p>
<p>
Enable the Administrator account lockout and click apply and click OK.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004508](https://github.com/user-attachments/assets/838ca2cb-e847-4b8e-bd5e-2f3208536220)

</p>
<p>
Observe the changes.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004624](https://github.com/user-attachments/assets/1a57ee6a-ebdd-4828-8f73-46303e4eb8bb)

</p>
<p>
Go back to the Group Policy Management and navigate back to Default Domain Policy and go to settings and verify the changes.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004739](https://github.com/user-attachments/assets/88183ae0-7e86-49b9-8fdf-5567debd9ea1)

</p>
<p>
Back in Azure, go to virtual machines and copy client-1's IP address into Remote Desktop and click Connect.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004816](https://github.com/user-attachments/assets/1f1ec40e-d6be-454f-b6aa-4e9d40c0dc64)

</p>
<p>
Login as jane_admin in order to  force the changes using gpudate in command prompt.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004915](https://github.com/user-attachments/assets/b0b845cc-0c50-4bc6-92e2-8f7938e80f31)

</p>
<p>
Once in client-1, open command prompt.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 004958](https://github.com/user-attachments/assets/f38c586a-7e46-4286-9b2f-04ac4a039e78)

</p>
<p>
Type gpupdate /force and press enter.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005029](https://github.com/user-attachments/assets/f8319739-6b43-4fff-a2b5-112339058c18)

</p>
<p>
The update has been completed successfully.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005254](https://github.com/user-attachments/assets/8c897c06-6d64-4616-a848-c8eb266f8628)

</p>
<p>
Type gpresult /r and press enter.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005420](https://github.com/user-attachments/assets/44a29e0b-8589-40d5-ba03-a330deac9e40)


</p>
<p>
Notice that the Default Domain Policy has been applied.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005552](https://github.com/user-attachments/assets/83907d31-7b1f-4445-a115-87e0881cb2ba)

</p>
<p>
Back in Azure, log out of client-1 and try to lock out one of the random accounts after 5 failed attempts and notice the lock out message that appears.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005731](https://github.com/user-attachments/assets/8fc21ac3-4c24-42b6-b125-a93c60972e9b)

</p>
<p>
In client-1, search for Active Directory Users and Computers.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005746](https://github.com/user-attachments/assets/9713fea4-0589-4784-90c7-3c43a358d833)

</p>
<p>
Expand mydomain.com, right-click on _EMPLOYEES and click Find.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005759](https://github.com/user-attachments/assets/820cbfb9-298a-4cda-b5e3-d46fd955e1b7)

</p>
<p>
Type the name of the user and click on Find Now to locate that user. In my case it was lil.jof
</p>
<br />

<p>
  
![Screenshot 2025-03-11 005922](https://github.com/user-attachments/assets/e6dc6abe-a80f-4d21-8279-e7bd96d06189)

</p>
<p>
  Right-click on the user and select properties. Check the "Unlock account. The account is currently locked out on the Active Directory Domain Controller" box, select Apply and OK.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 010052](https://github.com/user-attachments/assets/1ad9d498-9a24-4795-a11b-4546e9bfa804)

</p>
<p>
After the account is unlocked, I logged back into client-1 as lil.jof and opened command prompt in order to verify.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 010140](https://github.com/user-attachments/assets/6bf4e9ed-bcfb-4fb9-a812-65b121ce97bd)

</p>
<p>
Back in dc-1, Open up Active Directory Users and Computers to search lil.jof. Right-cick and select Reset Password.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 010244](https://github.com/user-attachments/assets/5dbf5d99-7b1f-4167-bfe1-3082f0b44508)

</p>
<p>
Enter a fresh password and make sure.  The "Unlock the user's account" option should also be checked.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011153](https://github.com/user-attachments/assets/990e139d-3ef0-4ce6-994f-042632d59dc7)

</p>
<p>
Logged back in as lil.jof in client-1.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011257](https://github.com/user-attachments/assets/6fcde54a-2779-431a-8b84-27b1886ff679)

</p>
<p>
Login was successful.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011452](https://github.com/user-attachments/assets/2ac66cf5-7387-4cc1-92cc-6bd6b2e78c98)

</p>
<p>
Once inside client-1 as lil.jof, search event.viewer.msc
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011619](https://github.com/user-attachments/assets/6d7934a6-a2bf-46fd-9e9a-7fb4d7aac7fe)

</p>
<p>
Expand Windows Logs in Event Viewer, then right-click Security and choose Find.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011634](https://github.com/user-attachments/assets/1ee6435e-0f64-4eca-807c-c71ece0b63e1)

</p>
<p>
Search the user lil.jof and click Find Next.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011850](https://github.com/user-attachments/assets/d207fa41-7558-4bf9-929c-6e441528d79d)

</p>
<p>
Cannot access the query because it needs administrator rights.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 011920](https://github.com/user-attachments/assets/3d3dab71-e28b-42b4-a782-28b01c31f252)

</p>
<p>
Search for event.viewer.msc,right-click and run as administrator.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 012005](https://github.com/user-attachments/assets/94496f27-8898-41f4-863d-0f48065877a4)

</p>
<p>
Login as Jane Smith to gain administrative rights
</p>
<br />

<p>
  
![Screenshot 2025-03-11 012114](https://github.com/user-attachments/assets/11f04dd1-a911-409d-b5cb-86b14639c710)

</p>
<p>
Go to Security after expanding Windows Logs, then right-click and choose Find.
</p>
<br />

<p>
  
![Screenshot 2025-03-11 012237](https://github.com/user-attachments/assets/38d289e5-e2b0-4c89-9438-cf6af0fae1de)

</p>
<p>
To conclude this lab, observe the failed attempts to login as lil.jof to conclude the lab.
</p>
<br />


