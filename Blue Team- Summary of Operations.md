# Blue Team: Summary of Operations
## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

## Network Topology
The following machines were identified on the network:

- Windows 10 Hypervisor
    - Operating System: Windows 10 Pro
    - Purpose: Hosts VMs with Hyper-V Manager
    - Private IP Address: 192.168.1.1
    - Public IP Address: 172.18.76.177
- Kali 
    - Operating System: Kali Linux
    - Purpose: Pen testing machine
    - IP Address: 192.168.1.90/24
- Target 1
    - Operating System: Debian Linux
    - Purpose: 1st target of attack
    - IP Address: 192.168.1.110/24
- Target 2
    - Operating System: Debian Linux
    - Purpose: 2nd target of attack
    - IP Address: 192.168.1.115/24
- ELK
    - Operating System: Ubuntu Linux
    - Purpose: SIEM/IDS - ELK Stack
    - IP Address: 192.168.1.100/24
- Capstone
    - Operating System: Ubuntu Linux
    - Purpose: Alert testing
    - IP Address: 192.168.1.105/24

## Description of Targets
The target of this attack was: `Target 1` (`192.168.1.110`).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

- Excessive HTTP Errors
- HTTP Request Size Monitor
- CPU Usage Monitor

## Monitoring the Targets
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

### Excessive HTTP Errors
Alert 1 is implemented as follows:

- **Metric:** http.response.status_code > 400
- **Threshold:** 5 in the last 5 minutes.
- **Vulnerability Mitigated:** This alert will notify the security operation analysts of a potential attack and allow them to act according to the incident response plan. This may include blocking the IP or changing authorisation credentials. 
- **Reliability:** Few false positives | High reliability.

### HTTP Request Size Monitor
Alert 2 is implemented as follows:

- **Metric:** http.request.bytes
- **Threshold:** 3500 in the last 1 minute.
- **Vulnerability Mitigated:** Since this will notify when the http request size is large enough, this can help alert if a DDoS attack is in progress.
- **Reliability:** Few false positives | High reliability.

### CPU Usage Monitor
Alert 3 is implemented as follows:

- **Metric:** system.process.cpu.total.pct
- **Threshold:** 0.5 in the last 5 minutes.
- **Vulnerability Mitigated:** This alert will trigger when CPU usage rises above 50%.
- **Reliability:** May trigger some false positives | Low reliability, since the CPU usage is not an indicator of attack, it can trigger when a resource-intensive process is running.




## *Will attempt if there is time*
TODO Note: Explain at least 3 alerts. Add more if time allows.
Suggestions for Going Further (Optional)
TODO:
Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain how to implement each patch.
The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
Vulnerability 1
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day
Vulnerability 2
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day
Vulnerability 3
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day

