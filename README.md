<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
Throughout this tutorial we focus on monitoring and analyzing network traffic between Azure Virtual Machines using Wireshark. It also includes working with Azure Network Security Groups (NSG) to manage and control network traffic. Various protocals such as ICMP, SSH, DHCP, DNS, and RDP are observed within Wireshark to understand how communication happens between systems or Virtual Machines.
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Actions and Observations</h2>

**1. Observing ICMP Traffic**
- If using Mac, install Microsoft Remote Desktop
- Using RDP, connect to the Windows 10 VM.
- Install [Wireshark](https://www.wireshark.org) within the Windows 10 VM.
- Open Wireshark and start a packet capture.
- Filter for ICMP traffic in Wireshark.
- Retrieve the private IP address of the Linux VM and attempt to ping it from the Windows 10 VM.
- Observe ping requests and replies within Wireshark.
- From the Windows 10 VM, open Command Line or PowerShell, and ping a public website (e.g., `www.google.com`).
- observe the traffic in WireShark
  
<img width="1898" height="788" alt="Screenshot 2026-02-24 185452" src="https://github.com/user-attachments/assets/d92f10d2-3ba4-427f-97ff-9a1f1e182b5e" />
<img width="1812" height="888" alt="image" src="https://github.com/user-attachments/assets/80508f41-8992-4105-828d-9798a3fb27ed" />
<img width="1886" height="915" alt="image" src="https://github.com/user-attachments/assets/eb959b0f-783c-411d-894a-cd462450668f" />
<img width="1549" height="910" alt="image" src="https://github.com/user-attachments/assets/323c53f5-4739-415c-8b1d-3341100f01c9" />
<img width="1386" height="420" alt="Screenshot 2026-02-24 191138" src="https://github.com/user-attachments/assets/1ea9505d-eedc-4b10-9809-ca031e3f8875" />
<img width="1902" height="936" alt="image" src="https://github.com/user-attachments/assets/8e2fffb7-5d4c-4480-bd8d-72703a0e6181" />




**2. Configuring a Firewall (Network Security Group)**
- Initiate a perpetual/non-stop ping from the Windows 10 VM to the Ubuntu VM.
- Open the Network Security Group (NSG) associated with the Linux VM and disable inbound ICMP traffic.
- Return to the Windows 10 VM and observe the ICMP traffic and command line ping activity in Wireshark.
- Re-enable inbound ICMP traffic in the NSG.
- Back in the Windows 10 VM, observe the ICMP traffic and ping activity resuming in Wireshark.
- Stop the ping activity.
<img width="624" height="555" alt="image" src="https://github.com/user-attachments/assets/fc9719cf-d706-4871-8813-325d3d813736" />
<img width="1794" height="1087" alt="image" src="https://github.com/user-attachments/assets/6f38a1a0-cb20-4205-83f8-6a2371de62d4" />
<img width="877" height="548" alt="Screenshot 2026-02-24 193855" src="https://github.com/user-attachments/assets/76b693af-162f-46f1-aa03-07ab91a953f6" />
<img width="1490" height="576" alt="image" src="https://github.com/user-attachments/assets/0cc8f104-b0eb-459e-9a4b-233500259c2f" />
<img width="777" height="535" alt="image" src="https://github.com/user-attachments/assets/a5af13de-76ab-416c-b06b-df151b5c6501" />




**3. Observing SSH Traffic**
- In the Windows 10 VM, open Wireshark and start a packet capture.
- Filter for SSH traffic in Wireshark.
- Using PowerShell in the Windows 10 VM, SSH into the Ubuntu VM using its private IP address:
  - `ssh labuser@<private IP address>`
- Type commands (e.g., username, password) in the Linux SSH session and observe SSH traffic in Wireshark.
- Exit the SSH connection by typing `exit` and pressing [Enter].
<img width="746" height="484" alt="image" src="https://github.com/user-attachments/assets/41e9dc17-1c21-4f78-861f-1005bffa1545" />
<img width="1221" height="566" alt="Screenshot 2026-02-24 202054" src="https://github.com/user-attachments/assets/09d8b753-4c66-44f3-bea7-886af2b5f5cd" />

<img width="1406" height="826" alt="Screenshot 2026-02-24 201620" src="https://github.com/user-attachments/assets/198ba6a0-08b9-4067-b40b-2fecfcac71fe" />







**4. Observing DHCP Traffic**
- Back in Wireshark, filter for DHCP traffic.
- In the Windows 10 VM, attempt to issue a new IP address using the Command Line:
  - `ipconfig /renew`
- Observe DHCP traffic appearing in Wireshark.
<img width="960" height="682" alt="Screenshot 2026-02-24 204137" src="https://github.com/user-attachments/assets/5dad524f-8a8f-469f-b5ed-71913330f7e6" />
<img width="1242" height="577" alt="Screenshot 2026-02-24 204753" src="https://github.com/user-attachments/assets/41814628-72d3-45a9-a9b2-7b0b100df463" />


**5. Observing DNS Traffic**
- Back in Wireshark, filter for DNS traffic.
- In the Windows 10 VM, use `nslookup` to resolve the IP addresses of `google.com` and `disney.com`:
  - `nslookup google.com`
  - `nslookup disney.com`
- Observe DNS traffic in Wireshark.
<img width="879" height="533" alt="Screenshot 2026-02-24 205139" src="https://github.com/user-attachments/assets/e3ce49c9-4e38-4c8e-8a22-62dd867e4f02" />
<img width="473" height="342" alt="Screenshot 2026-02-24 205818" src="https://github.com/user-attachments/assets/f6252881-980c-4e05-8a90-52f74e00f078" />
<img width="1538" height="865" alt="Screenshot 2026-02-24 205837" src="https://github.com/user-attachments/assets/005ce102-9125-4095-b074-77e40418dfdb" />
<img width="470" height="353" alt="Screenshot 2026-02-24 205918" src="https://github.com/user-attachments/assets/80bbe9cc-2918-4ee6-b4fc-846b94ddaed2" />
<img width="1427" height="984" alt="Screenshot 2026-02-24 205946" src="https://github.com/user-attachments/assets/1673974f-cbb5-407d-b476-4fbb2a0d26b4" />



**6. Observing RDP Traffic** 
- Back in Wireshark, filter for RDP traffic using the filter `tcp.port == 3389`.
- Observe the non-stop traffic being transmitted.
  - Explanation: RDP traffic constantly transmits because it streams a live view from one computer to another, leading to continuous traffic.
<img width="1151" height="725" alt="image" src="https://github.com/user-attachments/assets/aa932325-279d-4d0e-80fa-2eade25e89de" />



<h2>Purpose</h2>

The purpose of this project is to develop a deeper understanding of how network traffic flows within cloud environments and how security configurations help control and protect that traffic. Within the Azure-based systems, this project allows us to analyze how devices communicate with each other between virtual networks and how security tools, such as Network Security Groups, regulate access and data transmission. This also helps us build practical knowledge of how various protocols function and how network activity can be monitored and observed. Lastly this project strengthens troubleshooting skills by allowing to identify, analyze, and resolve network connectivity and security issues. Overall, the project provides foundational experience that is essential for effectively managing, securing, and maintaining cloud-based network infrastructures in Microsoft Azure.

