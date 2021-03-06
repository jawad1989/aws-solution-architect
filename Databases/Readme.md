
Table of Contents
### 1. RDS
### 2. Non RDS
### 3. Data Warehousing
### 4. ElastiCache
### 5. Lab
  ## 5.1. Create a RDS isntance
  ## 5.2. RDS Backups, Multi-AZ and Read Replicas
  
***************************

## 1.  RDS
* You cant ssh into RDS
* Max retention period 35 days
* RDS is not serverless, aurora serverless is serverless
* Backups:
  * Auto backups are enabled by default
  * back data is stored in S3
  * if RDS is of 20 GB back up will be of 20 GB
* Snapshots:
  * Are done manually
  * stored even after you delete the original RDS instance
  
 
> Whenever you retore a Restored backup or manual snapshot, the restored version will be a new RDS instance with new DNS end point

### Aurora
  * is a RDMS that combines speed and availibiiity of high end commercial DBs with cost effectiveness
  * 5 times better than MYSQL
  * 3 times better than Postgress
  * start with 10 GB, scales in 10GB increments to 64 TB
  * Compute resources can scale upto 32 vCPUs and 244 Gb memoery
  * 2 copies of your DB is contained in each AZ, with minimum 3 AZ. Total 6 copies
  * upto 15 replicas, where MYSQL allow upto 5 replicas, Postgress allow upto 1
  * In region replication only, where MYSQL cross Region
  * Automated failover is only available for only aurora
  
  #### Aurora SERVERLESS
   * is an on demand autoscaling configuration for the Aurora. 
   * Auroa Serverless DB Cluster automatically starts up, shuts down and scales capacity up or down based on yur app's need
   * for infrequent, intermittent and un predecitable workloads 
   
   
  
  
### RDS Two features

  1. Multi AZ - for Disaster Recovery  
     * Primary and secondary
     * failover is automatic
  
  2. Read Replicas - for performance 
      * Write on one DB1 is copied on DB2
      * For Read you can point your db
      * upto 5 read replicas of one DB
      * you can have read replicas in a second region
      * Backups should be ON for activating read replicas

### * Types of RDS Databases
  1. MYSQL
  2. MariaDB
  3. SQL Server
  4. Postgress
  5. Aurora
  6. Oracle
 

## 2. Non Relational Datbases
 * Dynamo DB
   * supports both document and key/value data
   * SSD Storage
   * Spread across 3 geographically distinct data centres
   * Evemtual Consistent Reads(Default)
      * Best Read Performance - consistency for all copies of data is usually reach within ***one second***
      * Repeating a read after short time 
   * Strongly Consistent Read
      * returns a result the reflects all writes that received a response prior to read (less than one second)
   
   Collection     = Table
   Document       = Row
   Key Value Pair = Fields
   
   Components:
    * Tables
    * Items (like rows) ( stored as JSON) ( made up of Key value pairs)
    * Attributes ( columns)
    * key= name of data, Value = the data iteself
    * Documents can be in JSON,XML,HTML
    * can have as many cols against a row
    
    DAX ( Dynamo DB Accellorator)
      * fully managed, clustered im memory cahce for dynamo DB
      * delivers upto 10x read performance
      * micro second performance
      * use cases: auction apps, gaming apps, retail sites using black froday
      * Write Thorough caching:   data is written in cache along with back end store at same time
      * Suitable for eventual consistent read only, not strong consisten read
      * not suitable for write intensive apps,
    Primary Keys:
      * sores/retrieved data using PK
      * 2 types:
        * partition key: 
          * unique attribute e.g. User ID
          * value of PK is input to internal hash function which determine the partition/physical location of data
          * no 2 items can have same partition key
        * Composite Key: (PK + Sort Key)
          * e.g. same user posting multiple times to a forum
          * PK would be a composite key made up of ( Partition key(userID) + SortKey(TimeStamp) 
          * 2 items may have the same PK
          * all items with same PK are stored together, then sorted according to sort key value
          * can store multiple items with same partition key
   
## 3. Data Warehousing
  * OLTP 
    * Online Transaction Processing: pulls up a row of such as Name, Date, Address etc
  
  * OLAP
    * Online Analytics Processing: Sum of Radios sold in Asia, USA, cost of radio in each region
      * Pulls large number of records
  
  * Redshift: Data warehousing solution or business intelligence
    * can scale to petabytes or more
    * only available in 1 AZ
    * less the 1/10th compared to other DWH solutions
    * Can be configured as
      * Single Node(160 GB)
      * Multi Node (leader/Computer Node)
    * Advanced Compression: compress individual columns
    * MPP: Massively Parallel Processing
    * Backups: Enabled by default, Max retention period 35 days
    * you are billed for 1 unit per node per hour
      * a 3 node DWS cluster running for a month would cost 2160 hours =(30 days * 24 hours * 3 Nodes)
      * will not be charged for leader node, only compute nodes will be charged
      
## 4. ElastiCache
  * webservice that makes it easy to deploy, operate and scale in memory cache in cloud
    e.g. most queried information in cache e.g. top most purchased item today in amazon tech department
  * used to speed up performance of existing databases( frequent identical queries) and web apps
  * Supports 2 open-source in-memory caching engines:
     1. Redis
      * advanced datatypes, multi Az, backup/restore
     2. Memcached
      * simple cache, easy to get started



# Questions

* RDS Reserved instances are available for multi-AZ deployments. = True

* With new RDS DB instances, automated backups are enabled by default. = True

* If I wanted to run a database on an EC2 instance, which of the following storage options would Amazon recommend?  = True

* If you want your application to check RDS for an error, have it look for an ___ERROR___ node in the response from the Amazon RDS API.

* Which AWS DB platform is most suitable for OLTP? = RDS

* If you are using Amazon RDS Provisioned IOPS storage with a Microsoft SQL Server database engine, what is the maximum size RDS volume you can have by default? 16 TB

* You are hosting a MySQL database on the root volume of an EC2 instance. The database is using a large number of IOPS, and you need to increase the number of IOPS available to it. What should you do?  add 4 additional EBS SSD vols and create  a raid 10 using these vols

* Technically a destination port number is needed, however with a DB security group the RDS instance port number is automatically applied to the RDS DB Security Group
