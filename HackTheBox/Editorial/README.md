# Editorial

<p align="center">
<img src="./dash.png?raw=true">
</p>

- Link: https://app.hackthebox.com/machines/Editorial
- Level: Easy

## Steps taken

These are a rough order of operations for the work done to pwn the Editorialmachine on Hack The Box; A machine labled as an 'easy' box. Tough box and I could not get root myself.

- Start the box
- Run a ping check on the device 
- Run an NMAP Scan to see open ports
<p align="center">
<img src="./nmap.png?raw=true">
</p>
- Find that 80 and 22 are open
- Add the site to /etc/hosts
- It is some sort of book signup/publishing box
- Found a domain, a way to write new books to the server, and a method of uploading files with right away calls out SSRF
<p align="center">
<img src="./input.png?raw=true">
</p>
- Using BURPSUITE and intercepting the preview function to localhost we can see its pointing to a local directory
<p align="center">
<img src="./burp.png?raw=true">
</p>
- Put that directory into our server and we get the image we previewed ourselves
<p align="center">
<img src="./imagepreview.png?raw=true">
</p>
- Now that we know we can snoop around we can try a port attack and see if and ports give a different response. 0 > 65535
- 5000 has a slghtly shorter response length
<p align="center">
<img src="./requestsize.png?raw=true">
</p>
- We send that port a request from burp and download the file it responds with using wget
<p align="center">
<img src="./burp2.png?raw=true">
</p>
- It's some sort of API endpoint
- Try the various API calls via burp and one actually had a file with creds; Seemed like some sort of ' thanks for joining' type of response
<p align="center">
<img src="./apicall.png?raw=true">
</p>
- Use SSH with those creds are we got the user flag
- Next in the app folder I see it's a git repo. 
- Used git log and git show to see if they left anything around in those commits
- Found credentials to prod but I got stuck here
- There are resources online that show how they got to root so I followed them but previous step was as far as I got


## Credits

- ffuf Fuzz DNS Enumeration: https://github.com/ffuf/ffuf
- https://portswigger.net/web-security/ssrf
- https://security.snyk.io/package/pip/gitpython

