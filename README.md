# Azure HDInsight and Hortonworks Data Platform Comparison with Hive/HiveQL Tutorial

This is a comparison guide on the high-level differences between HDInsight and HDP as Hadoop services. There is a tutorial provided on the latter half of the guide on how to use Hive and HiveQL to analyze data from a text file using HDInsight and HDP. This is for the purposes of briefly introducing a way to use these systems and to provide resources to get started.

## Table of contents
* [Requirements](https://github.com/bkhong/HDInsight-vs-HDP#requirements)
* [Introduction](https://github.com/bkhong/HDInsight-vs-HDP#introduction)
* [Comparison](https://github.com/bkhong/HDInsight-vs-HDP#comparison)
* [HDInsight Hive and HiveQL Tutorial](https://github.com/bkhong/HDInsight-vs-HDP#hdinsight-hive-and-hiveql-tutorial)
* [HDP Hive and HiveQL](https://github.com/bkhong/HDInsight-vs-HDP#hdp-hive-and-hiveql)
   
## Requirements
  * Azure subscription or [30 day free trial account](https://azure.microsoft.com/en-us/free/)
  * [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
  * [Oracle JDK](http://www.oracle.com/technetwork/java/javase/downloads/index-jsp-138363.html)

## Introduction
### What is Hortonworks Data Platform?
**[Hortonworks Data Platform](http://hortonworks.com/products/data-center/hdp/)** (HDP) is an open source Hadoop distrubution that uses the [YARN operating system](http://hortonworks.com/apache/yarn/) and HDFS to manage on-premises data. It contains a variety of Apache processing engines to process data such as Hive, Tez, Storm, and Spark. 


### What is Azure HDInsight?
**[Azure HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/)** is an open source Hadoop service that is built on HDP that offers data clusters optimized for the cloud. Since it is backed by HDP, it contains much of the same functionality with some key differences. 

### On-Premises vs. Cloud Data
The primary difference between HDInsight and HDP resides in the way they store data. An organization with an **on-premises** data service stores data internally onsite. A **cloud** data service stores its data externally on public data servers. HDP is an on-premises service, while HDInsight is a cloud service.

## Comparison
### Summary of Differences
 | HDInsight | HDP
:---: | :---: | :---:
**Setup** | Simple: no download required | Complex: download required
**Operating Systems** | Any | Linux
**Data Storage** | Cloud | On-premises
**Entry Cost for Large Clusters** | Lower | Higher
**File Storage** | Azure Blob Storage | HDP File Store

### Advantages of HDInsight:
* Its **cloud storage capabilities**. The cost of entry to initialize large node clusters is significantly smaller if using cloud services. 
  * Building large node clusters with HDP would require a substantial amount of data center space, which raises the starting cost of building clusters. 
* **More cost efficient for smaller projects** than HDP's on-premises data service, since clusters can be deleted and usage is billed by the hour.
* **Automatic provisioning of clusters** allows HDInsight clusters to be more easily created.
* **Quick and easy setup**, only requires Azure subscription so it runs on any operating system. Since there is no need to download the service, **system memory is not an issue**. 
  * On HDP, the user would need access to a Virtual Machine if their native OS is not Linux, which is occassionally unreliable. **HDP has a higher entry barrier** since it is very technical to set up and is time consuming to do so. Since HDP is run locally, it subsumes a significant amount of system memory. 
* Access to **Azure Blob storage** and other Azure services.
* **Offers cluster scaling** which allows the user to change the number of nodes in a cluster without deleting it.
* Much more **throrough documentation and tutorials** than HDP, so it is more useful for beginniners and industry professionals alike.
* Azure platform offers **support for hybrid scenarios** through its HDP foundation and Analytics Platform System to link data from the cloud to on-premises, or moving on-premises data to the cloud. 

### Advantages of HDP:
* Its **on-premises data storage capabilities**. 
  * Offers **better security** for sensitive data than public cloud services. Users of HDP own the data they use in their local file system or data centers.
  * Cloud services make it difficult to pinpoint where data is located, and on-premises storage allows for better **data visibility**
  * Using private data centers and local file systems enables users to **control latency issues**, which overcomes latency in cloud services
* **More cost efficient for bigger, long-term projects**, since data center space that is built would accommodate clusters for cheaper over a long period of time
* Access to **HDP File Store**

## HDInsight Hive and HiveQL Tutorial
1. We will be using [this](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/data/Mass-Shooting-Data.txt) public mass shooting dataset. Download the file to your local drive.
2. Create an Azure storage account and pin the account to the dashboard. Here is a [guide](https://github.com/Microsoft/azure-docs/blob/master/articles/storage/storage-create-storage-account.md) that reviews this process.
![pintodashboard](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/pin_to_dashboard.png)
3. Click on the storage account from the dashboard to open it. Click on **Blobs**, then select the name of your storage account. You should see a list of default directories.
![blobs](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/blobs.png)
4. Click on the **example** directory, then click on the **data** directory. You should see a list of datasets with a variety of file types.
![exampleblob](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/example_folder.png)
![datablob](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/data_folder.png)
5. Click on **Upload** and select the data file from your local drive. Click **Upload** at the bottom of the window to upload the file. 
![upload](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/upload.png)
6. Verify that **Mass-Shooting-Data.txt** is in the **data** folder, then return to the Azure portal dashboard.
![datafolderwithdataset](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/data_folder_with_dataset.png)
7. Create a HDInsight cluster from the Azure portal. Microsoft documentation has a [guide](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-tutorial-get-started) that goes over cluster configuration. Pin the cluster to the dashboard for ease of access.
8. Click on the cluster from the dashboard, and select **Cluster Dashboard** from the **Quick links** section, then click **HDInsight Cluster Dashboard** to view the cluster through Ambari. Alternatively, the link **https://[ClusterName].azurehdinsight.net** will open Ambari, where [ClusterName] is the name of your cluster.
![clusterdashboard](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/cluster_dashboard.png)
9. Enter the cluster credentials specified when you first created the cluster (*not* the SSH credentials) with the default username **admin**.
10. Select **Hive View** from the header at the top of the page.
![hiveview](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/hive_view.png)
11. Paste the following HiveQL statements in the **Query Editor** section.

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
    SELECT * FROM shootingdata;
    ```

 The keywords perform the following:
  * **set hive.execution.engine=tez**: Sets the execution engine to use Tez, which increases query performance.
  * **DROP TABLE**: Prevents table conflicts if queried multiple times, this deletes the table and data file if the table already exists.
  * **CREATE EXTERNAL TABLE**: Creates a new external table that stores the columns and column names.
  * **ROW FORMAT**: Communicates to Hive about how the data is formatted and what the delimiters are.
  * **STORED AS TEXTFILE LOCATION**: Communicates to Hive where the text file is stored. The **wasbs:///** prefix is a relative path used when the file is in the default storage container for the cluster you are using.
  * **SELECT**: Selects all of the columns from the table.
12. Click **Execute**, and the **Query Process Results** section below the **Query Editor** will display the table after the query has finished processing. The data will look like this (some of the columns will not appear in this screenshot due to limitations on the browser width):
![selectall](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/select_all.png)
13. An example of a more specific query is provided below. This query requests for the day, city, and state of all the mass shootings with 10 or more casualties. Delete the previous statements from the **Query Editor** and paste the following statements. 

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

14. Click **Execute**, and the **Query Process Results** section will display the following table.
![select10ormore](https://github.com/bkhong/HDInsight-vs-HDP/blob/master/media/select_10_or_more.png)

## HDP Hive and HiveQL
To repeat the HDInsight HiveQL tutorial above on HDP, you will need to have HDP installed first. Follow this [guide](http://docs.hortonworks.com/HDPDocuments/Ambari-2.4.2.0/bk_ambari-installation/content/ch_Getting_Ready.html) for instructions on how to set up the Ambari server on your OS and how to create clusters on Ambari. If you have a non-Linux machine, you will need to download VirtualBox to use HDP. The process of querying data using Hive is identical to doing it on HDInsight since they both use the Ambari UI. The differences in using HDP instead of HDInsight are mainly in the way that the clusters are created on Ambari instead of on HDInsight's Azure interface, and files are uploaded to the HDP File Store instead of Azure Blob Storage.
