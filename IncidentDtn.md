# Incident Detection & Response Simulation

## Overview

This project simulates an Incident Detection & Response process using Wazuh, a Security Information and Event Management (SIEM) tool, and the Elastic Stack (Elasticsearch, Logstash, Kibana). The simulation focuses on detecting security incidents such as brute force attacks, unauthorized logins, and malware infections. Alerts are triggered based on suspicious activities, and response actions are simulated to investigate and mitigate potential threats.

## Project Setup

This project uses the following components:
- **Wazuh**: SIEM for monitoring system and network logs.
- **Elastic Stack (Elasticsearch, Logstash, Kibana)**: For data aggregation, alert visualization, and analysis.
- **Linux Server (Ubuntu)**: The environment used to set up the system.

### Prerequisites

- Ubuntu 20.04 or higher.
- Internet connection for installing packages.
- Root or sudo privileges for installing and configuring the necessary tools.

### Installation

Clone this repository to your server and run the following scripts.

#### 1. Install Wazuh Manager

```bash
chmod +x install_wazuh_manager.sh
./install_wazuh_manager.sh
This script installs the Wazuh manager on your server, enabling you to collect and process security logs.

2. Install Wazuh Agent
bash
Copy
Edit
chmod +x install_wazuh_agent.sh
./install_wazuh_agent.sh
This script installs and configures the Wazuh agent on a target machine to send logs to the Wazuh manager.

3. Install Elastic Stack (Elasticsearch, Logstash, Kibana)
bash
Copy
Edit
chmod +x install_elastic_stack.sh
./install_elastic_stack.sh
This script installs the Elastic Stack on your server, which integrates with Wazuh to visualize and analyze security alerts.

Configure Wazuh for Incident Detection
1. Brute Force Attack Detection
Wazuh is configured to monitor authentication logs for brute force attempts. The detection rule is set up in /var/ossec/etc/ossec.conf.

2. Unauthorized Login Detection
Wazuh monitors failed login attempts and unauthorized access in /var/log/auth.log. Alerts are generated when suspicious login activities occur.

3. Malware Infection Detection
Wazuh detects unusual file activities, such as file creation or execution of suspicious files, as indicators of malware infections.

Simulate Security Incidents
Simulate Brute Force Attack: Use hydra to simulate brute-force login attempts.

bash
Copy
Edit
hydra -l root -P /usr/share/wordlists/rockyou.txt ssh://<target_ip>
Simulate Unauthorized Login: Attempt SSH login with incorrect credentials.

bash
Copy
Edit
ssh root@<target_ip>
Simulate Malware Infection: Create and execute a suspicious file.

bash
Copy
Edit
touch /tmp/suspicious_file
chmod +x /tmp/suspicious_file
./tmp/suspicious_file
View Alerts in Kibana
Once the incidents are simulated, view the alerts in Kibana:

Access Kibana through http://<kibana_ip>:5601.

Go to Discover to view logs and security alerts generated by Wazuh.

Automate Response with Wazuh Active Responses
Wazuh can be configured to take automated actions (e.g., block IPs involved in attacks). An example configuration for blocking an IP after a brute force attack can be found in the ossec.conf file under the <active-response> section.

Results
Brute Force Attack: Alerts are generated when multiple failed login attempts are detected.

Unauthorized Login: Alerts are triggered for suspicious login activities.

Malware Infection: Alerts are created when suspicious files are executed.

Conclusion
This project demonstrates how to implement an incident detection and response process in a Security Operations Center (SOC) environment using Wazuh and Elastic Stack. It provides a basic framework for detecting, investigating, and responding to cyber threats in real time.

Future Improvements
Integrate with additional threat intelligence feeds for enhanced detection capabilities.

Automate responses based on alert severity (e.g., automatic isolation of infected machines).

Extend the setup to include cloud environment monitoring (e.g., AWS, Azure).
