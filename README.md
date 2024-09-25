### Azure Sentinel RDP Attack Map

## Objective

TBD

<img src="https://github.com/user-attachments/assets/81d9719e-a74d-4fda-bfc0-ffd59ddc8f07" width="450"/>


### Skills Learned

- TBD

### Tools Used

- TBD


## Steps


### Create Virtual Machine



### Allow All Traffic Through Firewall



### Create Log Analytics Workspace & Connect To VM



### Setup Azure Sentinel



### Log into VM with Remote Desktop (fail 1 logon) 


### Turn Off Windows Firewall on VM
<img src="https://github.com/user-attachments/assets/e4369f4f-7df4-437d-87a9-2a028750fe4a" width="300"/>

Turning off Windows Firewall on a VM while capturing a live cyber attack demo, allows me to demonstrate true vulnerabilities without the interference of built-in security mechanisms. The firewall is designed to block unauthorized network traffic, which could prevent certain attack vectors from being executed successfully during the demo. By disabling it, I showcase the behavior of unprotected systems and how attackers exploit weak or misconfigured security settings. This setup helps in illustrating the importance of proper security controls and provides a controlled environment for observing real-time attack tactics, tools, and impact. 

### Retreive Powershell Script, Generate Geolocation API key and Run Custom Script
![honey9](https://github.com/user-attachments/assets/5ae0ae50-171f-4965-bf9b-aa7302d56564)


### Create Custom Log in Log Analytics Workspace
<img src="https://github.com/user-attachments/assets/120c85d1-d7d3-4ea3-8c05-a43d0a8d6794" width="550">
<img src="https://github.com/user-attachments/assets/cddabee8-6b7f-427c-96ab-4dda30c516e4" width="400"><br>

I start by collecting a sample log from script output on my VM. First, I ensure that the VM is connected to my Log Analytics Workspace through the Microsoft Monitoring Agent. This connection allows logs and data from my VM to be sent to the workspace. I save it as a .txt file. The next step is to head into the Azure portal and navigate to Log Analytics Workspace. From there, I select the workspace I’m working with and click on Custom Logs under the Settings section. I click Add to start the process of creating a custom log. I upload my sample log file, and the system analyzes it to help define the structure of the log data. Afterward, I name my custom log file with a unique identifier, MyCustomLog_CL. Now that my custom log is configured, data from my VM’s script output will start flowing into Log Analytics under the newly created custom log type. I can query the data using the custom log name in the KQL to analyze and visualize my logs as needed.





### Extract Fields From Raw Custom Log Data


### Setup Visual Map
