# ActiveDirectoryLab

In this lab, we will be setting up a Basic Home Lab Running Active Directory using VirtualBox | Add Users w/PowerShell

![image](https://github.com/user-attachments/assets/ffaaa4aa-4078-49c6-8c2c-cd2c00f19383)


Let's Start off with downloading virtualbox from https://www.virtualbox.org/wiki/Downloads

Download Server2019 ISO from https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019

Download Windows 10 ISO from https://www.microsoft.com/en-us/software-download/windows10ISO

Once Windows 10 ISO and Server2019 ISO save them on your desktop in a folder to access later

![Image 11-9-24 at 3 51 PM](https://github.com/user-attachments/assets/c1b06829-0ee7-4f26-b4cc-b06d095ecbf7)
Open VirtualBox. Once opened, click "New" to add machine --> Name machine 'DC' or 'Domain Controller' --> change the version to other Windows (64-bit)

![Image 11-9-24 at 3 53 PM](https://github.com/user-attachments/assets/e9cddbeb-24ab-499d-9578-86adf7a6611a)
Go to systems --> change clipboard and drag n drop to bidirectional
and change base memory to 2048 MB & processor to 2 CPU


![Image 11-9-24 at 3 59 PM](https://github.com/user-attachments/assets/905d8b28-e90a-42cd-8f6c-e525ca35a055)
Go to network --> add two NATs --> NAT 1 add to internet --> NAT 2 add to internal VM
Hit apply

![Image 11-9-24 at 4 02 PM](https://github.com/user-attachments/assets/ac0bdbe4-c31e-4d93-bd1b-42795d77f258)
At this point start your empty machine
You need to go to the folder you saved your two ISO files in

Add in Windows Server 19 ISO

![Image 11-9-24 at 4 07 PM](https://github.com/user-attachments/assets/8dd8d994-d4e4-49a3-95b3-3dddb5abda8b)
Once everything is loaded, your screen should look liike this
Hit next --> select the STANDARD desktop experience --> select custom install --> next
![Image 11-9-24 at 4 20 PM](https://github.com/user-attachments/assets/a1b0f2ab-d983-4f45-a5d6-3d425171e8ef)
Let this load and boot by itself and do NOT touch the keyboard

![Image 11-9-24 at 4 39 PM](https://github.com/user-attachments/assets/db588369-49ff-48c7-910e-0444c74a4999)
2019 Windows Server is now installed --> password is Password1 --> login into your server

Let's set up our IP Address --> click network internet button on right bottom --> click change adapter 
![Image 11-9-24 at 4 52 PM](https://github.com/user-attachments/assets/07e3bd8c-7041-4ab3-87ce-089ff39356bb)
Here you have to figure out which one is your home internet and which one is internal vm internet

![Image 11-9-24 at 5 31 PM](https://github.com/user-attachments/assets/9f568089-c956-435d-b2b2-dcf33d01c4dd)
To check which ethernet connection is which, you need to right click the ethernet icon, status, and details 

![Image 11-9-24 at 5 46 PM](https://github.com/user-attachments/assets/98522aca-09cb-4484-b87b-a86fa131cc95)
Need to change the IP address on the internal network. Right click on internal —-> properties —> IPv4 and double click on it —> add in IP: 172.16.0, Mask: 255.255.255.0
Use yourself as a loopback address
So you ping yourself

![Image 11-9-24 at 6 31 PM](https://github.com/user-attachments/assets/d45d5d0b-7f09-4009-b832-aa5b929b01e1)
In the server manager —> add roles —> next —-> next —> Active Directory Domain Services —> next —-> next —> install

![Image 11-9-24 at 6 37 PM](https://github.com/user-attachments/assets/5dc1f9f0-fce4-4eba-8ce2-9d46ae9d4398)
AD is now installed on the server manager

![Image 11-9-24 at 6 41 PM](https://github.com/user-attachments/assets/de0b369f-ab0b-4fbd-868e-1f3552c28710)
After AD is configured, you need to add a post-deployment configuration. Hit ‘add a new forest’ and name the Root domain name: mydomain 

Hit next —-> asks for password: Password1 —> next —> next —> next —> install 
Computer automatically restarts because AD was installed 

![Image 11-9-24 at 7 58 PM](https://github.com/user-attachments/assets/78cb07b3-9f26-4f9b-81ef-37bb8dcc0fa7)
Notice how the login screen now says MYDOMAIN\Administrator

![Image 11-9-24 at 8 03 PM](https://github.com/user-attachments/assets/980e8321-e046-4c92-96de-e453ab437e40)
Now we’re going to create our own dedicated domain Admin account instead of using the built in administrator 

Start —> Windows Administrative Tools —> Active Directory Users and Computers

![Image 11-9-24 at 8 04 PM](https://github.com/user-attachments/assets/0cb7974d-0e4f-42c3-89d6-4700b3527a6b)
Right click on mydomain —> New —> Organizational Unit
Name it _ADMINS —> uncheck the box —> okay
Click on _ADMIN —> New —> User 

![Image 11-9-24 at 8 14 PM](https://github.com/user-attachments/assets/43b91467-b096-4ffc-8f5f-83356976c398)
Enter [Your First Name] —> [Your Last Name] —> [a] for admin + [first initial of First Name] + [Last Name] —> next —> add password [Password1] 
*Check Password never expires for purposes of this lab*
Hit finish

![Image 11-9-24 at 8 16 PM](https://github.com/user-attachments/assets/a176fd9e-a875-48cb-af81-f0b5aa0c7d7b)
We have an admin account but it’s not official an admin account

![Image 11-9-24 at 8 25 PM](https://github.com/user-attachments/assets/db6cc527-b58f-4cc0-8995-1a44af6a8188)
Right click —> properties —> member of —> add —> type in domain admins —> check names —> okay —> apply

![Image 11-9-24 at 8 29 PM](https://github.com/user-attachments/assets/07b2f92e-d2d9-4d20-906a-dbb9d5695e53)
Log out of account —> click other user —> use your domain user account

Now we need to create our RAS/NAT connection to allow client1 (windows 10) to be on a virtual private network to access the internet to through the domain controller. 

![Image 11-9-24 at 8 52 PM](https://github.com/user-attachments/assets/d48406bb-4d57-48df-b6a6-f3049cce58c6)
Add roles and features —> next —> next —> next —> remote access —> next —> next —> routing —> add features —> next —> next —> next —> install

![Image 11-9-24 at 9 30 PM](https://github.com/user-attachments/assets/f4c1296d-bccb-4606-9e26-127984e09b6c)
Tools —> Routing & remote access —> right click DomainController on the left side —> configure and enable remote access —> enable Network Address Translation (NAT) —> next —> click the internet —> next —> finish
RAS & NAT is Complete

Set up DHCP controller on Domain Controller which allows our Windows 10 Clients to get an IP address to let them get on the internet to browse the internet from a private internal network 
![Image 11-9-24 at 9 45 PM](https://github.com/user-attachments/assets/68edd09f-bd41-4450-ac27-d2d3ddab8f3e)
Add roles & features —> next —> next —> next —> DHCP Server —> Add Features —> next —> next —> next —> install 

![Image 11-11-24 at 11 08 AM](https://github.com/user-attachments/assets/69e5eb44-8d74-4bc8-ad6d-cccab58e47f2)
Tools —> DHCP —> on the left side click the down arrow —> IPv4 —> right click —> new scope —> next —> name your scope after IP range

![Image 11-11-24 at 11 16 AM](https://github.com/user-attachments/assets/64b4c844-ab4b-49af-825e-ba16558c175e)
Range is 172.16.0.100-200
Add in your start rand and end range and make your length 24 --> next --> next --> next

![Image 11-11-24 at 11 20 AM](https://github.com/user-attachments/assets/a3b48bd7-8a3a-41f7-b969-3bb480f8789c)
Add in the default ip address for the DC 
Hit ‘add’ Next —> next —> next —> finish 

![Image 11-11-24 at 11 22 AM](https://github.com/user-attachments/assets/3f9c604a-bfe1-4ca6-b49d-2631c89cdd3b)
Right click on the DC.mydomain.com —> click authorize —> then refresh
In the DC window we need to configure the local server that lets us browse the Internet https://github.com/joshmadakor1/AD_PS/archive/refs/heads/master.zip
![Image 11-11-24 at 12 02 PM](https://github.com/user-attachments/assets/0374cb8e-3f18-4cb0-b8d6-ed8305522aab)

![Image 11-11-24 at 12 10 PM](https://github.com/user-attachments/assets/df1c31d6-d1cf-43a3-9c70-2a41e5c43c81)
Extract the script onto the desk —> open folder and open txt file called names —> add your name —> save file and close

Open PowerShell —> go to ISE —> right click and run as an administrator 
![Image 11-11-24 at 12 25 PM](https://github.com/user-attachments/assets/8ed25f5d-f904-4cdd-881f-5c8cfc440c94)
In PS open fold you just downloaded —> in PS script type ‘Set-ExecutionPolicy Unrestricted’ —> yes to all
To run and pull in the names from PS you need to cd c:\users\a-anwachukwu\desktop\AD_PS-master
Hit enter —> ls —> play button 



