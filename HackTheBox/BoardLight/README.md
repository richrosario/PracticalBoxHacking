# BoardLight

<p align="center">
<img src="./Pwned.png?raw=true">
</p>

- Link: https://app.hackthebox.com/machines/BoardLight
- Level: Easy

## Steps taken

These are a rough order of operations for the work done to pwn the BoardLight machine on Hack The Box; A machine labled as an 'easy' box.

1. Start the box
2. Run a ping check on the device 
3. Run an NMAP Scan to see open ports
4. Find that 80 and 22 are open
<p align="center">
<img src="./nmap.png?raw=true">
</p>
5. Try to get into 22 with blank creds; Access Denied

6. Visit 80 and browse around; Found a @board.htb domain in the about me section

<p align="center">
<img src="./domain.png?raw=true">
</p>
7. Add that DNS to the hosts file to see if I can hop over to other domains
8. Performed some DNS enumuration with Ffuf – Fuzz Faster U Fool
9. Got a hit on crm.board.htb (FUZZ.board.htb)
<p align="center">
<img src="./fuzz.png?raw=true">
</p>
10. Replace the previous string value in the /etc/hosts file with the new crm.board.htb

11. Visit that site to find a Dolibarr CRM app; google default creds and was able to log in. Nothing interesting here though

<p align="center">
<img src="./crmapp.png?raw=true">
</p>

12. Found an exploit online for a reverse shell

13. Start a NC listener, ran the exploit after downloading, and was able to get in

14. Upgraded my shell session

15. Looked around online to see where this web app typically stores credentials

16. Found some mysql credentials for someone called dolibarrowner

17. Logged into mysql with those credentials and browsed the users table which had a ton of hashed passwords( Can try hashcat here if needed )

18. Ran cat /etc/passwd | grep bash to find a root and larissa user. Going to try to ssh back into this machine with the password found in the mysql directory

<p align="center">
<img src="./linuxdiscovery.png?raw=true">
</p>

19. Ran an switch user (su larissa) and put that password in; got into the user directory and grabbed the flag

20. To escalate my privleges I was having trouble figuring it out. Got some direction from some blogs that used a SUID explot

21. Ran find / -perm /u=s 2>/dev/null to find a potential SUID exploit

22. Started an FTP server on my kali machine and brought the file over to the session and executed it to get root


Detailed instructions followed in my own instance are in the 'AzureTrainingLab' folder.

## Credits

- Dolibarr Explot: https://github.com/nikn0laty/Exploit-for-Dolibarr-17.0.0-CVE-2023-30253
- Dolibarrr Details: https://wiki.dolibarr.org/index.php?title=Authentication,_SSO_and_SSL
- ffuf Fuzz DNS Enumeration: https://github.com/ffuf/ffuf
- MYSQL: https://www.geeksforgeeks.org/mysql-in-kali-linux-command-line/
- SUID Exploit: https://github.com/MaherAzzouzi/CVE-2022-37706-LPE-exploit
- Blog Post when I got stuck: https://medium.com/@RejuKole.com/boardlight-htb-walkthrough-by-reju-kole-69656ec11832


