## Microsoft Azure SOC and HoneyNet


<p align="center">
<img src="https://imgur.com/cW8RYr1.png alt="Traffic Examination"/>  
</p>



## Summary

For this project, I built a HoneyNet and SOC in Microsoft Azure. To accomplish this, I provisioned all of the resources necessary for a cloud infrastructure including virtual machines, flow logs for each VM, a log analytics workspace to ingest the log data, a key vault, a storage account, vnets, network security groups and a SIEM (Azure Sentinel). After provisioning, I left the resources exposed to the internet in order to gather attack data for 24 hours. The environment was then hardened and left on for another 24 hours. Finally, I gathered log data and created a spreadhseet to show the change in traffic patterns in the 24 hour period after the environment was hardened.
<br />
<br />


## Environments and Architecture Technologies Used

- Microsoft Azure (Cloud Platform)
  - Resource Groups
  - Azure Virtual Machines (2 Windows, 1 Linux)
  - Log Analytics Workspace
  - Azure Sentinel (SIEM)
  - Key Vault
  - Storage Account
  - Network Security Groups
  - Microsoft Defender for Cloud (Cloud-native Application Protection Platform (CNAPP))
  
 - Remote Desktop Protocol (Used for logging in to the VMs)
 - OSB Studio (For recording some my labs showcasing the procedures)
 
 ## Security Metrics Used for Queries in the Log Analytics Workspace
 
 - Syslog (For Linux Event Logs)
 - SecurityIncident (For Sentinel Created Incidents)
 - SecurityAlert (For Alerts Triggered in the Log Analytics Work Space)
 - AzureNetworkAnalytics_CL (For Malicious Events Triggered)
 - SecurityEvent (For Windows Event Logs)
 <br />
 <br />

</summary>
 
 
  ## Architecture Before Hardening
  
  Before hardening, all resources were exposed to the internet with public endpoints and the Network Security Group firewalls were wide open.
  <br />
  <br />
  ![Architecture Diagram](https://imgur.com/TcINeqM.png)
  <br />
  <br />
  
 ## Attack Maps Before Environment Hardening 
 These maps show malicious traffic attempting to penetrate the Azure environment before security controls were implemented. 
 
  ![Attack Map](https://imgur.com/JF0gqP9.png)
  <br />
  <br />
  ![Attack Map](https://imgur.com/86YhWnh.png)
  <br />
  <br />
  ![Attack Map](https://imgur.com/XJnrrgq.png)
  <br />
  <br />
  
  ## Metrics Before Implementing Security Controls
  
  The below table displays the metrics that were measured while the environment was insecure for 24 hours:
  
  ![Before Table](https://imgur.com/7TtL0tn.png)
  
  <br />
  <br />
  
  
  ## Architecture After Hardening
 
  
  After hardening, the VMs had their exposed ports (RDP/SSH) closed, the resources were all secured behind firewalls and a v-net with it's own network security group. Firewall rules were then set to only allow my workstation PC to access any of the resources in the environment for purposes of gathering log traffic data.
  <br />
  
  ![Architecture Diagram](https://imgur.com/ZBGHKPC.png)
  <br />
  <br />
  
   ## Metrics After Implementing Security Controls 
   
   The below table displays the metrics that were measured after the environment was hardened with security controls for 24 hours.
  
  ![After Table](https://imgur.com/u8PKIIQ.png)
  <br />
  <br />
  
 ## Rate of Change
 
 As can be seen in the below chart, the incidents dropped significantly when the environment was hardened. Had I ran the controls even longer no doubt the incidents would have decresed even more.
 
 ![Rate of Change Table](https://imgur.com/cQHeXFV.png)
 <br />
 <br />
 
 ## NIST Utilization as a Guideline for Security Controls


 ![NIST](https://imgur.com/eQ9x5ls.png)
 <br />
 <br />
 
 Utilizing the following steps, an organization handling any high priority incident can do so using the NIST 800-61 guide successfully:
 
 - Step 1: Preparation: (In this lab I prepared by setting up a log analytics workspace to log traffic coming into the HoneyNet, I configured Azure Sentinel (SIEM) and set up alerts to be triggered when incidents did occur.
 
 - Step 2: Assigning the incident to someone, setting the status (Low, Medium, High), inspecting the logs, investigating the incident to determine if it is a false positive or true positive and to determine the scope (it's affect on the environement or network).
 
 - Step 3: Using the Incident Response Playbook to catalog the details of the incident (basically the who, what, when, where, why and how) 
 
 - Step 4: Document the Findings and Close Out
 <br />
 <br />
 
 ## Cost Analysis
 
 ![Lab Cost](https://imgur.com/jN51Kle.png)
 <br />
 <br />
 
 My total cost for this excercise was about 30USD. Had I turned off my VMs nightly the cost would be less but the traffic would have stopped being ingested by the logs. The forecasted cost was $130USD had I left all of the resources running for one full month.
 <br />
 <br />  

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastially reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the given period of time following the implementation of the security controls.
