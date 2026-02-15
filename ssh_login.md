SSH Attack Simulation and Defence Escalation on Victimbuntu (Attacker POV)

Environment:
- Wazuh Manager: Ubuntu Server 24.04
- Wazuh Agent: Ubuntu 20.04 LTS
- Attacker: Kali Linux
- Network Config: Bridged
- Monitoring: File Integrity, Sys log monitoring enabled

Attack Simulation:
1. An attacker connect to network area with root ip 192.168.18.0 at 20:30:44.
2. The attacker try to perform Reconnaisance to indentify target ip within the network. Attacker use nmap with -sS (stealth half-open scan) and -O (detect all operation system within network) configuration. The attacker notice there's 2 Linux's OS stated with ip address of -.152 and -.158. Attacker noticed that .152 have 5 open ports (/21 ftp, /22 ssh, /80 http, etc).
3. Attacker is conficed that the victim server ip is .152. To boost their confidence, they try to scan again, this time the target is .152.
4. After confincing scan, attacker plan the best attacking scenario. The attacker choose brute SSH login attempt because the port /22 is open.
5. The attacker begin to attack victim using msfconsole (metasploit). Inside they're using auxiliary/scanner/ssh_login module to brute and scan victim username and password to gain access. Attacker set file named "smallpass.txt" containing 4 possible passwords and another file named "users.txt" containing 3 possible usernames. The attacker set RHOST and USER/PASS_FILE using their respective .txt. After a short attack, attacker has the credentials of the user, that is victim@password123 and user@password123.
6. The attacker logged in using ssh attempt and input the victim credentials (this time is victim@password123). A successful attempt has been done. Now attacker has the credentials info and saving it into victim.txt.
7. After gaining access, attacker access the info of the victim and claiming root of the server. After gaining root, the attacker now creating backdoor access. Using credentials of backdooruser@password123, the attacker succesfully created a backdoor access for futher unauthorized login.

Attack rundown:
20:30:44 - Accessing victim root network
20:44:00 - Scanning devices inside of the network
20:47:22 - Scanning open ports of the victim
21:01:08 - Exploit SSH login credentials
21:09:00 - SSH login to victim server
         - Exploitation and Creating backdoor user
