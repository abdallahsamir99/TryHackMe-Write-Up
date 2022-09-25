<h1>TryHackMe: Pickle Rick Walkthrough</h1>
A Rick and Morty CTF. Help turn Rick back into a human!

https://tryhackme.com/room/picklerick

![1_oI-mrJuUN00omQnhK7eWNw](https://user-images.githubusercontent.com/92990208/192146378-c8a814bf-b4c0-41c6-822a-a43824fdee73.png)

> Let’s start with enumeration

We start with a Nmap scan on the given IP address
to show the open ports and get more information about IP address

![1_JArFCetWZvS0MJ91A_OKQw](https://user-images.githubusercontent.com/92990208/192146420-74749b1a-2846-4a63-b484-9d8341cb1f9a.png)

Nmap gives us this result and only 2 ports are open.
Here we are able to see that our SSH port is open. This port isn’t too vulnerable unless we have found someone’s credentials, we can ignore port 22 for now, and hence it leaves us with port 80. Go to http://10.10.197.80/ where we see a page hosted as follows

![1_bdVMWzIp_vEiLLHUVnSSXA](https://user-images.githubusercontent.com/92990208/192146443-baf99716-d630-40dc-8d5d-7d67139287cf.png)

By looking for the first time, we can see that there is nothing important on this page.

But what if we check the page source?

![1_OGxpsfTqjXY27Fk7Mp_78w](https://user-images.githubusercontent.com/92990208/192146454-e95a1581-90ef-44ff-a402-30d89ed13b96.png)

We got a username here in the HTML comment

username: R1cKRul3s

Now check if there is important information in robots.txt


![1_d_3HvV-1-0RRo_XE7sOZcA](https://user-images.githubusercontent.com/92990208/192146473-655e4c0f-569a-43e5-90ea-f474d5a96173.png)

Looks like we found the password

password:wubbalubbadubdub

> step 2

Now, try to find hidden directories

In this case, we can use dirbuster to get the hidden directories

![1_bLpx2f82lWI1qdKdNznR0Q](https://user-images.githubusercontent.com/92990208/192146501-50c48fa5-5fbe-49e7-8add-55f6d3e0bb41.png)

![1_T1dSXVDKBfiBb3wkxbrNSQ](https://user-images.githubusercontent.com/92990208/192146528-406874ba-bc1e-40a4-8003-93291b4f72d3.png)


We can see here some of the hidden directories, You will notice that there is a login page.

![1_TbaWqtbsyNK_Nc6LcvYm7A](https://user-images.githubusercontent.com/92990208/192146550-b8b81fec-9f4e-4f35-8782-abe4430a694d.png)

Go to the login page and enter the credentials.


![1_NOGYz7QNyLShgWJdvOIdSQ](https://user-images.githubusercontent.com/92990208/192146573-c1bacd5a-3987-4b93-b7ee-d5a0c0ac898a.png)

This page is called the command portal lets try and actually enter some commands and see what happens.
If we enter the ls command we can see that some results are being returned. It would seem that we have also found our first ingredient.


![1_BE4JO8MArjzx_mf6IgPxYg](https://user-images.githubusercontent.com/92990208/192146588-e406c942-e2f3-496f-9c34-4befba400a32.png)


When we try to open the first text file with the command cat to see the first ingredient we see this page which means there are some commands we cannot use instead of using cat we can use the command nl

![1_3rsWXuDYN8T8lVNMybXALQ](https://user-images.githubusercontent.com/92990208/192146626-64c4e5f0-0893-49dc-a894-67facc274eb9.png)

**Now we can see the first ingredient**

We have now found one ingredient, and we have two ingredients to find

To find the other ingredients, let’s go and take a look at the files of the system.

![1_Zx9SCQ1O9Iuq80GDV1OqAg](https://user-images.githubusercontent.com/92990208/192146649-5941c73a-7469-4daa-b4a6-5f057b8df1aa.png)

We note that We can run Sudo commands without any password

Here we have a list of all folders and subfolders in the root. Upon closer inspection, we find two flags: /home/rick/second ingredients and /root/3rd.txt


![1_HY4OssJRb4t7G_HtpTSAMQ](https://user-images.githubusercontent.com/92990208/192146668-2eaf8366-7fc2-43b8-8d6b-f4688fe4a241.png)


![1_-3wLoZXEY79itEfIcIk1aQ](https://user-images.githubusercontent.com/92990208/192146676-5e3b8ed8-905c-4a8c-b01a-6255633736ad.png)

Finally, we find the three ingredients to help rick back into a human !!

