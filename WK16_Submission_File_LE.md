## Week 16 Homework Subission File: Penetration Testing 1

#### Step 1: Google Dorking

Altoro Mutual wants to ensure that private information that is unavailable on their public website cannot be found by searching the web. 

- Using Google, can you identify who the Chief Executive Officer?
  - Karl Fitzgerald
  ![image](https://user-images.githubusercontent.com/93744925/161839236-60d93753-db6f-4bf1-acf3-dabba6751ef7.png)

- How can this information be helpful to an attacker?
  - This information can be usefule to an attacker dur to being able to perform social engineering attacks, ie., email phishing, directly to the CEO and other executives.

#### Step 2: DNS and Domain Discovery

- Enter the IP address for `demo.testfire.net` into Domain Dossier and answer the following questions based on the results:

  1. Where is the company located? 
    Sunnyvale, CA

  2. What is the NetRange IP address? 
    65.61.137.64 - 65.61.137.127

![image](https://user-images.githubusercontent.com/93744925/161836947-c84d2689-5bca-4f45-9f85-1482064f928c.png)

  3. What is the company they use to store their infrastructure? 
  Rackspace Backbone Engineering
  
  4. What is the IP address of the DNS server? 
  65.61.137.117

#### Step 3: Shodan

  - What open ports and running services did Shodan find? 
   -Ports: 80, 443, 8080 https://www.shodan.io/host/65.61.137.117 
   
![image](https://user-images.githubusercontent.com/93744925/161837776-4d770163-e72c-40b6-8654-2b142483f771.png)

#### Step 4: Recon-ng

- Install the Recon module `xssed`. Run the commands:
     - marketplace search xssed
     - marketplace install recon/domains-vulnerabilities/xssed
     - modules load recon/domains/vulnerabilities/xssed
   
  ![image](https://user-images.githubusercontent.com/93744925/161839474-02e0da8c-0c8f-48f7-a4a2-2df5935084b5.png)

- Set the source to `demo.testfire.net`. 
  - Run the command: info
  - Run the command: options set SOURCE demo.testfire.net to set the source
![image](https://user-images.githubusercontent.com/93744925/161840132-ff09c627-c225-4db4-b2c8-d5d344b0b371.png)

- Run the module.
  - Run the command: run  
![image](https://user-images.githubusercontent.com/93744925/161840435-9f31013b-f8bf-4c84-bd19-07a2b7d64ad6.png)

Is Altoro Mutual vulnerable to XSS? YES, there is 1 total vulnerability found.

### Step 5: Zenmap

Your client has asked that you help identify any vulnerabilities with their file-sharing server. Using the Metasploitable machine to act as your client's server, complete the following:

- Use Zenmap to run a service scan against the Metasploitable machine.
  - namp -T4 -F 192.168.0.10
   
  
  - Bonus command to output results into a new text file named `zenmapscan.txt`. 
    - namp -T4 -F -oN zenmapscan.txt 192.168.0.10 

    ![image](https://user-images.githubusercontent.com/93744925/161841485-de449cd3-c308-4da3-a1e8-15dfc80bf0e8.png)

- Zenmap vulnerability script command:
  - namp -T4 -F --script ftp-vsftpd-backdoor,smb-enum-shares 192.168.0.10
  ![image](https://user-images.githubusercontent.com/93744925/161841335-d7416df0-4738-4ea3-ace9-a212518e7be9.png)

  ![image](https://user-images.githubusercontent.com/93744925/161841234-976e4381-4551-420d-bc33-859dd0607dee.png)


- Once you have identified this vulnerability, answer the following questions for your client:
  1. What is the vulnerability? CVE-2011-2523:Zenmap was able to enumerate the vulnerable service running on port 21.  
  2. Why is it dangerous? The vsftpd v2.3.4 is vulnerable to a backdoor command execution, whcih present a threat to running this particular version of software. Successful execution of this vulnerability results in opening the backdoor port 6200 of the system and running as root.
  4. What are your recommendations for the client to protect their server? I recommmend constant monitoring and updating with the patch for vsfptd 2.3.4.  The vsFPTD 2.3.4 patch was released on July 3, 2011.
  ![image](https://user-images.githubusercontent.com/93744925/161841682-11e3d049-c438-461f-8109-76c263015b2b.png)

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.  

