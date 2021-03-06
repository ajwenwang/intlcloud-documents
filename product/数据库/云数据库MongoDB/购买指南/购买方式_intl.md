Log in to the [Tencent Cloud official website](https://cloud.tencent.com/), select MongoDB from the product menu (as shown below) and go to the [MongoDB Overview](https://cloud.tencent.com/product/mongodb) page.
Click **Get Started** to go to the [product purchase page](https://buy.cloud.tencent.com/mongodb).
Below are the descriptions of the main settings in the purchase page:
### Billing Options and Region ###
#### Billing Options ####
The prepaid (monthly/yearly subscription) and pay-as-you-go billing are supported. Pay-as-you-go might work best for you if your business is experiencing fluctuating traffic, unpredictable sales volume, or doing temporary urgent projects. Pay-as-you-go is postpaid, so the system will freeze your account credits for one hour cost of using the hardware when you create a database instance, and your account will be billed every hour on the hour (Beijing time, accurate down to the second). With pay-as-you-go, you only need to pay for what you use with no upfront payment required. The monthly subscription is prepaid and is suitable for businesses with long sale cycle stable traffic because it offers lower unit prices than pay-as-you-go. With prepaid plans, you pay in advance. You can choose to prepay for either one month/year or multiple months/years of the service to meet your business needs.
#### Region ####
Tencent Cloud managed data centers are distributed globally, spanning 4 regions in China (South China, East China, North China, and Southwest China), and more than 6 regions across the globe (Southeast Asia, Asia Pacific, Western U.S., Eastern U.S., North America, Europe, etc.). We are deploying more nodes to achieve higher global coverage. Available Regions include Guangzhou, Shanghai, Beijing, Chengdu, Chongqing, Hong Kong, Singapore, Seoul, Mumbai, Bangkok, Silicon Valley, Toronto, Virginia, Frankfurt, and Moscow. Available finance zones include Shenzhen Finance and Shanghai Finance.
Notes: 
While cloud products deployed within the same region can communicate with each other over the private network, the private networks for the resources in different accounts are completely isolated from each other.
Cloud products in different regions cannot communicate with each other over a private network.
Because each region is independent, cross-region access to Tencent Cloud resources is not supported through private networks.
When purchasing Tencent Cloud resources, we recommend you select a Region closest to your customers to minimize connection latency.
#### Availability Zones ####
In a Region, Availability Zones refer to Tencent Cloud physical IDCs with independent power facilities and networks. Availability Zones are designed to prevent single point failures (except for large-scale natural disasters or major power failures) from affecting other Availability Zones in the same region to ensure your business availability. Availability Zones in the same Region are connected via low-latency private networks.
### Basic Configurations ####
The basic configuration includes the configuration of server type, database version, storage engine, instance type, number of shard nodes, computing resource specification, and storage capacity. See below for details.
#### Configuration Types ####
Two types of models are available: High IO and High IO (10 GB).
#### Version ####
The version 3.2 is currently available and version 3.6 will be released soon.
#### Engine ####
TencentDB for MongoDB supports two storage engines: WiredTiger and Rocks.
#### Instance type and number of nodes ####
Instance types include replica set and sharding instances. For replica set instances, the "1 Master and 2 Slaves" architecture is configured by default. For sharding clusters, you can select the number of shards and the number of nodes in each shard as needed. Each shard has "1 Master and 2 Slaves" by default. To improve data availability, you can increase the number of nodes in each shard. To increase the storage capacity of the cluster, you can increase the number of shards.
#### Specification ####
The table below shows the available computation specifications for each node:
| CPU | MEM |
| 1 core | 2 GB |
| 2 cores | 4 GB |
| 4 cores | 8GB |
| 6 cores | 16GB |
| 12 cores | 32GB |
| 24 cores | 64GB |
| 24 cores | 128GB |
| 32 cores | 240GB |
#### Capacity ####
You can select storage specifications according to computation specifications. The storage space of Oplog is 10% of the configured storage capacity by default, while you adjust the percentage in Tencent Cloud Console.
### Network and Project ###
#### Network type ####
VPC networks and basic networks are supported. If you select a basic network, only devices in the basic network can access the database instances you created. If you select a VPC network, only devices in the current subnet can access the database instances you created.
#### Project ####
You can select a project based on your business needs.
### Purchase Quantity and Usage Period ###
#### Purchase quantity ####
Each user can purchase up to 10 monthly subscription instances, and up to 30 pay-as-you-go instances in all regions.
#### Usage period ####
With prepaid plans (monthly/yearly subscription), you can select a usage period of up to 3 years. We offer a variety of discounts for your purchase - the longer service period you sign for, the more discounts you will get: 12% off for usage periods more than 6 months, 60% off for 2-years usage periods, and 70% off for 3-year a usage periods.
