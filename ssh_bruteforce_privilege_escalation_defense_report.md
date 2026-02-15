SSH Attack Simulation and Defence Escalation on Victimbuntu (Defender POV)
1. Executive Report
   On Feb 6, 2026, a simulated attack against a Linux Endpoints (Victimbuntu - 192.168.18.152). The attempt started with reconnaissance on device within the network and scanning of open ports of the victim. The attack also involving SSH brute-force authentication attempts, stealing credentials, privilege escalation within the endpoint, and unauthorized account creation.
   The Wazuh succesfully detected the stages of the attack. The incident was classified as High due to affirmed privilege escalation and persistence establishment.

3. Environment:
- Wazuh Manager: Ubuntu Server 24.04
- Wazuh Agent: Ubuntu 20.04 LTS
- Attacker: Kali Linux
- Network Config: Bridged
- Monitoring: File Integrity, Sys log monitoring enabled

Detection Analysis:
3.1 Recoonnaissance Phase:
- Multiple attempts to connect is viewed. The pattern is consistent with network scanning behavior. There's also "nmap" in the rule.description.
- Potential MITRE.ATTACK.ID: T1046
3.2 Brute Force Attempt
- Wazuh detected multiple SSH login attempts that stated "Authentication Failed" in the rule.description
- Repeated credentials attempt errors from single IP (.40)
- The potential attack is Brute Force Attempt, mapped to: T1110 and T1078
- Severety level: Medium. Flagged: True
3.3 Compromised
Successful SSH login using stolen credentials was detected.
Log Evidence (auth.log):
"Accepted password for victim from <192.168.18.40>
Severety level: High. Flagged: True
3.4 Privilege Escalation
Attacker successfully escalate privilige, becoming a root. Backed with evidence of sudo execution logs and root shell access observed. This attack mapped to: T1548 - Abuse Elevation Control Mechanism. Severity High and Flagged as true.
3.5 Persistence Mechanism
Attacker created a new privileged account:
- backdooruser
- Added to sudo group
Detected via:
- useradd logs
- usermod logs
Mapped to: T1098 – Account Manipulation and T1078 – Valid Accounts
Severity is Critical and Flagged true, reason:
Unauthorized creation of privileged account indicates full system compromise and long-term persistence.

