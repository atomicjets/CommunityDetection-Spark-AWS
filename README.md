# CommunityDetection-Spark-AWS

A Spark application, written in Python, to figure out strongly connected components with Bi-directional Label Propagation algorithm.

This project implemented an 1.2GB Twitter network dataset by AWS EMR cluster. 

## How to replicate the experiment
   - Upload labelp.py and dataset to your bucket in AWS S3. (if you already have an [**AWS account**][AWS account])
   
   - Create a cluster in AWS EMR. </br>
   
     - Launch mode : `Step execution` (You can also choose `Cluster` and use `SSH` to connect your cluster.) </br>
     
     - Step type : `Spark application` </br>
       (configure) </br> 
       Name : `labelp` </br> 
       Deploy mode : `cluster` </br>
       Spark-submit options : `--driver-memory 10g --executor-memory 5g` . Without setting memory, application may fail for memoryoverhead. (For more details : [**Running Spark on Yarn**][Running Spark on Yarn])</br>
       Application location : choose your `labelp.py` in S3 </br>
       Action on failure : `Terminate cluster` (Recommended) </br>
    
     - Vendor : `Amazon`, Release : `emr-5.2.0` (If you choose `Cluster` mode before, choose Application : `Spark: Spark 2.0.2...`.) </br>
     
     - Instance type : `m1.xlarge` </br>
       Number of instances : `7` </br>
       (You can use other type and number of instances, but make sure that your total memory is larger than 66G, which was observed as the maximum memory used during the process.) </br>
       
     - Permission : `Default` </br>
       (If you choose `Cluster` mode before, upload your public key to AWS and select it here) </br>
       
     - Click `Create cluster` button. </br>
       Done! </br>
       Your cluster will be terminated automatically after the application is finished.
 
[AWS account]:https://aws.amazon.com/
[Running Spark on Yarn]:http://spark.apache.org/docs/latest/running-on-yarn.html

## Where to find the dataset I used

[**Dataset : Twitter**][Dataset : Twitter] </br>
R. Zafarani and H. Liu, (2009). Social Computing Data Repository at ASU [http://socialcomputing.asu.edu]. Tempe, AZ: Arizona State University, School of Computing, Informatics and Decision Systems Engineering

[Dataset : Twitter]:http://socialcomputing.asu.edu/datasets/Twitter

## Results
format : `('label',u'CommunitySize/Members')` </br>
See [**output-spark**][output-spark] folder.

[output-spark]:https://github.com/linghaol/CommunityDetection-Spark-AWS/tree/master/output-spark

## 
