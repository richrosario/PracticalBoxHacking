#  Butler Walkthrough

1. Installed the machine from the Google Drive link
2. Run sudo nmap -p- -A -T4 to find a couple ports open including a login page for Jenkings
3. Tried Brute force via Burpsuite and FoxyProxy ; Did not work.
4. Using a commonly known jenkins default credential we run an interecept and get a return on some cookies.
5. Now we will look for some sort of remote code execution/reverse shell on google
	- We start an ncat on the target machine
	- We run the remote code/reverse shell we found inside the Jenkins default script console and we get in via our source machine as a low level user
        - Now we know its running windows so we can look for exploits on that build as an option but we wont
6. On the source server we start up an ftp server and run a window winpeas
	- winpeas.exe is a script that will search for all possible paths to escalate privileges on Windows hosts
7. We found a privelaged escalation running from admin  that will allow us to get system on this machine  because the systme is looking for anything called WISE ( no quotes or space ) and executing it
8. So what we’ll do is create a reverse shell script and place it on the ftp and rename it to wise. Then we need the service itself to run the exe!!!
    	- We first need to stop the service and re run it so the admin takes over the service
    	- When we restart the service we are in as admin
	