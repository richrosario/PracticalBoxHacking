# Course Notes and Misc.

- Installed an instance of Kali Linux on VMware Workstation 17 Player
- Updated user permissions
- Installed pimpmykali -> https://github.com/Dewalt-arch/pimpmykali
- Installed Wiresahrk -> https://www.wireshark.org/
- Installed GEDIT -> https://help.gnome.org/users/gedit/stable/

### Scripting with BASH

- **BASH**: Unix shell and command language
- IP Sweeper
    - We’re building a ping sweeper for a network and looking for used IP’s in a given range
    - **mousepad [ipsweep.sh](http://ipsweep.sh/)**
        - Brings you into a bash text editor
        - /home/kali/Documents is the project directory
    - **nmap** is a tool that allows us to do port scanning
        - One Liner with a list of IP’s created earlier
        - for ip in $(cat ips.txt); do **nmap** $ip; done
- **Utilize sockets to connect one node to another node**
    - [s.py](http://s.py) file in the socket folder
    - We basically write a script that shoots a connection to an open port on a node
        - To open a port on a node we use net cat:
            - nc -nvlp 777
        - Then we run the python script and you can see the connection come in

### 5 stages of ethical hacking 

1. Reconnaissance(Information Gathering)
    1. Active: Running port scanners e.g.
    2. Passive: Googling the clients name e.g. / referred to as passive recon 
2. Scanning and Enumeration
    1. nmap, Nessus, Nikto
3. Gaining Access(Exploitation)
4. Maintaining Access
5. Covering Tracks
    1. Then you start again; full circle

