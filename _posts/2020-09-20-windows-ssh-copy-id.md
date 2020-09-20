---
layout: post
title: "Windows's ssh-copy-id"
date: 2020-09-20 10:15:00 +8
comments: true
categories:
---



So now I am back using Windows again. This is the PC from my current company, yeah just keep it up with that. As I try to use OpenSSH in Windows, it has some differences from MAC and Linux, I guess. 

I want to copy SSH pubkey from my local machine to remote server (Ubuntu, in virtualbox). Hence, I just typed:

```powershell
PS C:\Users\IDICRAD\.ssh> ssh-copy-id .\id_rsa pompom@localhost -p 22100
# I use NAT network with port forwarding from remote (10.0.2.15:22) to localhost (127.0.0.1:22100)
```

But it doesn't work.

![](https://raw.githubusercontent.com/ichromanrd/blog-images/master/windows-ssh-copy-id/01.PNG)



Hmm, do some googling and I found this [reference](https://www.chrisjhart.com/Windows-10-ssh-copy-id/#:~:text=At%20the%20moment%2C%20Windows%2010's,Linux%20device%20for%20passwordless%20login.). So we just need to use this command:

```poweshell
PS C:\Users\IDICRAD\.ssh> type .\id_rsa.pub | ssh 
```

There is one more error.

<img align="left" height="100" src="https://raw.githubusercontent.com/ichromanrd/blog-images/master/windows-ssh-copy-id/02.PNG">



Yep just make a `.ssh/authorized_keys` file in remote server. Repeat `type` command and it works now. No need to enter password anymore.



Cheers! :beers: