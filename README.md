# DNS-Testing

<p align="center">
<img src="https://i.imgur.com/MwrkwEQ.png" height="60%" width="60%" alt="DNS Photo"/>
</p>

<h1> Objectives </h1>

- Inspect DNS A-records on the server 
- Create some of my own A-Records on the server and observe them from the client
- Delete records from the server and inspect/clear the client DNS cache to gain understanding
- CNAME records
 <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 Pro (22H2)

<h2>DNS Configuration Steps</h2>
<p>
Remote Connect to both of our VMs made from the previous Active Directory lab. 

 - Open up our command prompt in DC-1 and attempt to “ping mainframe”
</p>

<p>
<img src="https://i.imgur.com/e5dZJkm.png" height="80%" width="80%" alt="DNS Steps">
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
Create an A-records for mainframe.com. Within DC-1 we will open up 

 - Server Manager > Tools > DC-1 > Forward Lookup Zones, and right click bensdomain.com
 - Click New Host (A or AAAA). Name it mainframe, and set the IP address to the dc-1 address listed under bensdomain.com
</p>

<p
<img src="https://i.imgur.com/mMUPdM9.png" height="80%" width="80%" alt="DNS Steps"/>
</p>


<p>
Attempt to ping mainframe on CLIENT-1 in the command prompt to test connectivity and also use ipconfig /displaydns to observe the DNS records.
</p>

<p>
<img src="https://i.imgur.com/96xUgLF.png" height="80%" width="80%" alt="DNS Steps">
</p>

<p><strong>.</strong></p>
<p><strong>.</strong></p>

<p>
In the Client VM, open the command prompt <b>as an Admin</b>. 
 
 - Ping "mainframe" it will fail. 
 - Nslookup "mainframe" provides similar results and shows that there is no DNS record for it.
 - A DNS A-record will have to be created for mainframe on the domain controller.
 - On the domain controller, open the DNS Manager and go to the domain you created within the Forward Lookup Zones tab.
 - In my case, it is bensdomain.com
 - Right click on the page and create a New Host.
 - For name, input mainframe and the IP address should be the same IP as the domain controller so that ping can resolve.
 - Refresh the DNS server so that the new record can be updated.
 - Upon returning to the client, ping mainframe once again to see that it will now resolve.
</p>
<br />


<p>
<img src="https://i.imgur.com/3m6LJUP.png" height="80%" width="80%" alt="DNS Steps">
</p>

<h2>Lessons Learned</h2>
<p>
In this lab, it helped me understand how DNS directly works on a computer and the network. DNS records can change and sometimes this can cause connectivity issues. The DNS cache may have the old records and needs to be cleared out to update to the new records. The command ipconfig /flushdns is a common troubleshooting tool that has been referenced a lot in IT programs and I did not get a complete understanding of how and why this works until I had done this lab. In the context of pinging "mainframe" at the start of the lab, the DNS cache gets checked first. If there is no result, the host file will be checked. The DNS server will be checked if there are no results in the host file. I made a record on the DNS server so a ping to the mainframe can resolve. A CNAME record maps an alias name to another domain name. In this case, "search" was another name for Google.
</p>
