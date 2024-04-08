# System design for karat interview
1. A music streaming service such as Spotify is deployed to multi servers. What are pros and cons?
这道题本质上是答分布式系统优缺点，我总结的有点长，面试答上其中一部分就可以。
   1. Advantages  
      1. Low latency than a centralized system – Distributed systems have low latency because of high geographical spread, hence leading to less time to get a response.
      1. Scalability: Distributed systems are highly scalable as they can be easily expanded by adding new nodes to the network. This allows the system to handle a large amount of data and traffic without compromising on performance.
      1. Fault tolerance: Distributed systems are fault-tolerant, meaning they can continue to function even if some nodes fail or go offline. This is because the workload is distributed among multiple nodes, so the system can continue to operate even if some nodes are down.
      1. Increased reliability: With multiple nodes in the network, distributed systems are more reliable than centralized systems. Even if one node fails, there are still other nodes that can provide the required service.
      1. Cost-effective: Distributed systems are often more cost-effective than centralized systems, as they can be built using off-the-shelf hardware and software components. This makes them a more affordable option for many organizations.
      1. Improved performance: Distributed systems can achieve higher performance by using parallel processing techniques, where tasks are split among multiple nodes in the network, and each node processes its share of the workload simultaneously. This can significantly reduce processing time and improve overall system performance.
   1. Disadvantages
      1. Network complexity: Distributed systems require a complex network infrastructure to operate, which can be difficult to set up and maintain. Network outages and bottlenecks can cause system failures and data loss.
      1. Security challenges: Distributed systems can be vulnerable to security threats such as cyber-attacks, data breaches, and unauthorized access. It can be challenging to implement robust security measures across all nodes and ensure data privacy and integrity.
      1. Synchronization issues: Data consistency and synchronization across all nodes can be a challenge, especially when multiple users are accessing the system concurrently. Ensuring data consistency and avoiding data conflicts requires complex algorithms and protocols.
      1. High development and maintenance costs: Distributed systems require specialized skills and expertise to design, develop, and maintain. This can lead to high development and maintenance costs, especially for large-scale systems.      
1. Load balance stragety  
   Question: The interview gave a scenario for Google docs and multiple users can access the same document, and google docs uses a Round Robin load balancing approach. Do you see any issues with using such an approach
    
   round robin的问题是可能某个服务器处理的请求远多于其他服务器，所以可以讲下其他的负载均衡策略。
    1. Round robin: Round robin load balancing distributes traffic to a list of servers in rotation using the Domain Name System (DNS). An authoritative nameserver will have a list of different A records for a domain and provides a different one in response to each DNS query.
    1. Weighted round robin: Allows an administrator to assign different weights to each server. Servers deemed able to handle more traffic will receive slightly more. Weighting can be configured within DNS records.
    1. IP hash: Combines incoming traffic's source and destination IP addresses and uses a mathematical function to convert it into a hash. Based on the hash, the connection is assigned to a specific server.  
   Dynamic  
      1. Least connection: Checks which servers have the fewest connections open at the time and sends traffic to those servers. This assumes all connections require roughly equal processing power.
      1. Weighted least connection: Gives administrators the ability to assign different weights to each server, assuming that some servers can handle more connections than others.
      1. Weighted response time: Averages the response time of each server, and combines that with the number of connections each server has open to determine where to send traffic. By sending traffic to the servers with the quickest response time, the algorithm ensures faster service for users.
      1. Resource-based: Distributes load based on what resources each server has available at the time.

1. Database sharding  
   Add cache; Hot shard, split into smaller ones; Shard by hash;
   1. Data redistribution: Balancing the workload by redistributing data across partitions based on access patterns or key ranges. This can be achieved by repartitioning the data or using techniques like consistent hashing.
   1. Caching: Implementing caching mechanisms, such as in-memory caches, to alleviate the load on the hot partition by serving frequent read requests directly from memory.
   2. Query optimization: Analyzing and optimizing queries that contribute to the hot partition problem. This can involve query rewriting, indexing, or restructuring the schema to reduce the concentration of access on specific partitions.
   1. Scaling resources: Adding more computational resources or nodes to handle the increased workload on the hot partition. Scaling horizontally by adding more nodes can help distribute the load more evenly.
   1. Monitoring and automation: Continuously monitoring the system's performance, identifying hot partitions, and applying automated mechanisms for workload redistribution or resource allocation as needed.

1. Client side vs server side analytics
   1. Advantages of server side
      1. Servers can be set up with infinitely more power than desktop machines and so can crunch "the big numbers".

      1. Performance can be more predictable as the same machines are used for everyone's analysis and generation of results.

      1. Output will not have dependencies on browser / browser version as they just have to display an image.

      1. More reliable
   1. Client-side Advantages
      1. If the number of clients is large, say thousands per minute, it can be good to unload the processing to client machines to avoid having them slow down a central server.
      2. Cheaper Server-side infrastructure will not be needed and so will not cost (the provider) money.
      3. Easy to implement
1. Web service slow why & solution?
   1. Network latency  
      To reduce network latency, you can use techniques such as compression, caching, content delivery networks (CDNs)
   1. Server load  
      To reduce server load, you can use techniques such as load balancing, scaling, caching, and performance monitoring.  
   1. Database performance  
      To improve database performance, you can use techniques such as normalization, indexing, caching, query optimization, and sharding.

