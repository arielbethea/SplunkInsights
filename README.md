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
Check file and directory details: <br/>
<img src="https://i.imgur.com/NvgHoCW.png" height="80%" width="80%" alt="Authorization Configuration Steps"/>
<p align="center"> 

<p>Used the ls -l command to check the file and directory details and used the ls -a command to check for hidden files. Alternatively, the ls -la command can be used to simultaneously check details of files, hidden files, and directories.
</p>
<p>There is 1 directory, 4 files, and 1 hidden file.
</p>
<br />

<br />
<br />
<p align="center"> 
File permissions description:  <br/>
<p>The permissions string contains 10 characters displaying whether we are looking at a directory (d) or file (-) and the read (r), write (w), and execute (x) permissions for the user, group, and other. - in place of r,w, or, x denotes a lack of that permission for a user, group, or other.</p>
<p>The first character displays whether it’s a directory or file. The second through fourth characters display whether the user has read, write, and/or execute permissions. The fifth through seventh characters display whether the group has read, write, and/or execute permissions. The eighth through tenth characters display whether other has read, write, and/or execute permissions.</p>
<br />

<p align="center">
<br />
Change file permissions:  <br/>
<img src="https://i.imgur.com/A43shaV.png" height="80%" width="80%" alt="Authorization Configuration Steps"/>
<p align="center"> 

<p>Only the user and group should have read and write permissions for the project_k.txt file, so I removed write permissions for other in the project_k.txt file by entering the command chmod o-w project_k.txt and confirmed the changes using the ls -l command.
</p>
<p>File project_m.txt is a restricted file that should only have permissions for the user and none for group or other. Group had read permissions, so I removed read permissions for group in the project_m.txt file by entering the command chmod g-r project_m.txt and confirmed the changes using the ls -l command.
</p>
<br />

<p align="center">
<br />
Change file permissions on a hidden file:  <br/>
<img src="https://i.imgur.com/4scAuZp.png" height="80%" width="80%" alt="Authorization Configuration Steps"/>
<p align="center"> 

<p>Used the ls -la command to view permissions on the hidden .project_x.txt file. Used the command chmod u=r,g=r .project_x.txt to change the permissions so that only the user and the group have read permissions. Confirmed the changes with the ls -la command.
</p> 
<br />

<p align="center">
<br />
Change directory permissions:  <br/>
<img src="https://i.imgur.com/WmdtABQ.png" height="80%" width="80%" alt="Authorization Configuration Steps"/>
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
