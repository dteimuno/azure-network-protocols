<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create Our Resources
- Observe ICMP Traffic
- Observe SSH Traffic
- Observe DHCP Traffic
- Observe DNS Traffic
- Observe RDP Traffic
- Terminate Azure Resources

<h2>Actions and Observations</h2>

<p>
<img height="80%" width="80%" alt="Screenshot 2024-05-14 at 2 01 25 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/de5d6777-a94b-4ac5-b0ca-57ca01cf7377">
</p>
<p>
Go to Azure Portal>Virtual Machines>Set: 'Vm name', 'Region', 'Image:Windows 10Pro 22H1 x64','Size', 'Username' and 'Password'. Confirm licensing permission and then review network settings and click 'Create' to Create VM1
</p>
<br />

<p>
<img height="80%" width="80%" alt="Screenshot 2024-05-14 at 2 29 33 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/9bb4c187-0cce-4e1b-98c5-a848604fc519">
</p>
<p>
Create an Ubuntu Linux VM by navigating to Azure Portal>Virtual Machines>Set: 'Vm name', 'Region', 'Image:Ubuntu Server 20.04 LTS x64 Gen2','Size', 'Username' and 'Password'.
</p>
<br />

<p>
<img height="80%" width="80%" alt="Screenshot 2024-05-14 at 2 40 53 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/649780ab-777e-4479-9070-846cf305a973">
</p>
<p>
Ensure that both VM1 and VM2 are both in the same resource group and on the same network group for the best results. 
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 1 38 17 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/f42ffed7-5959-4602-8b91-579e8b9876eb">
</p>
<p>
Use Remote Desktop to connect to your newly created Virtual Machines. For each machine, type in the Public IP address(gotten from Azure) and click connect. Enter your user name and password to login
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 1 44 16 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/d5d48078-43d0-4181-a242-eafdee1d8565">
</p>
<p>
Open Interner Explorer on VM1(Windows 10 Pro), and download Wireshark
</p>
<br />

<p>
<img width="499" alt="Screenshot 2024-05-15 at 1 46 53 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/8f23d88b-ae2b-445b-9ffc-6d0f4f78d4ac">
</p>
<p>
Setup and install Wireshark after download.
</p>
<br />

<p>
<img width="750" alt="Screenshot 2024-05-15 at 1 51 10 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/a7e28ec1-7205-49e4-8dbc-9bff0fcb7b71">
</p>
<p>
Open Wireshark. Double-click Ethernet to inspect network traffic.
</p>
<br />

<p>
<img width="748" alt="Screenshot 2024-05-15 at 1 54 36 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/fcc385e1-a70b-4d7c-83ac-150c06a6ee64">
</p>
<p>
Type ICMP in search bar, and press ENTER  to filterr out traffic by the ICMP protocol. There is no network traffic seen.
</p>
<br />

<p>
<img width="1397" alt="Screenshot 2024-05-15 at 1 59 25 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/91f5f406-b431-4042-a7e4-04d650e82e78">
</p>
<p>
Ping VM2(ubuntu) on VM1 using Windows Powershell. Determine the Private IP address of VM2, open Powershell and enter the ping command followed by the private IP address. The diagram above shows a successful ping, confirming they are on the  same network.
</p>
<br />

<p>
<img width="696" alt="Screenshot 2024-05-15 at 2 04 19 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/51e1901c-c553-463d-a1e9-5412cf3406dd">
</p>
<p>
Try to ping google.com by typing the ping google.com as ordinary and by the IPv4 addrress. They both show a success return of information. Meaning we can access google on this machine(VM1)
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 2 08 54 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/4bc6310c-829c-442c-874d-82e7d7c11e50">
</p>
<p>
Ping VM2 non-stop from VM1. Observe the network traffic ans results showing continued ping success.
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 2 17 08 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/41d133c5-4c99-42c1-928f-d7226a50519d">
</p>
<p>
Deny inbound network traffic to VM2. To do so, go to Azure> Network Security Groups> the Network Security Group for VM2> Settings>Inbound Security Rules. Create rule to deny all  incoming ICMP traffic. To do so,  Click "Add", click "ICMP" in Ports subheading, click Deny under actions. Click save. Refresh Virtual Machine for effects to take place
<img width="1131" alt="Screenshot 2024-05-15 at 2 21 17 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/07d72277-24ed-459d-bea0-e424842bcc2b">
Request starts to be inhibited because inbound traffic to the ICMP port is blocked. This illustrates the power of firewalls. 
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 2 26 03 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/63c30ac4-5058-4606-84b9-27de40c47b5c">
</p>
<p>
Re-enable ICMP traffic to VM2 ports via Network Security Groups. See below the effect of re-enabling the ICMP port in Wireshark and Windows Powershell
<img width="1153" alt="Screenshot 2024-05-15 at 2 30 25 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/7b54e159-4cb9-421e-b9bd-a470dae25f27">
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 2 39 29 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/e92a0170-f54f-43bb-a5c4-290d1fa4bf55">
</p>
<p>
Connect securely to the SSH of VM2. Type: ""ssh username@VM2 Private IP address"> Type yes> Type in password and press ENTER. If you successfully log in, you should see a green labelling of  VM2 showing you a remotely connected to it.
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 2 39 29 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/0a8c65c3-f89e-4625-b09a-bad7fbbc0734">
</p>
<p>
Enter a few commands and view results in powershell. Once done, type exit cmd to exit VM2 shell
</p>
<br />

<p>
<img width="80%" Height="80%" alt="Screenshot 2024-05-15 at 2 39 29 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/63277420-8ef0-4617-aa05-bc985d9a1929">
</p>
<p>
Change wireshark query to DNS.In powershell, type nslookup www.google.com. Press ENTER. Powershell should show results as well as Wireshark showing network data
</p>
<br />

<p>
<img width="80%" height="80%" alt="Screenshot 2024-05-15 at 3 02 05 AM" src="https://github.com/dteimuno/azure-network-protocols/assets/169619672/89c4b807-fe9d-4210-a8ba-e13e40ac37ed">
</p>
<p>
Delete virtual machines and resources in Azure to not rack up a sizeable bill
</p>
<br />
