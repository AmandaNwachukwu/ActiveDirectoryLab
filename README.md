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




