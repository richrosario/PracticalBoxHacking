# PermX

<p align="center">
<img src="./Pwned.png?raw=true">
</p>

- Link: https://app.hackthebox.com/machines/PermX
- Level: Easy

## Steps taken

These are a rough order of operations for the work done to pwn the PermX machine on Hack The Box; A machine labled as an 'easy' box.

- Start the box
- Run a ping check on the device 
- Run an NMAP Scan to see open ports
- Find that 80 and 22 are open
- Nothing when you hit the site so i'm going to perform some DNS enumuration with FFUF

<p align="center">
<img src="./FUZZ.png?raw=true">
</p>

- That lms domain looks intersting so we add it to the /etc/hosts file
- Visit the site and we have a login screen for chamilo

<p align="center">
<img src="./chamilo.png?raw=true">
</p>

- Looking around the internet for an exploit and found the following: https://starlabs.sg/advisories/23/23-4220/
- The exploit involves sending a reverse shell file via curl to the target server, then calling it.
- Found a good php reverse shell online, linked below.

<p align="center">
<img src="./exploit.png?raw=true">
</p>

- As you can see are file is in there so after calling it we get a reverse shell on our listener

<p align="center">
<img src="./reverseshell.png?raw=true">
</p>

- Then I used the python one-liner python3 -c ‘import pty; pty.spawn(“/bin/bash”)’ to get a a stable shell
- Did some digging and the only item of value is I find a user called mtz in /home
- Looking around online I find out I should be looking for a config.php file that would contain database credentials.

<p align="center">
<img src="./configdb.png?raw=true">
</p>

- With our newly obtained credentials I decided to try the password, via ssh login, with the mtz username found earlier
- This got me in via ssh as admins typically reuse their password. I found the user flag in here.

<p align="center">
<img src="./shell.png?raw=true">
</p>

- Ran sudo -l to check sudo privileges. Found IUser mtz may run the following commands on permx: (ALL : ALL) NOPASSWD: /opt/acl.sh
- I'm blocked from editing /opt/acl.sh but online I saw someone use something called linked files. Following a video of someone performing something similar on another retired box.
- What I did was make a script that allows our mtz user to change perms on a file for any user as long as its in the mtz direcory, so we created a link to the sudoers file and repalce the NOPASSWD attribute to ALL.
- This invovled a lot of trial and error and various resources but I eventually got escalated.
- Root flag was in there root directory.


## Credits

- Chamilo Exploit: https://starlabs.sg/advisories/23/23-4220/
- Reverse shell: https://github.com/pentestmonkey/php-reverse-shell
- ffuf Fuzz DNS Enumeration: https://github.com/ffuf/ffuf
- MYSQL: https://www.geeksforgeeks.org/mysql-in-kali-linux-command-line/



