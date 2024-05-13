# AdventOfCyber 2023
Notes related to the day-by-day follow along to TryHackMe's Advent of Cyber 2023 challenges

*https://tryhackme.com/r/christmas*

- **Day1**
    - **Security Frameworks**
        - NIST
        - ISO 27000
        - MITRE ATT&CK
        - Cyber Kill Chain
- **Day2**
    - **All about Log Files**
        - Common Log Locatiojn
            - Windows : Event Viewer
            - Linux: var/log
    - GREP: Command dedicated to find a provided text in a file
        - -r Recursive searches in the entire working directory
        - -e Searches using REGEX
- **Day3**
    - **OSINT** is gathering and analyzing publicly available data for intelligence purposes, which includes information collected from the internet, mass media, specialist journals and research, photos, and geospatial information.
    - **Google Dorking** involves using specialist search terms and advanced search operators to find results that are not usually displayed using regular search terms.
    - **WHOIS** database stores public domain information such as registrant (domain owner), administrative, billing and technical contacts in a centralized database
    - Github is a vulnerable site if searched probably
- **Day4**
    - **Scanning**
        - **Passive Scanning**: This method involves scanning a network without directly interacting with the target device (server, computer etc.). Passive scanning is usually carried out through packet capture and analysis tools like Wireshark; however, this technique only provides basic asset information like OS version, network protocol etc., against the target.
        - **Active Scanning**: Active scanning is a scanning method whereby you scan individual endpoints in an IT network to retrieve more detailed information.
        - Other Types Of Scans:
            - Network
                - NMAP
                    - sS: Live hosts and associated ports
                    - sN: Live hosts no ports
                    - -O: OS’s running
                    - sV: List of running services on a host
            - Port
                - Filtered ports indicate it’s open but not accepting connections
            - **Nikto**: Nikto is open-source software that allows scanning websites for vulnerabilities. It enables looking for subdomains, outdated servers, debug messages etc., on a website. You can access it on the AttackBox by typing
- **Day5**
    - Brute Forcing
        - Connecting to a remote computer
            - SSH
            - RDP
        - Ways of attacking
            - **Shoulder Surfing**
            - **Password Guessing**
            - **Dictionary Attack**
            - **Brute Force Attack**
- **Day6**
    - Email Analysis: We use a hash value found in an attachment and reverse search it across the web in the tools below
        - Two main concerns with email analysis
            - **Security issues:** Identifying suspicious/abnormal/malicious patterns in emails.
            - **Performance issues:** Identifying delivery and delay issues in emails
        - Two types of email risks
            - Social Engineering
            - Phishing
    - Emails can be opened in a text editor and analyzed further to grab information
        - **EMLANALYZER** is a free command line tool
        - Some free tools to analyze suspicious emails amount other things
        
        | VirusTotal | A service that provides a cloud-based detection toolset and sandbox environment. |
        | --- | --- |
        | InQuest | A service provides network and file analysis by using threat analytics. |
        | IPinfo.io | A service that provides detailed information about an IP address by focusing on geolocation data and service provider. |
        | Talos Reputation | An IP reputation check service is provided by Cisco Talos. |
        | Urlscan.io | A service that analyses websites by simulating regular user behaviour. |
        | Browserling | A browser sandbox is used to test suspicious/malicious links. |
        | Wannabrowser | A browser sandbox is used to test suspicious/malicious links. |
- **Day7**
    - CyberChef is a web-based application - used to slice, dice, encode, decode, parse and analyze data or files.
        - We encode the file found in the email yesteday
        - CyberChef: https://gchq.github.io/CyberChef/
