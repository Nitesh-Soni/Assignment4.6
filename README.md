1.If 7TB is the available disk space per node (9 disks with 1 TB, 2 disk for operating system etc. were excluded.). Assuming initial data size is 600 TB. How will you estimate the number of data nodes (n)?
Ans: 
h=crs/(1-i)
where: 
c = average compression ratio. It depends on the type of compression used and size of the data. When no compression is used, c=1. 
r = replication factor. It,s default value is 3
S = size of data to be moved to Hadoop. =600TB 
i = intermediate factor. It is usually 1/4.
h=1*3*600*(1-1/4)
h=2400
N= h/d
Where h = hadoop storage required =600TB
d= storage available each node = 7TB
N = number of data nodes
N= 2400/7
N=342.87
N ~ 343
Therefore,  the number of datanode required are 343.

2. .Imagine that you are uploading a file of 500MB into HDFS.100MB of data is successfully uploaded into HDFS and another client wants to read the uploaded data while the upload is still in progress. What will happen in such a scenario, will the 100 MB of data that is uploaded will it be displayed?
Default block size is  of 64 MB for Hadoop 1x and 128 MB for Hadoop 2x whereas, for the above scenario let us consider block size of 100 MB which means that we are going to have 5 blocks without replication. Let’s consider an example of how does a block is written to HDFS:

We have 5 blocks (A/B/C/D/E) for a file, a client, a namenode and a datanode. So, first the client will take Block A and will approach namenode for datanode location to store this block and the replicated copies. Once client is aware about the datanode information, it will directly reach out to datanode and start copying Block A. Once the block is copied, client will get the confirmation about the Block A storage and then, it will initiate the same process for next block “Block B”.

So, during this process if 1st block of 100 MB is written to HDFS and the next block has been started by the client to store then 1st block will be visible to readers. Only the current block being written will not be visible by the readers.
 

