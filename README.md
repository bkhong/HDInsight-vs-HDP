# Azure HDInsight and Hortonworks Data Platform Comparison with Hive and HiveQL Tutorial
<Add description>

## Table of contents

## Requirements
  * Azure subscription or [30 day free trial account](https://azure.microsoft.com/en-us/free/)
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Oracle JDK](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)

## Introduction
### What is Hortonworks Data Platform?
**Hortonworks Data Platform** (HDP) is an open source Hadoop distrubution that uses the YARN operating system and HDFS to manage on-premises data. It contains a variety of Apache processing engines to process data such as Hive, Tez, Storm, and Spark. 


### What is Azure HDInsight?
**Azure HDInsight** is an open source Hadoop service that is built on HDP that offers data clusters optimized for the Cloud. Since it is backed by HDP, it contains much of the same functionality with some key differences. 

### On-Premises vs. Cloud Data
The primary difference between HDInsight and HDP resides in the way they store data. An organization with an **on-premises** data service stores data internally onsite. A **cloud** data service stores its data externally on public data servers. HDP is an on-premises service, while HDInsight is a cloud service.

## Comparison
### Summary of Differences
 | HDInsight | HDP
:---: | :---: | :---:
**Setup** | Simple-- no download required | Complex-- download required
**Operating Systems** | Any | Linux
**Data Storage** | Cloud | On-premises
**Entry Cost for Large Clusters** | Lower | Higher
**File Storage** | Azure Blob Storage | HDP File Store

### Advantages of HDInsight:
* Its **cloud storage capabilities**. The cost of entry to initialize large node clusters is significantly smaller if using cloud services. 
  * Building large node clusters with HDP would require a substantial amount of data center space, which raises the starting cost of building clusters. 
* **More cost efficient for smaller projects** than HDP's on-premises data service, since clusters can be deleted and usage is billed per hour.
* **Automatic provisioning of clusters** allows HDInsight clusters to be more easily created.
* Easy and **quick to set up**, only requires Azure subscription so it runs on any operating system. Since there is no need to download the service, **system memory is not an issue**. 
  * On HDP, the user would need access to a Virtual Machine if their native OS is not Linux, which is occassionally unreliable. **HDP has a higher entry barrier** since it is very technical to set up and is time consuming to do so. Since HDP is run locally, it subsumes a significant amount of system memory. 
* Access to **Azure Blob storage** and other Azure services.
* **Offers cluster scaling** which allows the user to change the number of nodes in a cluster without deleting it.
* Much more **throrough documentation and tutorials** than with HDP, so it is more useful for beginniners and industry professionals alike.
* Azure platform offers **support for hybrid scenarios** through its HDP foundation and Analytics Platform System to link data from the cloud to on-premises, or moving on-premises data to the cloud. 

### Advantages of HDP:
* Its **on-premises data storage capabilities**. 
  * Offers **better security** for sensitive data than public cloud services. Users of HDP own the data they use in their local file system or data centers.
  * Cloud services make it difficult to pinpoint where data is located, and on-premises storage allows for **data visibility**
  * Using private data centers and local file systems allows users to **control latency issues**, which overcomes latency in cloud services
* **More cost efficient for bigger, long-term projects**, since data center space that is built would accommodate clusters for cheaper over a long period of time
* Access to **HDP File Store**

## HDInsight Hive and HiveQL Tutorial

1. We will be using [this](/.data/Mass-Shooting-Data.txt) public mass shooting dataset. Download the file to your local drive.
2. Create an Azure storage account and pin the account to the dashboard. There is a GitHub [guide](https://github.com/Microsoft/azure-docs/blob/master/articles/storage/storage-create-storage-account.md) that reviews this process.
![pintodashboard](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/pin_to_dashboard.png)
3. Click on the storage account from the dashboard to open it. Click on **Blobs**, then select the name of your storage account. You should see a list of default directories.
![blobs](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/blobs.png)
4. Click on the **example** directory, then click on the **data** directory. You should see a list of datasets with a variety of file types.
![exampleblob](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/example_folder.png)
![datablob](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/data_folder.png)
5. Click on **Upload** and select the data file from your local drive. Click **Upload** at the bottom of the window to upload the file. Verify that **Mass-Shooting-Data.txt** is in the **data** folder, then return to the Azure portal dashboard.
![upload](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/upload.png)
![datafolderwithdataset](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/data_folder_with_dataset.png)
6. Create a HDInsight cluster from the Azure portal. Microsoft documentation has a [guide](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started) that goes over cluster configuration. Pin the cluster to the dashboard for ease of access.
7. Click on the cluster from the dashboard, and select **Cluster Dashboard** from the **Quick links** section, then click **HDInsight Cluster Dashboard** to view the cluster through Ambari. Alternatively, the link **https://[ClusterName].azurehdinsight.net** will open Ambari, where [ClusterName] is the name of your cluster.
![clusterdashboard](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/cluster_dashboard.png)
8. Enter the cluster credentials specified when you first created the cluter (*not* the SSH credentials) with the default username **admin**.
9. Select **Hive View** from the header at the top of the page.
![hiveview](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/hive_view.png)
10. Paste the following HiveQL statements in the **Query Editor** section.
```sql
set hive.execution.engine=tez;
DROP TABLE shootingdata;
CREATE EXTERNAL TABLE shootingdata (day string,
city string,
state string,
injured int,
killed int,
lat double,
lng double)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS TEXTFILE LOCATION 'wasbs:///example/data/';
SELECT day, city, state FROM shootingdata 
WHERE INPUT__FILE__NAME LIKE '%Mass-Shooting-Data.txt'
AND shootingdata.injured + shootingdata.killed >= 10;
```

## Same with Hortonworks


