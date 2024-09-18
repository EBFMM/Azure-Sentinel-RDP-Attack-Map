# Azure Sentinel RDP Attack Map

![image](https://github.com/user-attachments/assets/81d9719e-a74d-4fda-bfc0-ffd59ddc8f07)

<img src="https://github.com/user-attachments/assets/81d9719e-a74d-4fda-bfc0-ffd59ddc8f07" width="700"/>


## Objective

The objective of this penetration test demo is to demonstrate the exploitation of a SMB (Server Message Block) vulnerability on the target system. The focus is to identify and exploit a weaknesses in this service, gaining unauthorized access, and successfully exfiltrating sensitive data. This demo highlights the critical risks associated with improperly secured network services and underscores the importance of robust security measures in protecting sensitive information from potential threats.

### Skills Learned

- Advanced understanding of network service vulnerabilities and their impact on system security.
- Proficiency in utilizing Metasploit for exploiting SMB vulnerabilities and gaining system access.
- Ability to execute comprehensive penetration tests and simulate real-world attacks on network services.
- Enhanced skills in assessing network services and identifying critical security vulnerabilities.

### Tools Used

- OpenVAS to provide a detailed report on potential threats and known vulnerabilities within the network.
- Metasploit framework, utilized for conducting penetration testing, by running an exploit module against the target machine to simulate a real-world attack.
- John the Ripper tool for password cracking.


## Steps

### Create Virtual Machine


### Allow All Traffic Through Firewall

The specific vulnerability identified as ‘Samba username map script Command Execution’ was leveraged to exploit the target system remotely. This vulnerability results from a flaw in the handling of the username map script within Samba, which allows the unauthorized execution of arbitrary commands on the victim system. During the assessment, I utilized a Metasploit exploit module specifically designed for this vulnerability; this module “exploits a command execution vulnerability in Samba versions 3.0.20 through 3.0.25rc3 when using the non-default ‘username map script’ configuration option” (Rapid7, 2018). By using the Metasploit ‘multi/samba/usermap_script’ exploit module, a crafted payload was sent to the vulnerable Samba service, which executed a malicious shell command. Through this exploit, I was able to bypass existing authentication mechanisms and achieve root access on the victim machine.


### Create Log Analytics Workspace & Connect To VM

After gaining root access on the victim machine through the Samba exploit, I proceeded to extract sensitive company data. Specifically, I targeted the user hash for the account redteam3student4. First, copying the user hash from the referenced /etc/shadow file found in the root directory. Then, utilizing the nano text editor to create an alternate file, I saved this hash to my local file system apart from the compromised machine. To decrypt the hash, I used the password-cracking tool John the Ripper entering the command ‘john hash.txt’ which effectively cracked the hash, obtaining the plaintext password for redteam3student4. Similarly, data discovered within the redteam3 -> student4 -> ‘mypass.txt’ file was copied to an alternate file on my local system, and the ‘base64 -d’ utility was used for decoding its contents which was base64 encoded.


### Setup Azure Sentinel

To remediate the vulnerability exploited on the remote system, several key security controls should be implemented. Firstly, it's essential to apply necessary patches and update Samba software to its latest version. Then, strict permissions and access controls must be configured for the ‘user_map script’ to reduce unauthorized access. Following, avoid running Samba with root permissions to reduce attack surface and limit access on the system. Additionally, the implementation of multi-factor authentication on sensitive systems improves the company’s overall security posture as “it operates on the principle that even if one credential becomes compromised, unauthorized users will be unable to meet the second or third form of required authentication” (Secoda, 2024). These measures together strengthen defenses against this exploit ensuring the protection of data against unauthorized access and security breaches.

### Log into VM with Remote Desktop (fail 1 logon) 


### Turn Off Windows Firewall


### Retreive Powershell Script, Generate Geolocation API key and Run Script



### Create Custom Log in Log Analytics Workspace



### Extract Fields From Raw Custom Log Data


### Setup Visual Map
