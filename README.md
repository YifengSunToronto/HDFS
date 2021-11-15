# HDFS
HDFS
Good for large data - Split file to smaller blocks and restored them in the same or different hosts. 
![image](https://user-images.githubusercontent.com/32372822/141703972-8af22114-5c54-4307-ac72-11cce366be7c.png)

![image](https://user-images.githubusercontent.com/32372822/141703998-0854b95d-b460-4e86-bb8c-e187899e039f.png)


![image](https://user-images.githubusercontent.com/32372822/141704580-e6503496-59af-4300-8544-c67500a8a9f0.png)
![image](https://user-images.githubusercontent.com/32372822/141704586-1a2c240a-1728-48ac-9d85-35e3a292e25f.png)


Why HDFS is Fault-tolarent?
It replicates data based on replicate factor - making # copies of data in other blocks
![image](https://user-images.githubusercontent.com/32372822/141704726-788432fa-846d-41c3-a5fd-453c6d73cf3a.png)

NameNode: Namespace image and Edit log are together used to maintain file history and where the data of file actually locates in the Datanode
User interacts with NameNode to get information of Datanode, then user get/write data directly to DataNode (to lower traffic of NameNode)

Note: NameNode is Single-Point-Failure. If NameNode fails, user cannot know where to find the actual data if FS. 
So we can 1. make backup copy (update multi NameNode in-parallel) 2. Use a lower NameNode - secondary node  3. StandyNameNode.

DataNode: Stores actual data in FS. 

-----------------------------------------------------

User Interaction with HDFS - Write / Read

Write:
User buffers and contacts NameNode -> NameNode returns user list of DataNodes for user to write to make up the file -> Data written to the 1st DataNode -> Data transferred to other Nodes.
![image](https://user-images.githubusercontent.com/32372822/141719315-32e4b83f-a127-48c2-ad80-ff7df35c1259.png)


Read:
User starts Read call to a NameNode -> NameNode returns DataNodes' addresses -> (If user is ran on a DataNode, then local copy of data will be used) -> User connects to nearst DataNode to stream data from the 1st block until the end block. (Seamless process / continuous streaming and the network call is handled by Hadoop - Hadoop does things for users!) 
If error/corruption happends, will try to read from another DataNode that has the copy of data. 

-----------------------------------------------------

Non-Functional

High-Availability:
Avoid Single-Point-Failure
Pssible SPF is NameNode as it's the early interface for both Write and Read.
So we need > 1 NameNode to handle all the associated requests. For the Idle NameNodes, they are the Standby NameNodes.
Standby NameNodes do not immediately take all actions as they are the active NaameNodes.
Alls actions taken by active NN is tracked by multiple JournalNodes. Active NN writes to JournalNode and there can only be 1 active NameNode does that at one time.
When failure happens, StandBy NameNodes copies actions that tracked by JournalNodes, then StandbyNN starts to work.
