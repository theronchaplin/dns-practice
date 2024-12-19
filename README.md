
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
  - Power on the DC-1 (domain controller) and Client-1 virtual machines in Azure.
  - Log into DC-1 as mydomain.com\jane_admin and into Client-1 as mydomain\jane_admin.
<br />
<br />

2. A-Record Exercise
  - From Client-1, attempt to ping "mainframe" and observe the failure.
    - Explanation: There’s no DNS record for "mainframe," so the request fails.
  - Use nslookup mainframe from Client-1 and confirm the failure (no DNS record).
  - On DC-1, create an A-record for "mainframe" and point it to DC-1’s private IP address.
  - Return to Client-1 and try pinging "mainframe" again. It should now work.
<br />
<br />

3. Local DNS Cache Exercise
  - On DC-1, change the "mainframe" A-record address to 8.8.8.8.
  - On Client-1, ping "mainframe" again. It will still respond with the old IP address due to the cached record.
  - View the local DNS cache using ipconfig /displaydns on Client-1.
  - Flush the DNS cache with ipconfig /flushdns and confirm it is empty (ipconfig /displaydns).
  - Ping "mainframe" again. This time, the new IP address from the updated DNS record will appear.
<br />
<br />

4. CNAME Record Exercise
  - On DC-1, create a CNAME record that maps "search" to www.google.com.
  - On Client-1, ping "search" to verify the CNAME record’s resolution.
  - Use nslookup search on Client-1 to observe how the CNAME record resolves.
<br />
<br />
