# HDFS
HDFS
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
![image](https://user-images.githubusercontent.com/32372822/141719315-32e4b83f-a127-48c2-ad80-ff7df35c1259.png)

