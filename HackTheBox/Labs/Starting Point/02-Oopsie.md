# Oopsie
---
### Initial Enumeration and Foothold

[[Nmap]] on **10.10.10.28** reveals ports 22 and 80 are open

```bash
nmap 10.10.10.28
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http
```

Going to `http://10.10.10.28/`

![[Pasted image 20210928015852.png]]

In the source code there's a javascript file being referenced 
>`http://10.10.10.28/cdn-cgi/login/script.js`

Navigating to `http://10.10.10.28/cdn-cgi/login/` shows a login page

The username and password  `admin:MEGACORP_4dm1n!!` from [[01-Archetype]] allow access to the **Admin Panel**

![[Pasted image 20210928020816.png]]

The **Uploads** tab looks juicy, but requires **super admin** privileges. 
>I continue to Inspecting the source code, console, and network tabs.

I find that a Cookie sent in the request contains 
```bash
role: "admin"
user: "34322"
```

Since the user's account id is suplied in the URI of the web request, I attempt a brute force attack using [[BurpSuite]]'s Intruder module. 
>First, I intercept the request and hit `ctrl + i` to strart *Intruder*

The *Intruder* tab allows us to change the payload flags to the id in the URI and iterate through a list of numbers 1-100 which can be generated with a simple bash or python script. Then click **Start Attack!**

![[Pasted image 20210928022355.png]]

We find that user ID 86575 has super admin web privileges
>Let's go back to \#Uploads

![[Pasted image 20210928022846.png]]

---
### Upload Exploit 
Let's try to find