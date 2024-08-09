# GreenHorn

<p align="center">
<img src="./pwned.png?raw=true">
</p>

- Link: https://app.hackthebox.com/machines/GreenHorn
- Level: Easy

## Steps taken

These are a rough order of operations for the work done to pwn the GreenHorn machine on Hack The Box; A machine labled as an 'easy' box.

- Started the box, VPN, and ran a ping check

- Ran my usual NMAP nmap -sC -sV -A 10.10.11.23 

- Ports 22, 80, 3000, & 8080 are open

- Add the HTTP-TITLE found in the NMAP to our /etc/hosts file

- Visit the webpage and we have a WebDev page that has an admin login at the bottom. The app referenced, Pluck 4.7.18, has a remote shell vulnerability. 

<p align="center">
<img src="./splashpage.png?raw=true">
</p>

- We'd need to log in to this app to perform that as I can't see any option to do that right now.

- Next logical place is exploring the other ports. 

- Find what looks like a git repo at port 3000

<p align="center">
<img src="./greenhorngitrepo.png?raw=true">
</p>

- Explore all the directories until I found a hashed password in the data directory.

- I tried cracking with HashCat but I got a insufficient memory error so let's try crackstation before beefing up the machine

<p align="center">
<img src="./hashtype.png?raw=true">
</p>

<p align="center">
<img src="./hashcommand.png?raw=true">
</p>

- We got our password, let's try SSH, and then that admin portal. (Admin portal logged in) 

- I found a place to perform a file upload so I prep the php shell I have saved

- The exploit requires it as a .pdf so we zip it up before uploading it

<p align="center">
<img src="./payloadzip.png?raw=true">
</p>

- We start a netcat listener on a new tab, and visit the link provided in the exploit page

<p align="center">
<img src="./reverseshell.png?raw=true">
</p>

- This spawns a shell which we immediately upgrade -> /usr/bin/python3 -c 'import pty; pty.spawn("/bin/bash")'

- Looking around there's a junior user which we are not actively sign in as; Also found a user.txt file that we can't get into

- I try to swich into that user with the password I have and it works; So we now know Junior and Admin are the same person in this context.

<p align="center">
<img src="./userflag.png?raw=true">
</p>
 
- The other file in here is an 'OpenVas.pdf' that we can't open

- Let's try to get it on our attack machine using WGET. (Need to understand why this works if we can't even open it locally) 

<p align="center">
<img src="./grappingthepdf.png?raw=true">
</p>

- Open the file and it has a pixelated password in the file, looks like an invite to the app.

- To be honest, I wasn't sure what to do here. After a while looking around online I discovered there's a tool to depixelate an image.

- Install and use the depix app, after cropping the pdf(app requires a .png) and we are able to show a long string password.

- Switch to root on the target machine, enter the password, and open the root.txt file


## Credits

- Reverse shell: https://github.com/pentestmonkey/php-reverse-shell
- https://crackstation.net/
- https://www.exploit-db.com/exploits/51592
- https://github.com/spipm/Depix

