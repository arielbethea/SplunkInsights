<h1>Creating a Dyanic and Intearctive Dashboard in Splunk</h1>

<h2>Scenario</h2>

- <b>Your Company</b>
  - Buttercup Enterprises is a large national online retailer operating in the US, which sells a variety of books, clothing and other gifts through its online webstore.
  - Buttercup Enterprises have recently invested in Splunk and now they want to start making use of it across the business.

- <b>Your Role</b>
  - You are one of the chosen few: a Splunk power user!
  - Your responsibility is to provide insights to users throughout the company
  - The teams you support include:
    - IT Operations
    - DevOps
    - Business Analytics
    - Security and Fraud

- <b>What Does the Business Want to See?</b>
  - We need to create a dashboard with four views:
    - IT Operations team: Investigate successful versus unsuccessful web server requests over time
    - DevOps team: Show the most common customer operating systems and which web browsers are experiencing the most failures
    - Business Analytics team: Show lost revenue from the Buttercup Enterprises website
    - Security and Fraud team: Show website activity by geographic location
      
<br />

<h2>Languages and Utilities Used</h2>

- <b>Splunk</b> 
  - <b>Search Processing Language (SPL)</b>
  - <b>Dashboard Studio</b> 

<h2>Environments Used </h2>

- <b>Windows 11</b> (22H2)
- <b>Server 2022</b>

<h2>Program walk-through:</h2>

<p align="center">
Web Server Status Codes Over Time: <br/>
<img src="https://i.imgur.com/yHcV2Dn.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 

<p>I used the following search <b>index=main sourcetype=access_combined</b> to search the main index for all web server events and specified a timeframe over the last 60 minutes. In the search results, I selected the status field and filtered by Top Values by Time. My new search was then automatically updated to <b>index=main sourcetype=access_combined | timechart count by status limit=10</b> and allowed me to create my data visualization for these results. 
</p>
<br />

<br />
<br />
<p align="center">
Most Popular Operating Systmes: <br/>
<img src="https://i.imgur.com/RTEodWE.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
  
<p>I used the following search <b>index=main sourcetype=access_combined | top limit=20 platform</b> after extracting a field based on the operating system name and labeling it as platform. Then I added  <b>showperc=f</b> in order to remove the pecent column from my table to allow for a cleaner view in the dashboard
</p>

<p align="center">
Web Browsers with Most Failures: <br/>
<img src="https://i.imgur.com/OZstsnI.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
  
<p>I used the following search <b>index=main sourcetype=access_combined | top limit=20 platform</b> after extracting a field based on the operating system name and labeling it as platform. Then I added  <b>showperc=f</b> in order to remove the pecent column from my table to allow for a cleaner view in the dashboard
</p>

<br />

<p align="center">
<br />
Change file permissions:  <br/>
<img src="https://i.imgur.com/A43shaV.png" height="80%" width="80%" alt="Creating Splunk Dashboar"/>
<p align="center"> 

<p>Only the user and group should have read and write permissions for the project_k.txt file, so I removed write permissions for other in the project_k.txt file by entering the command chmod o-w project_k.txt and confirmed the changes using the ls -l command.
</p>
<p>File project_m.txt is a restricted file that should only have permissions for the user and none for group or other. Group had read permissions, so I removed read permissions for group in the project_m.txt file by entering the command chmod g-r project_m.txt and confirmed the changes using the ls -l command.
</p>
<br />

<p align="center">
<br />
Change file permissions on a hidden file:  <br/>
<img src="https://i.imgur.com/4scAuZp.png" height="80%" width="80%" alt="Creating Splunk Dashboar"/>
<p align="center"> 

<p>Used the ls -la command to view permissions on the hidden .project_x.txt file. Used the command chmod u=r,g=r .project_x.txt to change the permissions so that only the user and the group have read permissions. Confirmed the changes with the ls -la command.
</p> 
<br />

<p align="center">
<br />
Change directory permissions:  <br/>
<img src="https://i.imgur.com/WmdtABQ.png" height="80%" width="80%" alt="Creating Splunk Dashboar"/>
<p align="center"> 

<p>Only the user should have permissions for the drafts directory, so I removed the execute permissions for the group in the drafts directory by entering the command chmod g-x drafts and confirming the changes by entering the command ls -l.
</p>  
<br />
<br />
<p align="center"> 
Summary:  <br/>
<p>Used the ls -l command and ls -a command to check the details of a directory and its files, including hidden files. Used the chmod command (e.g. chmod o-w project_k.txt) to remove file permissions for restricted files and used the ls-l command to confirm that changes were successful. Used the chmod command (e.g. chmod u=r,g=r .project_x.txt) to change file permissions on a hidden file and used the command ls -la to confirm the changes. Used the chmod command to change directory permissions (e.g. chmod g-x drafts) and confirmed the changes using the ls -l command.
</p>

<br />
 
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
