# Sharding and Partitioning

It is a very useful and crucial concept and comes in handy when we want to scale our database.

**Sharding**: method of distributing data across multiple machines. 

**Partinioning**: splitting  a subset of data within the same instance/container/server/machine/database. 

## How a database is scaled?
A database server is just a database process (MySQL, MongoDB) running on an EC2 machine. 

<img width="285" alt="Screenshot 2024-04-06 at 11 18 40 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/310497bf-edf2-4273-898c-51920d1de506">

Let's take an example to understand it:

Let's say we have a service running in production and is serving real traffic. We're getting more users day by day that our DB is unable to manage. So, to solve this, we scale up our DB, as of course, we don't want to lose our customers and make an excuse as the request would start taking more time to send a response, and in some instances, it may start failing. To resolve this, we'll have to scale our DB (verticle scaling) and give it more CPU, RAM, and Disk.

Before scaling:

<img width="389" alt="Screenshot 2024-04-06 at 11 10 28 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/c7295737-b256-4bc9-8810-6b73ec2adb16">


After scaling: say we have more reads in the database as compared to writes. so in that case, a read replica can be created which will serve the read requests and write and other complex read requests will be served by the normal server. 

<img width="389" alt="Screenshot 2024-04-06 at 11 10 40 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/3406e7cf-3102-42fd-8166-1bd9d538e487">

(Bulkier Server + Read Replica)

But, as we made a very good service and our product went viral. Our bulky DB is unable to handle the load, so we scale up again. But, after a certain stage, vertical scaling will not work as it has its limits. so we'll have to start the horizontal scaling. Say, one DB server was handling 100 WPS and we cannot scale up beyond that but we are getting 1050 WPS, we can scale horizontally and split the data.

<img width="338" alt="Screenshot 2024-04-06 at 11 22 25 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/7f50410c-217b-47cc-8049-d7f24788a775">

By Adding one more Database server, we reduced the load to 750 WPS on each node and thus higher throughput.
<img width="338" alt="Screenshot 2024-04-06 at 11 27 42 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/5dff977d-32fa-42ba-a981-9da1b74593b3">

Each database server is thus a shard and we say that data is partitioned.


Here, we partitioned the 100 GB of total data into 5 mutually exclusive partitions.
Each of these partitions can either live on one database server or a couple of them can share one server. And this depends on the number of shards we have.
<img width="338" alt="Screenshot 2024-04-06 at 11 39 10 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/1efcc812-34d0-43eb-be51-96d218fb71b0">

<img width="627" alt="Screenshot 2024-04-06 at 11 49 35 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/5cf96069-7ddf-4aac-96ac-6e8497b41e51">

POV: Increasing CPU/Memory resources within the existing containers is verticle scaling. Since, vertical scaling has its limit so after a certain point we cannot increase the limit, in that case, horizontal scaling comes into play.

Sharding is increasing the machines/databases to increase the reads or writes. Here, we are distributing the data across multiple machines. 

## How a Partition the Data?

There are two types of partitioning:-
1) Horizontal Partitioning
2) Vertical Partitioning
It depends upon the load, use cases, and access pattern.

## Advantages of sharding

- Handle large Reads and writes
- Increase overall storage capacity
- Higher availability 

## Disadvantages of sharding
- Operationally complex
- cross-shard queries expensive 




All Duahrams are made using **LucidCharts**
