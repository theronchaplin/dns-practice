
<h1>Practice & Understanding DNS</h1>

This lab focuses on Domain Name System (DNS) concepts and practical exercises to configure and test DNS records. We'll use Azure-hosted virtual machines to understand how DNS A-records, CNAME records, and local DNS caching function. Through hands-on activities, the lab demonstrates DNS troubleshooting and record management in a controlled environment.<br />
<br />
<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- PowerShell
<br />
<br />

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)
<br />
<br />

<h2>Walkthrough Steps</h2>

1. Setup
  - Power on the DC-1 (domain controller) and Client-1 virtual machines in Azure
  - Log into DC-1 as mydomain.com\jane_admin<br />
      ![image](https://github.com/user-attachments/assets/7422fa0a-5a27-4478-aa5e-7dd36bec3f0a)
  - Log into Client-1 as mydomain\jane_admin<br />
      ![image](https://github.com/user-attachments/assets/8e5ee4d0-9045-4083-905e-54abc8930f60)
<br />
<br />

2. A-Record Exercise
  - From Client-1, attempt to ping "mainframe" and observe the failure
    - Explanation: There’s no DNS record for "mainframe," so the request fails<br />
      ![image](https://github.com/user-attachments/assets/aaea69af-c79d-4c39-ba2c-163263fc91c6)
  - Use nslookup mainframe from Client-1 and confirm the failure (no DNS record)<br />
      ![image](https://github.com/user-attachments/assets/1c49961b-736f-4c92-a718-db57a97e8448)
  - On DC-1, create an A-record for "mainframe" and point it to DC-1’s private IP address<br />
      ![image](https://github.com/user-attachments/assets/7cba78bb-42fb-4805-a787-c1b7c77d2f72)
  - Return to Client-1 and try pinging "mainframe" again. It should now work<br />
      ![image](https://github.com/user-attachments/assets/622d4c58-171b-40b4-9dd1-205f421966c3)
<br />
<br />

3. Local DNS Cache Exercise
  - On DC-1, change the "mainframe" A-record address to 8.8.8.8<br />
      ![image](https://github.com/user-attachments/assets/8321fed5-601b-4fd5-8236-8bd51b9ddf40)
  - On Client-1, ping "mainframe" again. It will still respond with the old IP address due to the cached record<br />
      ![image](https://github.com/user-attachments/assets/13761564-3c47-4938-a98e-2d2012526203)
  - View the local DNS cache using ipconfig /displaydns on Client-1<br />
      ![image](https://github.com/user-attachments/assets/6c03873c-4ec5-4a5b-90af-382268d71076)
  - Flush the DNS cache with ipconfig /flushdns and confirm it is empty (ipconfig /displaydns)<br />
      ![image](https://github.com/user-attachments/assets/dd811ca5-2d0d-465d-b848-abceceff4822)
  - Ping "mainframe" again. This time, the new IP address from the updated DNS record will appear<br />
      ![image](https://github.com/user-attachments/assets/18114235-3c3e-4e03-b3e6-0f20ff4c6c9d)
<br />
<br />

4. CNAME Record Exercise
  - On DC-1, create a CNAME record that maps "search" to www.google.com<br />
      ![image](https://github.com/user-attachments/assets/bd66d740-3191-4243-b18d-7970880950a7)
  - On Client-1, ping "search" to verify the CNAME record’s resolution<br />
      ![image](https://github.com/user-attachments/assets/12c5afc1-66fd-4f96-9891-f9358c46e24f)
  - Use nslookup search on Client-1 to observe how the CNAME record resolves<br />
      ![image](https://github.com/user-attachments/assets/b8982030-7967-42cc-839f-c850bcc7e2da)
<br />
<br />
