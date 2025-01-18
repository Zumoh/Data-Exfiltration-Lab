# Data-Exfiltration-Lab

This investigation analyzes a PCAP file to identify a secret agent's activities, communication patterns, and potential data exfiltration methods. The focus is on uncovering hidden operations and understanding how sensitive data may be transferred or compromised within the network.

## Objective

This investigation examines a PCAP file to identify the secret agent, their activities, and their communication network. By analyzing network traffic, the goal is to uncover the agent's identity, the tools or methods they are using, and the individuals or entities they are interacting with. This analysis aims to provide insights into the agent's operations and uncover any potential security risks.

### Skills Learned

- Threat Identification:
   - Recognizing signs of smishing, such as unsolicited messages, urgency, poor grammar, and suspicious links.
- Analytical Skills:
   - Using tools like VirusTotal, Cisco Talos, AnyRun, WHOIS, and URLscan.io to analyze and interpret data.
   - Understanding and correlating information across multiple cybersecurity tools.
- Dynamic Malware Analysis:
   - Running and observing the behavior of suspicious links and files in a sandbox environment (AnyRun).
   - Interpreting reports on activities, network connections, file modifications, and processes.
- IP Reputation and Domain Analysis:
   - Checking the reputation of IP addresses and domains using services like Cisco Talos and WHOIS.
   - Understanding how domain registration and timing can indicate malicious intent.
- Forensic Reporting:
   - Documenting findings clearly and concisely.
   - Creating detailed reports on analysis and conclusions.
- Preventive Measures:
   - Learning how to identify and avoid potential phishing threats.
   - Advising on actions to take when encountering suspicious messages or links.

### Tools Used

- VirusTotal: To scan link found in the text message.
- Cisco Talos: To evaluate the safety and reputation of IP addresses associated with the url.
- AnyRun: To Execute and analyze the links in a controlled environment to observe its behavior.
- Whois: To acertain ownership details of the domain found in the link.
- URLscan.io: To analyzes the URL to identify its behavior and potential risks.

## Investigation

In the ever-evolving landscape of cybersecurity, threats can come in many forms. Recently, I encountered a smishing text—a text-based phishing attempt designed to deceive users into clicking malicious links. Through a meticulous investigation, I uncovered the deceptive tactics employed by the threat actors and the tools they used to mask their malicious intent. Here’s a detailed account of the analysis and findings.
