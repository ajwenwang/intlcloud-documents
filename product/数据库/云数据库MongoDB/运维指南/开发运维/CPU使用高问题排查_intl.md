If you find the CPU utilization is high when using MongoDB, you can troubleshoot the problem as follows.<br>
1. Check if your database operation is too frequently.
You can check the monitoring metrics on the console, as shown below. If the QPS is high, you may evaluate whether the instance needs to be upgraded. If the QPS is not high, check if there is any slow log.
![](https://main.qcloudimg.com/raw/e013e4387e144b8f98ab1de810503c0d.png)


2. Check if there is a slow log on MongoDB.
Log in to the [Console of TencentDB for MongoDB](https://console.cloud.tencent.com/mongodb) and view the slow log of the instance by using "Query statistics", as shown below.
![](https://main.qcloudimg.com/raw/19a7b1568cf38f6b493cb5088cfdff93.png)
Please pay attention to keywords such as command, COLLSCAN, IXSCAN, keysExamined and docsExamined.
 
 
 - command indicates the operations recorded in a slow log.<br>
 - COLLSCAN indicates a full table scan is performed. IXSCAN indicates an index scan is performed. For more information, please see [MongoDB official website](https://docs.mongodb.com/manual/reference/explain-results/index.html).<br>
 - keysExamined the number of index entries scanned. docsExamined indicates the number of documents scanned. Larger keysExamined and docsExamined values mean that no index is created or the index is less distinctive. Please confirm the fields for which an index is created.<br>
For more log descriptions, please see [MongoDB official website](https://docs.mongodb.com/manual/reference/log-messages/index.html).