1. 如何降低一个短视频共享服务(类似snap)的server cluster 费用
   1. Only serve the most popular videos from CDN and other videos from our high capacity storage video servers
   2. For less popular content, we may not need to store many encoded video versions. Short videos can be encoded on-demand.
   3. Some videos are popular only in certain regions. There is no need to distribute these videos to other regions.
1. 视频共享系统升级来handle 未来不断增加的流量，预算需要考虑哪些因素
   1. Understand requirement
      1. Number of users
      2. Videos to share
      3. Video size
      4. Video Quality
      5. Server type: Whether you choose on-premise, cloud-based, or hybrid, servers can significantly impact the overall cost
   1. Hardware and Software Costs
   2. Bandwidth Costs
   3. Maintenance and Update Costs  
      Electricity and cooling
1. 一个类似Facebook的app。我们现在加个功能：在每个帖子上显示多少friends查看了该帖子。怎么设计这个功能
   Use distributed counter,
   1. Decide the number of shards based on followers
   2. When write reqeust comes, send it to a shard counter maybe using round robin
   3. Merge all the counter together and save to cache
   4. Display cached result
   5. After a while when the tweet is less popular, decrease number of shards
1. Design a smart refrigerator
   1. Potential Users Household, Restaurant, Grocery Store
   2. Key features
      1. Identify all the items that are put into the fridge
      1. Auto ordering certain ‘regular’ supplies when they are likely to run out. Milk, essential groceries, baby products etc. Saves time thinking about these products and investing time into ordering them.
      1. Alerting when certain produce is about to expire. Helps reduce wastage and saves money
      1. Alerting when an expired product is taken out of the fridge. Prevents accidental illness which could otherwise have been caused by eating expired food, particularly certain medicines!
      1. Help achieve fitnes goals by tracking their usage of certain fitness products

1. Estimate storage needed for a system that can store logs, and search logs.
2. There is a system for file uploading and sharing. When uploading a file, to remove duplicate, that file is checked against all the files uploaded already. If the files are of same size, then the files are compared bit by bit. How to improve the system to make it more efficient?
1. There is a new kind of game machine, which users can retrieve left credits from previous play, or connect to credit cards, to play a new game. Say now there are 100,000 machines setup globally, what would be the concerns on such system?
1. If you are building a web-based password validation system, with some password restrictions (such as English characters only, 8-16 length, at least 1 upper, 1 lower, 1 symbol) - what would be your concern on building such system?

1. We are working on a service that generates subtitles for users' videos. This process starts a new thread for every video and is processor-intensive. Currently, this service runs as a single process on a machine.We've run into a bug where if the service is processing more than 10 videos at the same time, the service crashes the server, losing all requests currently being processed and affecting other processes on the machine. It may take a long time to find and fix this bug. What workarounds could we implement to continue running the service while we do so?

1. We are working on a mobile app for the board game Go. We'd like to add a feature where the computer will analyze a completed game. The analysis looks at each position from the game and provides suggested moves to help improve our users' play. We've found a library we can use to do this analysis. It takes an average of a minute on a modern desktop computer to analyze an entire game. An average game consists of about 200 moves.We are considering two approaches. 1) running this analysis on the phone itself, and 2) sending the game to a server farm for analysis that will be returned to the user.What are some advantages or disadvantages of each approach?
   
1. You're working on infrastructure for internet-connected vending machines. The plan is to install around 100,000 of these vending machines in the coming year, in major cities around the world. These machines will connect to the internet through cellular devices. Each machine will connect to a central server at midnight to report remaining stock and any maintenance issues like coin jams or stuck items. These machine status updates will be stored in a database, and a batch job will run at 1 AM to schedule the restocking and maintenance of machines.Are there any problems with the above design?
   
1. We are running a simple photo storage and sharing service. People upload their photos to our servers and then give links to other users who can then view them. Instead of using a cloud service, we have our own server farms.  You've been tasked with creating an estimate of the storage required over the coming year and the cost of that storage. What information would you need and what factors would you consider as you generate this estimate?

1. We are running a simple photo storage and sharing service. People upload their photos to our servers and then give links to other users who can then view them. We're trying to figure out how to split the photos and associated data evenly onto multiple machines, especially as we get new users. We've decided to shard the photos evenly alphabetically by username. For example, if we had 26 servers, all the usernames starting with 'a' would be on server 1, usernames starting with 'b' would be on server 2, and so on. We have created a scheme like this that will work for any number of servers. Are there any problems with this design and how to solve it?

1. 什么是Strong consistence, eventually consistence，下面三种情况各适用哪种consistence?
    - api request 20 milliseconds, get metadata of media files     - analytics application     - bank system

1. Doc需要很多人电子sign，sign完后会自动发送notification，每 个doc都有一个ID。现在由于bug导致只有50%的notification被发送，500个server上每个 server都有发送notification的log，log包括成功发送的docID。DB里有所有需要发送notification的doc信息，问怎样把没发的notification发出去? 要求解决方法 scalable
