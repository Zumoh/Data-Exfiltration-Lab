# Data-Exfiltration-Lab

This investigation focused on analyzing email-related network traffic to identify suspicious email communications that might indicate information leakage and to complete a challenge provided by LetsDefend.io.

#

<img width="624" alt="Screenshot 2025-01-18 at 9 32 13 AM" src="https://github.com/user-attachments/assets/fefd8e97-3b91-42b4-a9f8-c44a171104ec" />


## Objective

This investigation examines a PCAP file to identify the secret agent, their activities, and their communication network. By analyzing network traffic, the goal is to uncover the agent's identity, the tools or methods they are using, and the individuals or entities they are interacting with. This analysis aims to provide insights into the agent's operations and uncover any potential security risks.

### Skills Learned

- **Network Traffic Analysis**:
   - Proficient use of Wireshark to capture and analyze network traffic.
      - Understanding protocols like SMTP, TCP/IP, and DNS is crucial for identifying suspicious network activity. This skill is fundamental for identifying threats, such as unauthorized data exfiltration or malware communication, within network traffic.
- **Email Protocol Analysis**:
   - Analyzing email traffic using protocols like SMTP.
      - By analyzing email headers, content, and attachments, I learned how to spot signs of phishing or data exfiltration through email. It also helps in identifying email spoofing or unauthorized email access.
- **Base64 Encoding and Decoding**:
   - Using tools (like Base64 decoders) to decode and interpret Base64 encoded data.
      - Base64 encoding is often used to obscure data (e.g., credentials or attachments) in network traffic. Learning how to decode this allows me to identify hidden information, such as login credentials or malicious payloads.
- **Attachment Analysis and File Identification**:
   - Identifying, decoding, and analyzing email attachments (e.g., using CyberChef for Base64-decoding files).
      - This skill allows me to extract and analyze email attachments, such as documents or executables, to identify sensitive or malicious content. I learned how to decode attachments, investigate file names, and uncover potential exfiltrated data.
- **Hashing and File Integrity Verification**:
   - Using algorithms like MD5 and SHA256 to generate and compare file hashes.
      - This technique helps me verify file integrity and identify files involved in data exfiltration or malicious activities by comparing hashes to detect alterations or known threats.
- **Forensic Analysis of Network Data**:
   - Reconstructing network sessions (e.g., using Follow TCP Stream) to view the full conversation.
      - This skill lets me reconstruct fragmented network sessions to understand communications between hosts, particularly when investigating data breaches or unauthorized activity.
- **Use of CyberChef for Decoding Complex Data**:
   - Familiarity with CyberChef to perform a variety of encoding and decoding tasks (e.g., Base64, URL-decoding, XOR decoding, etc.).
- **Understanding Data Exfiltration and Security Breaches**:
   - Recognizing signs of data exfiltration through email traffic or other network protocols.
      - Being able to identify when data is being illicitly sent outside the organization, whether through email or other methods, is key for preventing breaches and securing sensitive information.

### Tools Used

- **Wireshark**: For analyzing the pcap file and capturing network traffic.
- **Base64** Decoder: For decoding Base64 encoded credentials.
- **CyberChef**: For decoding Base64 encoded email attachments.
- **MD5 Algorithm**: For calculating the MD5 hash of email attachments.

### Preparation

The file we need to investigate is located at _/root/Desktop/ChallengeFile_, and the name of the pcap file is _smtpchallenge.pcap_.

Note: The pcap file was sourced from publicly available resources.

To open Wireshark and begin investigating, simply double-click on the icon that looks like a blue shark fin.

#
<img width="624" alt="Screenshot 2025-01-18 at 8 34 11 AM" src="https://github.com/user-attachments/assets/889dfb8c-c278-47f9-b7c5-5ddd95bb6287" />

#
Once Wireshark is open, navigate to the directory where the pcap file is stored (_~/root/Desktop/ChallengeFile_). To do this:
1. Click on the **File** menu located in the top-left corner of your screen.
2. Select **Open** from the drop-down menu, or alternatively, press Ctrl+O on your keyboard.

#
<img width="632" alt="Screenshot 2025-01-18 at 8 36 49 AM" src="https://github.com/user-attachments/assets/2dfc2511-c0a0-41cf-9b2e-f566c9aef0e6" />

#

3. Navigate to the appropriate directory in the pop-up window.
4. Click on the pcap file (smtpchallenge.pcap) and click **Open**.

