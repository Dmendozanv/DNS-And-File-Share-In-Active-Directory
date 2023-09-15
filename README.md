# DNS-And-File-Share-In-Active-Directory
<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe how DNS works within a Domain Controller between the Domain Controller and its various users.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory
- DNS

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Windows 2022 Server
  
<h2>Setup</h2>

Create two Virtual Machines, with one of them being the Domain Controller (DC-1) and the other being (Client-1). The DC-1 VM will be on a Windows 2022 Server and the Client-1 will be on Windows 10. (See Active Directory Repository).
<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/CYeS2eR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/dDPRr2X.png" height="80%" width="80%"/>
</p>
<p>
First, open Command Prompt in Client-1 and attempt to ping "mainframe". You will notice that it fails to find the mainframe IP address. To allow the domain controller to recognize "mainframe" an A-Record needs to be added to its DNS. Go to the server manager and then click on DNS. Within DNS add an A-Record with the DC-1's private IPAddress.
</p>
<br />

<p>
<img src="https://i.imgur.com/zZOZTOC.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Now if you go back into Client-1 you can ping mainframe and it will be recognized with the new IPAddress. 
</p>
<br />

<p>
<img src="https://i.imgur.com/cV8mFwV.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
<p>
<img src="https://i.imgur.com/rl3mUaM.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
</p>
Now go back into DC-1 and change the A-Record to 8.8.8.8. You will notice that when you ping mainframe in Client-1 again it will still have the old address. The DNS will need to be flushed so it will have the new DNS. Make sure to go into Command Prompt as admin and enter ipconfig/flushdns. This should allow it to recognize the new address.
</p>
<br />

<p>
<img src="https://i.imgur.com/jx3s1UY.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Next add a CNAME ALIAS for www.google.com, you will name it search. Now if you go back into Client-1 and nslookup/search it will show you www.google.com and its IPAddress.
</p>
<br />

<p>
<img src="https://i.imgur.com/FoTAnBG.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
Finally add a CNAME ALIAS for www.google.com, you will name it search. Now if you go back into Client-1 and nslookup/search it will show you www.google.com and its IPAddress.
</p>
<br />

<h2> Final Thoughts</h2>

<p> By creating A-Records and CNAME Alias we can see how the DNS functions when falling under a Domain Controller. Also flushing the DNS can also be a way to troubleshoot when an end user is unable to connect and the DNS has changed.</p>
