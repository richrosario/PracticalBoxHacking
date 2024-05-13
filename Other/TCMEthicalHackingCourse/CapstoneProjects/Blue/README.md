#  Blue Walkthrough

1. Installed the machine from the Google Drive link
2. Run sudo nmap -p- -A -T4 192.168.0.161
3. Found the following -> https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/
4. Scan again with auxilary modules via Metasploit and run with the updated variables
5. We gain a shell via the Metasploit payload

