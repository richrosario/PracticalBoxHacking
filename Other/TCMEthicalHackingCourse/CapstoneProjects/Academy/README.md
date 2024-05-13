#  Dev Walkthrough

- Installed the machine from the Google Drive link
- Run sudo nmap -p- -A -T4 192.168.0.xxx and founds ports open (12,22,80)

- Default apache web page at the ip: http://192.168.0.xxx/
    - Very revealing
    - tells us a lot
    - maybe php
- First we start at the note.txt file that’s in there  at port 21
    - Results of ftp
    - We used default logins
    - We grab the file and put in our machine
    - We found a hash
        - See it using hash identifier
        - We are going to crash the md5 cash using a word file in the form of rockyou.txt and running a hashcat
            - Note that usually we would not urn this in cpu(vm) but in the base host off GPU as hashes usually do
        - SUCCESS
            - We cracked the hash found in that file and now we have a login/password. But what can we do with this? where does it go? They mention ‘academy’ so perhaps its a new tool or site
        - Directory Busting?
            - One way is running **dirb** on the target host
                - multileveled which takes longer
            - **ffuf** is a faster one
                - 1 lvl deep so quicker
            - Found the /academy directory and hit to find the new student portal
                - Used logins found before
                - Found an attachment option in the student picture we can attack
                    - Could also hit sql injections on those fields
            - We will try a **php reverse shell**
                - Googled one and downloaded it
                - set up a net cat on the source server
                - Uploaded that php file up
                - it worked but we are not an elevated user
                    - BUT we are in the machine when you upload a picture! reverse shell success
            - Now we need to do **privelaged escalation**
                - **LinPEAS**: Hunts for privelaged escalation
                - We grab the file from github and host a web server using python at he source
                - We go from the target machine(we got in via reverse shell) and while in the machine  we **wget** into the web server hosted at the source  and grab the [linepeas.sh](http://linepeas.sh) file so we can run it in the target  server
                    - Findings
                        - **Top Findings**
                            - We get a password
                                - We went into this file and found a ton of database information
                                - cat etc/passwd -> admin 
                                - We ssh in with that password now that we know its an admin.
                                - Usually we would LinPEAS in here again
                            - *** * * * /home/grimmie/backup.sh**
                                - **Once we ssh in** now we’re going to look for this directory
                                    - We found what appears to be performing some sort of backup but it’s not crontab(**a linux script scheduler)**
                                    - **PSPY**: Monitor Linux processes without root privileges’
                                        - We move this tool into our target form source using wget into the transfers folder that’s acting as an ftp because of that web server we have running
                                            - We can now see all the processes running on the machine
                                                - We found a running backup process triggering that [backup.sh](http://backup.sh) file from earlier but as root. So we are going to place a reverse shell bash script into the backup file and its going to run it, not knowing its running the backup + reverse shell
                                                    - This should reverse shell us in as root