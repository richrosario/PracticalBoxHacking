# Cap

<p align="center">
<img src="./pwned.png?raw=true">
</p>

- Link: https://app.hackthebox.com/machines/Cap
- Level: Easy

## Steps taken

These are a rough order of operations for the work done to pwn the Cap on Hack The Box; A machine labled as an 'easy' box. 

- Ran an NMAP scan to see 3 open ports(21,22,80)
<p align="center">
<img src="./nmapp.png?raw=true">
</p>
- Port 80 has some sort of security snapshot dashboard that I can navigate as a user called 'nathan'
<p align="center">
<img src="./dashboard.png?raw=true">
</p>
- I am able to query more than one page or report by just switching the id in the url
- Went one by one descending from 9 until I found some interesting packets in 0
- I'm able to see clear text FTP credentials
<p align="center">
<img src="./pcap.png?raw=true">
</p>
- They work with FTP and with nathan@SSH and I'm able to get the user flag
- The default way to escalate is always linepeas.sh
- I grab the linpeas.sh file using wget to my attack machine and then setup an HTTP server to wget the file from the target machine I'm logged into via SSH
- I modify the file's permissions and run linpeas to find /usr/bin/python3.8 is is vulnerable and able to be ran
<p align="center">
<img src="./linpeas.png?raw=true">
</p>
- Looking online I find a way to use a python instance to change the UID using the OS library and spawn a bash session ( /usr/bin/python3 -c 'import os; os.setuid(0); os.system("/bin/sh")' )
- I cat the root library and find the root flag



## Credits

- https://github.com/peass-ng/PEASS-ng/tree/master/linPEAS
- https://steflan-security.com/linux-privilege-escalation-exploiting-capabilities/

