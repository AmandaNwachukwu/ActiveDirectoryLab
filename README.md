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
To check which ethernet connection is which, you need to right click the ethernet icon, status, and details --> the 169.254.234.63 is the the internal IP address

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

![Image 11-9-24 at 8 04 PM](https://github.com/user-attachments/assets/0cb7974d-0e4f-42c3-89d6-4700b3527a6b)
Right click on mydomain —> New —> Organizational Unit
Name it _ADMINS —> uncheck the box —> okay
Click on _ADMIN —> New —> User 

![Image 11-9-24 at 8 14 PM](https://github.com/user-attachments/assets/43b91467-b096-4ffc-8f5f-83356976c398)
Enter [Your First Name] —> [Your Last Name] —> [a] for admin + [first initial of First Name] + [Last Name] —> next —> add password [Password1] 
*Check Password never expires for purposes of this lab*



