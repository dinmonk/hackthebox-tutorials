
*(Table of Contents)**



Hack the box :  Lame
=============

Introduction
-------------

This is one of the easy boxes on hack the box, and it is also one of the most notarised, making it easy for beginners to see different tutorials on how to do it.  I will be using Metasploit, however in the oscp exams you are not allowed to use Metasploit, so for a tutioral on how to do it without metasploit check out https://0xdf.gitlab.io/2020/04/07/htb-lame.html .  https://0xdf.gitlab.io/   also has a lot of really good write ups, with a good amount of detail for beginners to look at.  Another good tool for beginners to learn hackthebox is “Cyber mentor”. He goes into the most detail out of the tutorials I have found. He has a lot of walkthroughs for beginner boxes and walks you through what all the tools do , as well as helping you to build you up step by step. Please find the cyber mentor link below: https://www.youtube.com/watch?v=ntBkyid_u8Y&list=PLLKT__MCUeiyxF54dBIkzEXT7h8NgqQUB&index=2 .







### Nmap vs zenmap
I am going to talk about 2 tools that you will use when you start pentesting and hack the box. Nmap is a tool that allows you to scan ports to find which ones are open and what system is running on the port. Nmap is done in command line and has a bunch of options and ways to scan. I would recommend to have a play around with the various nmap options, an image of which can be found below. Zenmap is the graphical version of nmap, that is nicer to look at for beginners, and shows you the nmap command it is running. This is helpful when you are trying to understand what each of these commands does. I have put below a comparison of a sample command and what nmap vs zenmap looks like for this same command. From my experience I feel it is nicer having the nmap just in a tab in my command, instead of having to go to another program to look back and forward when sometimes doing multiple nmap scans.



#### Nmap options image
below is a image of   the  command   nmap –help

                    
> nmap -help

![](https://github.com/dinmonk/dinmonk/blob/main/nmap.jpg)

This allows you to see what the function on nmap do
![](/examples/php/../uploads/nmap.jpg)
### zenmap scan
![](/examples/php/../uploads/zenmap2.png)
### nmap scan
![](/examples/php/../uploads/nmapsame.png)



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
i will now look at the open ports and search for vulnerabilities in them.
####Google – searchspolit 
Now as you get more experienced in doing Hackthebox and CTF you will start to learn what are common weakness that a lot of boxes use while you do not have this depth of knowledge google and exploit-db will be your best friends.

Once you have your open ports and what possible OS they are running you can do 2 things one is google search each of the OS for vulnerabilities and see what there is. The other option is to do it in command line with a tool called searchspoilt this tool connects to Exploit-DB to see what vulabilties are known on the database

The first thing i saw was vsftpd 2.3.4 so i will search to see any exploits it has.

#### Google search image　

![](/examples/php/../uploads/google.png)


#### searchsploit image

![](/examples/php/../uploads/searchsploit_github.png)

#### Metasploit Vsftpd 2.3.4

Metaspliot is a very powerful tool that has ready made scripts that you can use to attack known vulnerabilities in systems if found on searchsploit.
>msfconsole

![](/examples/php/../uploads/msfconsole_github.png)