- **Day8**
    - BlockChain: A blockchain is a distributed database or ledger that is shared among the nodes of a computer network. As a database, a blockchain stores information electronically in digital format.
    - Smart Contracts: DeFi applications facilitate currency exchange between entities; a smart contract defines the details of the exchange. A **smart contract** is a program stored on a blockchain that runs when pre-determined conditions are met.
        - Very similar to any program created from a scripting language
    - Most smart contract vulnerabilities arise due to logic issues or poor exception handling. Most vulnerabilities arise in functions when conditions are insecurely implemented through the previously mentioned issues.
    - https://remix.ethereum.org/#optimize=false&runs=200&evmVersion=null&version=soljson-v0.8.7+commit.e28d00a7.js
- **Day9**
    - New web app deployed on Docker
    - Using Metasploit to hack
    - **Pivoting:** Once an attacker gains initial entry into a system, the compromised machine can be used to send additional web traffic through - allowing previously inaccessible machines to be reached in the network.
- **Day10**
    - Hacking a game
        - We basically hack a game by altering memory as that’s where game data is stored
            - We are able to find out guard random numbers and increase HP e.g.
        - The tool used is the Chrome friendly **CETUS** tool
- **Day11**
    - Memory Forensics
        - Memory forensics (sometimes referred to as memory analysis) refers to the analysis of volatile data in a computer’s memory dump. Information security professionals conduct memory forensics to investigate and identify attacks or malicious behaviors that do not leave easily detectable tracks on hard drive data.
        - **Volatility** is an open-source memory forensics toolkit written in **Python**. Volatility allows us to analyze memory dumps taken from Windows, Linux and Mac OS devices and is an extremely popular tool in memory forensics.
            - https://volatility3.readthedocs.io/en/latest/volatility3.plugins.html
            - We use a variety of plug ins that look into the machine in detail
- **Day12**
    - Malware Analysis
        - **Detect It Easy (DIE):** This tool provides information about the file, such as its architecture, significant headers, packer used, and strings
        - **CAPA**: Detects capabilities in executable files. May it be for the installation of a service, invocation of network connections, registry modifications and such.
        - **UPX:** Unpacks malware. Packing malware is a common technique used by malware developers to compress, obfuscate or encrypt the binary. With this, contents such as significant strings and headers will not be immediately visible to Static Analysis Tools.
    - As discussed above, malware tends to do the following; **Registry Modification, File Modification and Network Connections**
- **We have covered several topics on this task about Malware Analysis. For a quick summary, we have learned the following:**
    - Key behaviors of malware aid in having an overview of what to expect in examining malware samples.
    - The precautions needed to consider while handling malware samples and the importance of sandboxes.
    - Conduct a Static Analysis and profile the nature of the binary without executing it.
    - Perform a manual Dynamic Analysis and observe the interactions of the malware sample in the **Registry**, **File System** and **Network**.
- **Day13**
    - **Packet Analysis**
- **Day14**
    - Web Apps
        - https://owasp.org/Top10/
        - **IDOR** refers to the situation where a user can manipulate the input to bypass authorization due to poor access control. IDOR was the fourth on the OWASP Top 10 list in 2013 before it was published under Broken Access Control in 2017. To learn more about IDOR, consider the following examples.
        - Think changing ID’s of pages or images(UID)
- **Day15**
    - Secure Coding
        - Force our way into a file upload vulnerability
        - By starting a reverse shell we upload a malicious file and then when someone uploads a file we gain root
- **Day16**
    - SQL Injections
- **Day 17**
    - HTML5 and Regex filtering
- **Day18**
    - Threat Hunting and Detection
    - **Sigma**: Sigma is an open-source generic signature language developed by Florian Roth & Thomas Patzke to describe log events in a structured format.
        - https://www.google.com/search?q=aoc+sigma+hunting&rlz=1C1GCEA_enUS999US999&oq=aoc+sigma+hunting&aqs=chrome..69i57j0i30i546l2.1673j0j7&sourceid=chrome&ie=UTF-8
- **Day19**
    - Hardware Hacking
- **Day20**
    - Firmware hacking
- **Day21**
    - MQTT Mosquito: https://en.kali.tools/all/?tool=855
- **Day 22**
    - Attack surface reduciton and vectors