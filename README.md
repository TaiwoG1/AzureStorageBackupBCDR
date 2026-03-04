<h1>Azure Secure Storage & Business Continuity (BC-DR) Architecture</h1>


<h2>Description</h2>
This project demonstrates a comprehensive approach to Data Security and Availability within Microsoft Azure. I implemented a secure storage environment for both unstructured data (Blobs) and file-level data (Azure Files), protected by a Recovery Services Vault. The project covers the full data protection lifecycle: from restricting network access and automating data tiering to configuring cross-region replication for disaster recovery. 
<br />
<br />


<h2>Tools & Technologies:</h2>

- <b2> Cloud Provider: Microsoft Azure  </b2>
- <b2> Storage Services: Blob Storage (Hot/Cool/Archive), Azure Files </b2>
- <b2> Security: Storage Firewalls (VNet Integration), Network Security Groups (NSG)  </b2>
- <b2> Data Management: Lifecycle Management Policies, PowerShell Scripting  </b2>
- <b2> BCDR: Recovery Services Vault, Azure Backup, Site Recovery (Replication)  </b2>
- <b2> Connectivity: RDP, SMB 3.0 Protocol  </b2>
</b2>


<h2>Architecture & Key Features:</h2>

- <b2> Network-Hardened Storage (Identity & Access):
I secured the storage account by disabling public access and permitting only "Selected Networks." To verify the security posture, I attempted to access the data from an unauthorized network, which resulted in a not authorized response. </b2> 
  <p align="center">
    <img width="960" height="434" alt="7f - access allowed into container since configuration allows access from all network" src="https://github.com/user-attachments/assets/2024e679-cb85-4089-b641-b30df62c7128" />
      <br />
    User access granted from external networks prior to the enforcement of access for only Select Network
    <br />
  </p>

  <p align="center">
    <img width="960" height="439" alt="7f - enable public network access from only select virtual networks 1" src="https://github.com/user-attachments/assets/ea0dfc7b-ac5f-4501-8957-01f855f010fb" />
<br />
    User access restriction rule configuration for only select networks
    <br />
  </p>

  <p align="center">
    <img width="960" height="433" alt="7f - f access denied into container since it is not in the selected virtual network" src="https://github.com/user-attachments/assets/d3dc4df3-9216-4a43-90c1-e2c7409a8966" />
      <br />
    User access denied from an unapproved network
    <br />
  </p>


- <b2> Azure Files & SMB Implementation:
I deployed an Azure File Share and configured the environment to allow SMB (Port 445) traffic. Using an Azure VM and a PowerShell mounting script, I mapped the file share as a network drive (S: Drive) to simulate a real-world corporate file-server environment. </b2>
  <p align="center">
    <img width="960" height="507" alt="7h - script executed and showing file share successfully on vm file explorer" src="https://github.com/user-attachments/assets/b606a078-1cc6-4f27-8627-a28a5ace0d4e" />
      <br />
     File share successfully mapped as a network drive on the Virtual machine
    <br />
  </p>


- <b2> Automated Data Lifecycle Management:
To optimize costs, I implemented Lifecycle Management rules. These rules automatically transition data from the Hot tier to the Archive tier and handle automated deletion based on the object's age. </b2>
  <p align="center">
    <img width="960" height="490" alt="7c - create lifecycle management rule for container in storage account (tiers changing)" src="https://github.com/user-attachments/assets/089348bf-a8f7-4394-9d18-265a9b68937b" />
      <br />
    Lifecycle Management Rule Logic
    <br />
  </p>

- <b2> Recovery Services Vault & Backup Operations:
I centralized all backup activities in a Recovery Services Vault (RSV).
  - <b2> VM Backup: Configured backup policies for the compute layer. </b2>
  - <b2> On-Demand Protection: Executed "Backup Now" operations to ensure an immediate recovery point was created. </b2>
  - <b2> Hybrid Readiness: Explored the integration for on-premises machine backups, showcasing the scalability of Azure's backup solutions. </b2>
  <p align="center">
    <img width="960" height="280" alt="9e - successful vm backup complete" src="https://github.com/user-attachments/assets/66d96bea-22a9-4bcc-bd08-c64578b3c86e" /> <br />
    Recovery Services Vault Overview & Backup Progress
    <br />
  </p>

- <b2> Disaster Recovery (Replication)
I configured a Replication Policy to ensure Business Continuity. By replicating resources to a secondary region, the infrastructure is prepared for a regional outage. I verified the failover settings to ensure a low Recovery Time Objective (RTO). </b2>


<h2>Lesson Learned:</h2>

- <b2> Importance of Ports: Enabling SMB (Port 445) is a prerequisite for Azure Files, and managing this via NSGs is critical for secure connectivity.</b2>
- <b2> Recovery vs Replication: Gained a deep understanding of the difference between Backups (Point-in-time recovery) and Replication (Immediate failover for continuity). </b2>
- <b2> Cost Governance: Discovered how Lifecycle Management policies directly impact the cloud bill by automating the use of cheaper (Archive) storage for old data. </b2>
- <b2> Defense-in-Depth: Verified that combining VNet service endpoints with IAM roles creates a layered security model that is much harder to breach than a single firewall. </b2>
</b2>


<h2>Summary</h2>
This project showcases the ability to manage data throughout its entire lifecycle, from secure creation and daily usage to long-term archiving and emergency recovery. It demonstrates the technical proficiency required to maintain high availability in a modern enterprise cloud environment. <br />

For a detailed breakdown of the technical implementation, specific configurations, and in-depth analysis, please refer to the [Full Project Report](https://github.com/TaiwoG1/) <br />