#

<img width="626" alt="Screenshot 2025-01-18 at 8 40 02 AM" src="https://github.com/user-attachments/assets/70294c96-326e-461a-8fdb-df6005fcd882" />

#

When investigating an email using Wireshark, it is essential to focus on the **Simple Mail Transfer Protocol (SMTP)**, as it is commonly used for sending and receiving email traffic. By doing so, you will be able to view all SMTP-related packets, which will allow you to examine the details of the email communications.

#

<img width="622" alt="Screenshot 2025-01-18 at 8 41 44 AM" src="https://github.com/user-attachments/assets/39bfc09b-6718-4381-9387-fc6a2777d3cd" />

#

Look for specific IP addresses, email addresses, and any payload data that might aid your investigation. In this case, we have identified two IP addresses. The Source IP Address (192[.]168[.]1[.]159) is the IP address of the sender's device (in this case, Ann) from which the authentication request is being made. The Destination IP Address (64[.]12[.]102[.]142) is the IP address of the mail server to which Ann is authenticating.

#

<img width="626" alt="Screenshot 2025-01-18 at 9 34 12 AM" src="https://github.com/user-attachments/assets/c4857808-5187-49f3-bd88-b7e15045d5de" />

#

1. Right-click on any of the packets (in this case, packet **#116**).
2. Scroll down to the **Follow** option in the drop-down menu.
3. Click on **TCP Stream** from the menu provided.

#

<img width="955" alt="Screenshot 2025-01-18 at 9 36 33 AM" src="https://github.com/user-attachments/assets/9a4f9dcb-4c7d-4cd0-aaff-b6afd20eeb2d" />

#

From the new pop-up window, we can gather most of our evidence in a single view. The "**Follow Stream**" method simplifies the investigation process by providing a comprehensive overview of the communication. This feature is invaluable for network analysis and security investigations because it allows you to reconstruct and examine the entire conversation between two endpoints, rather than analyzing individual packets separately.
#
By filtering out irrelevant packets, the "**Follow Stream**" method displays only the packets that are part of the specific conversation you are interested in. This enables you to see the full content of the communication, including any payload data, which is crucial for understanding what is being transmitted and identifying potential issues or threats.

### Question 1. What is the email address of Ann's secret boyfriend?  

#### Answer: _mistersecretx@aol[.]com_

#

Based on the conversation in the stream, it is reasonable to conclude that the email address mistersecretx@aol.com belongs to Ann's secret boyfriend. This email address can be identified from the "**RCPT TO**" or “**Recipient To**” line in the stream.

#

<img width="787" alt="Screenshot 2025-01-18 at 9 47 53 AM" src="https://github.com/user-attachments/assets/80baeb9e-a195-40c3-bfbe-2da1cd8b446b" />

#

<img width="785" alt="Screenshot 2025-01-18 at 9 49 01 AM" src="https://github.com/user-attachments/assets/9b98635b-3828-49b0-82e7-cf3842e2374e" />

#

### Question 2. What is Ann's email password? 

#### Answer: _558r00lz_

#

From the stream, we can see that authentication was successful, but the credentials are encoded in **Base 64**.

#

<img width="790" alt="Screenshot 2025-01-18 at 9 55 36 AM" src="https://github.com/user-attachments/assets/cc3f93ee-1ee9-4bf9-a27c-6402fce13b3e" />

#

To view the credentials in plain text, we need to decode them. For this, you can use a tool called **Base64**. Simply copy the login information, paste it into the **Base64** tool, and click on **Decode**. This will convert the encoded credentials into plain text.

#

<img width="578" alt="Screenshot 2025-01-18 at 9 57 37 AM" src="https://github.com/user-attachments/assets/c3a84929-522e-445a-901d-20f773e573d5" />

#

<img width="784" alt="Screenshot 2025-01-18 at 9 58 25 AM" src="https://github.com/user-attachments/assets/2520b557-1312-453f-b760-14e52cdec8c9" />

#

### Question 3. What is the name of the file that Ann sent to his secret lover? 

#### Answer: _secretrendezvous.docx_

#

Further investigation of the stream is necessary to determine whether Ann sent her secret lover a file, and if so, what the name of that file is. To do this, continue following the stream until you reach the **Content-Type** and **Content-Disposition** lines. These lines are crucial for identifying the type of content being transmitted and understanding how any attachments should be handled.

#

<img width="569" alt="Screenshot 2025-01-18 at 10 01 07 AM" src="https://github.com/user-attachments/assets/3a1e8597-8497-40fc-94aa-cd5d70b13d3f" />

#

<img width="786" alt="Screenshot 2025-01-18 at 10 02 51 AM" src="https://github.com/user-attachments/assets/823ebce5-831b-47b5-b8bf-35d456f2e74c" />

#

### Question 4. In what country will Ann meet with her secret lover? 

#### Answer: _Mexico_

#

To obtain this information, we need to read the document Ann attached in her email. Follow these steps:
1. Copy the entire encoded message found in the attachment.
2. Paste the encoded message into **CyberChef**.
3. Select "**From Base64**" as the recipe in CyberChef.
4. Once the entire encoded message is in the **Input section** of CyberChef, click on the **floppy disk icon** in the **Output section** to save the decoded message as a Word - document.

#

<img width="578" alt="Screenshot 2025-01-18 at 10 11 16 AM" src="https://github.com/user-attachments/assets/9c26512e-05a8-470a-a3bf-5c7fd342b5b0" />

#

5. Open the downloaded Word document to view the details of the attached file.

#

<img width="574" alt="Screenshot 2025-01-18 at 10 12 45 AM" src="https://github.com/user-attachments/assets/8a28c46b-3c15-45ee-91f5-d7060435f665" />

#

<img width="793" alt="Screenshot 2025-01-18 at 10 13 32 AM" src="https://github.com/user-attachments/assets/2e7623bd-06ca-4113-b366-6e7a9b41695a" />

#

### Question 5. What is the MD5 value of the attachment Ann sent?

#### Answer: _9e423e11db88f01bbff81172839e1923_

#

To get the MD5 (Message Digest Algorithm 5) hash, we want to open the CLI (Command Line Interface) also known as Terminal or Command prompt. The methods for doing this can vary depending on your operating system. For this exercise, I used **Git Bash**.

#### Windows 
press the **Windows key** to open the Start menu. Type **cmd** or **Command Prompt** in the search bar and select **Command Prompt** from the search results.

#### macOS
Open **Finder** and go to the **Applications** folder. From the Applications folder open the **Utilities** folder and select **Terminal**.

#### Linux
Open the **Applications** menu and search for **Terminal** and then select **Terminal**.

Once the Terminal is open, navigate to the directory where the file is saved. To verify you are in the correct directory, list its contents.

```cd Downloads``` - change to the Downloads directory.

```ls``` - lists the content(s) of the Downloads directoy.

#

<img width="562" alt="Screenshot 2025-01-18 at 10 19 07 AM" src="https://github.com/user-attachments/assets/c73fc760-eade-4590-a438-6c0f7ea843aa" />

#

<img width="564" alt="Screenshot 2025-01-18 at 10 20 15 AM" src="https://github.com/user-attachments/assets/28c956c9-cef7-4d0c-9688-d9c0f3556a5f" />

#

Run the following command from the directory where the file is stored: 

```md5sum "filename"```

- ```md5sum``` - Uses the MD5 hashing algorithm to generate a hash value.
- ```"filename"`` -     The name of the file for which you want to obtain the hash value.

The md5sum command calculates the MD5 hash of the specified file, which is a unique identifier (checksum) for the contents of the file. It can be used to verify the integrity of files, ensuring they haven’t been altered.

#

<img width="542" alt="Screenshot 2025-01-18 at 10 23 27 AM" src="https://github.com/user-attachments/assets/9d4127a5-ada1-4a12-9cc7-7b444e2a8757" />

#

Make sure to replace "**filename**" with the actual name of the downloaded file. For example, in this case, you would run: 

```md5 download1.docx```

#

<img width="567" alt="Screenshot 2025-01-18 at 10 25 10 AM" src="https://github.com/user-attachments/assets/193b4600-d285-4b60-8c2c-3741cc401bd4" />

#

The terminal will calculate the MD5 hash of the file (download1.docx) and output the MD5 hash value followed by the file name.

#

<img width="569" alt="Screenshot 2025-01-18 at 10 25 59 AM" src="https://github.com/user-attachments/assets/5655e45e-a0fa-44ba-8bb2-f0f13870fef7" />

#

<img width="782" alt="Screenshot 2025-01-18 at 10 26 36 AM" src="https://github.com/user-attachments/assets/5316682e-d474-41c0-9ce4-8ffe46d75a7b" />













