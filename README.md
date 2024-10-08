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
![honey8](https://github.com/user-attachments/assets/dccd6a7e-33a6-4ecc-9db7-f4c06f90cf0d)
The first step I took was setting up a VM in Azure portal. Navigate to the "Virtual Machines" section. From there, I clicked on "Create" and chose "Virtual Machine." I configured the VM by selecting the appropriate subscription, creating a new resource group for better organization, and choosing a region close to my location for optimal performance. For the operating system, I picked a Windows Server image, since I'll be using RDP to simulate the attacks.

### Allow All Traffic Through Firewall
![honey18](https://github.com/user-attachments/assets/4126c9ba-6cb9-4ed6-bf13-fbee37fb1f44)
The next step is to configure the firewall to allow all incoming traffic. I started by going to the "Networking" tab in the Azure portal for the VM and clicked on the “Inbound port rules” section. Here, I modified the security group settings to ensure that the firewall wouldn’t block any traffic by creating a new inbound rule that allows all traffic by selecting "Any" for both the source and destination IPs, as well as for the protocol (TCP/UDP). I set the priority to a lower number to ensure that this rule would take precedence over any other rules. This setup will allow any type of network traffic to reach the VM, which is necessary for testing and simulating attack scenarios that Azure Sentinel can detect/log.


### Create Log Analytics Workspace & Connect To VM

![honey1](https://github.com/user-attachments/assets/421cd8f0-b3f9-461b-a2e2-b355536d4f8f)
<br><br>
The next step is to create a log analytics workspace and connect it to the virtual machine. I navigated to the "Log Analytics Workspaces" section in the Azure portal then clicked "Create." I selected the same resource group as my VM, gave the workspace a name and region. Adding this workspace is crucial because it allows me to centralize logs and data from the VM for real-time analysis in Azure Sentinel. The workspace streamlines monitoring, making it easier to detect anomalies and suspicious activity.
<br><br>
![honey19](https://github.com/user-attachments/assets/a27ab84d-cab9-4938-b872-e6ed340e95a3)
Once the workspace was created, I went to the VM’s "Extensions" tab and added the "Log Analytics Agent" extension. During the setup, I linked the agent to the Log Analytics Workspace I just created by providing the workspace ID and key. This connection allows the VM to send security and performance data directly to Azure Sentinel through the workspace, enabling me to monitor and detect any suspicious RDP activity.


### Setup Azure Sentinel
![honey3](https://github.com/user-attachments/assets/97e492de-e232-4706-a1fe-70266160bc78)
The next step was to enable Azure Sentinel and configure it to collect all necessary data from the virtual machine. I started by navigating to the 'Azure Sentinel' in the Azure portal and clicked "Add" to create a new instance. I selected the log analytics workspace I had set up earlier, as this is where Sentinel would pull the data from.
<br><br>
![honey2](https://github.com/user-attachments/assets/cc37f432-c32c-480d-9b8b-885463cd44f7)
During this setup, I ensured that "All Events" was checked under data collection tab, as this would allow Sentinel to collect every type of event from the VM, including RDP login attempts, process executions, and other critical security events.

### Log into VM with Remote Desktop (fail 1 logon) 
![honey4](https://github.com/user-attachments/assets/c5fd7b3c-1e7e-4b75-9a07-796c117ca67f)
![honeyfail](https://github.com/user-attachments/assets/3cc1865c-da2e-4c11-9f84-a016a27c2796)
<br><br>
I opened the Remote Desktop Connection app on my local machine and entered the public IP address of the VM. For the test, I purposely entered incorrect login credentials to generate failed login events for documentation and ensuring the data was being correctly logged. After attempting the failed login, I accessed the VM’s Event Viewer by logging in with correct credentials and navigating to Windows Logs > Security. I located the event ID 4625 associated with the failed logon attempt, which provided detailed information about the login failure, including the time, username, and source IP address. 

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
![honey13](https://github.com/user-attachments/assets/f6df14f4-5af5-4862-bf9d-63bba71be625)

### Setup Visual Map
![honey15](https://github.com/user-attachments/assets/2d4dfe67-d94b-4bb5-b5d1-2f7fa8cc5535)
![honey16](https://github.com/user-attachments/assets/c03992b2-dba5-4111-93ef-813a4b8b72a6)

