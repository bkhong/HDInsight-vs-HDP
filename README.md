# Azure HDInsight and Hortonworks Data Platform Comparison
<Add description>

## Table of contents

## Requirements
  * Azure subscription or [30 day free trial account](https://azure.microsoft.com/en-us/free/)
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Oracle JDK](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)

## Comparison
### What is Hortonworks Data Platform?
**Hortonworks Data Platform** (HDP) is an open source Hadoop distrubution that uses the YARN operating system and HDFS to manage on-premises data. It contains a variety of Apache processing engines to process data such as Hive, Tez, Storm, and Spark. 


### What is Azure HDInsight?
**Azure HDInsight** is an open source Hadoop service that is built on HDP that offers data clusters optimized for the Cloud. Since it is backed by HDP, it contains much of the same functionality with some key differences. 

### On-Premises vs. Cloud Data
The primary difference between HDInsight and HDP resides in the way they store data. An organization with an **on-premises** data service stores data internally onsite. A **cloud** data service stores its data externally on public data servers. HDP is an on-premises service, while HDInsight is a cloud service.

### Summary of Differences
 | HDInsight | HDP
--- | --- | ---
**Setup** | Simple-- no download required | Complex-- download required
**Operating Systems** | Any | Linux
**Data Storage** | Cloud | On-premises
**Entry Cost for Large Clusters** | Lower | Higher
**File Storage** | Azure Storage Blobs | HDP File Store

### Extended Comparison
Advantages of HDInsight:
* Its cloud storage capabilities. The cost of entry to initialize large node clusters is significantly smaller if using cloud services. Building large node clusters with HDP would require a substantial amount of data center space, and thus raises the starting cost of building clusters. 
* More cost efficient than HDP's on-premises data service, since clusters can be deleted and usage is billed per hour.
* Automatic provisioning of clusters allows HDInsight clusters to be more easily created.
* Easy and quick to set up, only requires Azure subscription so it runs on any operating system. Since there is no need to download the service, system memory is not an issue. On HDP, the user would need access to a Virtual Machine if their native OS is not Linux, which is occassionally unreliable. HDP has a higher entry barrier since it is very technical to set up and is time consuming to do so. Since HDP is run locally, it subsumes a significant amount of system memory. 
* Access to Azure Blob storage and other Azure services.
* Offers cluster scaling which allows the user to change the number of nodes in a cluster without deleting it.
* Much more throrough documentation and tutorials than with HDP, so it is more useful for beginniners and industry professionals alike.
* Azure platform offers support hybrid scenarios through its HDP foundation and Analytics Platform System to link data from the cloud to on-premises, or moving on-premises data to the cloud. 

Advantages of HDP:
* 




## Installation + code for HdInisght

## Sane with Hortonworks


