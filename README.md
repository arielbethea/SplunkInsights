<h1>Creating a Dynamic and Interactive Dashboard in Splunk</h1>

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
<br />
Challenge Task:  <br/>
<p>Q1. How can we find events with a status of 200 that are not purchase events?
</p>

<p>This can be found using the search <b>index=main sourcetype=access_combined action!=purchase status=200</b>
</p>

<p align="center">
<img src="https://i.imgur.com/E7wbVvg.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
<br />
  
<p>Q2. How can we find events where someone had an error when trying to either add an item or remove an item from their cart? (Hint: A HTTP status code of 200 means the transaction was successful. A code of 400 or higher usually means that a failure occurred.)
</p>
 
<p>I was able to find this using two search methods.
</p>
<p>The first method <b>index=main sourcetype=access_combined (remove OR addtocart) status>=400</b>
</p>
<p align="center">
<img src="https://i.imgur.com/bVWeaJN.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
<br />
</p>

<p>The second method
</p>
<p><b>index=main sourcetype=access_combined (action=remove OR action=addtocart) status>=400</b>  
</p>

<p align="center">
<img src="https://i.imgur.com/RJsXWus.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
<br />
</p>

<p align="center">
Creating Dynamic and Interactive Dashboards <br/>
<p align="center"> 
  
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
  
<p>I used the following search <b>index=main sourcetype=access_combined | top limit=20 platform</b> after extracting a field based on the operating system name and labeling it as platform. Then I added  <b>showperc=f</b> in order to remove the pecent column from my table to allow for a cleaner view in the dashboard.
</p>

<p align="center">
Web Browsers with Most Failures: <br/>
<img src="https://i.imgur.com/OZstsnI.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 
  
<p>To report failures by web browser, I created the following filter <b>index=main sourcetype=access_combined status>=400</b> since status codes of 400 or greater indicate an error. Then I selected User Agent and Top Values by Time, and my new search was automatically updated to <b>index=main sourcetype=access_combined status>=400 | timechart count by useragent limit=10</b>.
</p>
<p>In order to keep a clean dashboard, I reduced the limit to 5 and added a filter removing browsers with a value of other, resulting in the updated search <b>index=main sourcetype=access_combined status>=400 | timechart count by useragent limit=5 useother=f</b>.
  
</p>

<br />

<p align="center">
<br />
Lost Revenue:  <br/>
<img src="https://i.imgur.com/APZuASl.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 

<p>I used the lookup command to extract product information from a csv file in the following search <b>index=main sourcetype=access_combined action=purchase | lookup product_codes.csv product_id</b>. In order to filter out failed purchase attempts, I updated to search to <b>index=main sourcetype=access_combined action=purchase status>=400 | lookup product_codes.csv product_id</b>. Finally, I added a sum function and timechart command to calculate the total number of failed purchases over the last 60 minutes, which was executed using the following search <b>index=main sourcetype=access_combined action=purchase status>=400 | lookup product_codes.csv product_id | timechart sum(product_price)</b>.
</p>

<br />

<p align="center">
<br />
Customer Locations:  <br/>
<img src="https://i.imgur.com/gIb1t6x.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 

<p>I created a cluster map using the following search <b>index=main sourcetype=access_combined | iplocation clientip | geostats count by City</b> in order to see all website traffic origins, where the iplocation and geostats commands were used to count the events by City. 
</p> 

<p align="center">
<br />
Challenge Task:  <br/>
<p>The map we’ve generated shows customers from all countries, but since Buttercup Enterprises is a US-based company, the Security team may only be interested in seeing customers who are NOT located in the US.</p>

<p>Q1. How would you update your search to remove events coming from “United States” from your map?
</p>
 
<p>To find customers from countries outside of the United States, the following command can be used <b>index=main sourcetype=access_combined | iplocation clientip | | search Country!="United States" | geostats count by City</b>. 
</p>

<p align="center">
<img src="https://i.imgur.com/KxpDPcU.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 


<br />

<p align="center">
<br />
<p>To demonstrate the dynamic dashboard, I have provided captures of information over different timeframes, as well as in light and dark mode.
</p>   
<p align="center"> 
Full Buttercup Enterprises Dashboard Over Last 60 Minutes:  <br/>
<img src="https://i.imgur.com/MlSQRTf.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>


 
<br />
<br />

<p align="center">
<br />
Full Buttercup Enterprises Dashboard Over Last 24 Hours:  <br/>
<img src="https://i.imgur.com/SjgoCIN.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 

<p align="center">
<br />
Dashboard in Dark Mode:  <br/>
<img src="https://i.imgur.com/zfdQUf4.png" height="80%" width="80%" alt="Creating Splunk Dashboard"/>
<p align="center"> 

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
