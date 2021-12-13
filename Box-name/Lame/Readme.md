




Hack the box :  Lame (can also download as pdf)
=============

Introduction
-------------

This is one of the easy boxes on hack the box, and it is also one of the most notarised, making it easy for beginners to see different tutorials on how to do it.  I will be using Metasploit, however in the oscp exams you are not allowed to use Metasploit, so for a tutioral on how to do it without metasploit check out https://0xdf.gitlab.io/2020/04/07/htb-lame.html .  https://0xdf.gitlab.io/   also has a lot of really good write ups, with a good amount of detail for beginners to look at.  Another good tool for beginners to learn hackthebox is “Cyber mentor”. He goes into the most detail out of the tutorials I have found. He has a lot of walkthroughs for beginner boxes and walks you through what all the tools do , as well as helping you to build you up step by step. Please find the cyber mentor link below: https://www.youtube.com/watch?v=ntBkyid_u8Y&list=PLLKT__MCUeiyxF54dBIkzEXT7h8NgqQUB&index=2 .







### Nmap vs zenmap
I am going to talk about 2 tools that you will use when you start pentesting and hack the box. Nmap is a tool that allows you to scan ports to find which ones are open and what system is running on the port. Nmap is done in command line and has a bunch of options and ways to scan. I would recommend to have a play around with the various nmap options, an image of which can be found below. Zenmap is the graphical version of nmap, that is nicer to look at for beginners, and shows you the nmap command it is running. This is helpful when you are trying to understand what each of these commands does. I have put below a comparison of a sample command and what nmap vs zenmap looks like for this same command. From my experience I feel it is nicer having the nmap just in a tab in my command, instead of having to go to another program to look back and forward when sometimes doing multiple nmap scans.



#### Nmap options image
below is a image of   the  command   nmap –help

                    
> nmap -help

![nmap_help](https://user-images.githubusercontent.com/95282035/145772118-31726f7d-7ce2-46db-a66e-b60a8abb8a89.jpg)



This allows you to see what the function on nmap do

### zenmap scan
![zenmap2](https://user-images.githubusercontent.com/95282035/145772309-6e817a2f-170c-431c-b411-190b3c6d4361.png)


### Nmap scan

![nmapsame](https://user-images.githubusercontent.com/95282035/145772475-961c9942-24ee-4a65-ad8c-031827faca53.png)



### Info about nmap/zenmap
Nmap has a book that goes through what each of the functions does to help you learn your way around. Both Zenmap and Nmap are completely free.
Nmap - https://nmap.org/book/man-target-specification.html 
Zenmap - https://nmap.org/book/zenmap-scanning.html 

Whenever you get a new box, the first thing I would do is to use as it is part of your recon. This is the most important stage of a pentest or CTF box. 


### Nmap scan breakdown

>sudo nmap - A 10.10.10.3

-A: Enable OS detection, version detection, script scanning, and traceroute
10.10.10.3 = ip of the target we are scanning

### Results Nmap
I will now look at the open ports and search for vulnerabilities in them.

#### Google – searchspolit 
Now as you get more experienced in doing Hackthebox and CTF you will start to learn what are common weakness that a lot of boxes use while you do not have this depth of knowledge google and exploit-db will be your best friends.

Once you have your open ports and what possible OS they are running you can do 2 things one is google search each of the OS for vulnerabilities and see what there is. The other option is to do it in command line with a tool called searchspoilt this tool connects to Exploit-DB to see what vulabilties are known on the database

The first thing i saw was vsftpd 2.3.4 so i will search to see any exploits it has.

#### Google search image　

![google](https://user-images.githubusercontent.com/95282035/145771949-d337b598-d2e3-448c-9439-07ecdf4b6857.png)


#### Searchsploit image

![searchsploit_github](https://user-images.githubusercontent.com/95282035/145772662-2d2628fe-a4f3-4698-aada-faba9b0d7d0f.png)


#### Metasploit Vsftpd 2.3.4

Metasploit is a very powerful tool that has ready made scripts that you can use to attack known vulnerabilities in systems if found on searchsploit.
>msfconsole

![msfconsole](https://user-images.githubusercontent.com/95282035/145772797-d43f13e1-c6a7-481b-8023-4111a5df9128.PNG)

Search vsftpd   -  This will show you the vulnerabilities and where the path to it is in metasploit so just copy the path which is under the name for the exploit you want.
![meta search](https://user-images.githubusercontent.com/95282035/145772940-8b3d9441-ac8d-4f5a-a88d-e64dfb1966f4.PNG)

#### Options
Options will tell you how the attack works and what you need to do to get it to work on this attack. I need to set the Rhosts.

![options](https://user-images.githubusercontent.com/95282035/145773118-15d275a7-e79e-4789-a333-cd9243beeab6.PNG)

### Rhosts
Rhosts = IP address of the target you are trying to attack
![rhosts](https://user-images.githubusercontent.com/95282035/145773228-f8f53612-0348-4988-81ee-f101a9fbedfd.PNG)

### Run
Once everything is set all you have to do is type command run and the attack will start
![run_vsftpd_meta](https://user-images.githubusercontent.com/95282035/145773408-64c4b0ff-f928-4d9c-aa6e-4fc67be68d18.PNG)

### Why Session not created
The exploit seems to have run but no session was created. I am not sure why this happened and am still trying to research why. I will update the section when I have an answer on why so other people can understand as well.

#### Next on list port 445

The next thing I saw was samba 3.0.20 on 445 so I will give that a search.

![samba 20_search](https://user-images.githubusercontent.com/95282035/145774683-fc5c811d-5f1c-4e88-a2a6-b27556cb80ce.PNG)

I see there is a command execution usermap so we will use that.  Normally I will look for command execution as my go to option if there are multiple options.


#### Search and use
I am searching the exploit on metasploit same as we did above with vsftpd

![search_use](https://user-images.githubusercontent.com/95282035/145775790-6687f8aa-dc4f-4a8f-81f6-e4015eca3ddf.PNG)

#### Setting r-l hosts
This time we have to set Rhost again and this time Lhost. Lhost is used to listen to the result of the scan this time so we need to set it to are IP address.  On Lhost I set it to tun0 this is a command that means vpn ip address being used.

![options_samba_lr_set](https://user-images.githubusercontent.com/95282035/145775909-5a61a757-e342-4b71-8050-62da20d6e2d9.PNG)

#### Run
As with above now everything is set we run the exploit

![run_samba](https://user-images.githubusercontent.com/95282035/145776384-956d56fb-9a2b-445f-a969-941ded1390ae.png)

### Shell
Now we have a shell that will look weird to most people as there is no text and it will just give you a blank line. This is just how shells look when using metasploit. There are ways to make this look nicer. I did not do that here.
I then did this command 
.find . -name user.txt   

This will look for any folder that has that name in hackthebox you are looking for the user.txt and root.txt these are what are considered flags.
### Search user.txt flag
0df5***************f5a

### Search root.txt flag
370*****************df

### End

I hope you enjoyed this write-up of the box Lame more write-ups will be up soon.






