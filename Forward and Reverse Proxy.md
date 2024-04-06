# Proxy, Forward Proxy, and Reverse Proxy

A proxy is a machine or set of machines that sits in between two systems. 

## Forward proxy
Forward proxy abstracts out the client by acting as a middleman. 

<img width="492" alt="Screenshot 2024-04-06 at 8 52 25 PM" src="https://github.com/Madhupatel08/Blogs/assets/54492585/08141a34-843c-4e63-943e-3fa77871d8b7">

Forward Proxy is something like this: Client --> Forward proxy --> Internet --> Origin Webserver

### Why do we need a Forward Proxy

1) "Security": protects the client's identity. For instance, if I'm making a call to google.com there is a forward proxy that will forward the request to the correct server based on my location. And the request will be served. 
2) Policies: restrict access to certain websites or tools. For example: ticktock was banned in India.
3) Caching: Caching some frequently accessed content. For example if the same document/information is being requested by the clients again and again caching this in proxy, will save time and can be frequently accessed.

## Reverse proxy
Reverse proxy abstracts out the complexity of downstream systems.

Reverse Proxy looks like this: Client --> Internet --> Forward proxy --> Origin Webserver

Adding to this, there can be multiple reverse proxies in the journey of a request from the client to the origin server. 

For example: Client --> Cloudfare (CDN) --> NGINX --> Origin Server

Here both Cloudflare and NGINX act as reverse proxies.

### Why do we need a Reverse Proxy

1) Load Balancing - across a set of API servers or DB servers
   - Different load balancing/Rate limiting algorithms are there such as Round Robin, IP Hashing, Least Response Time, Weighted Round Robin, etc.
     which are used to distribute incoming network traffic across multiple servers or resources to ensure optimal utilization, maximize throughput, minimize response time, and avoid overload on any single resource.
2) Routing - Sending/routing incoming requests to appropriate services or servers.
3) Caching - saving some of the frequently accessed data into the reverse-proxy/load-balancer for serving it frequently.
4) Abstraction - Abstraction of infra elasticity (autoscaling) & becoming the single point of contact. For example: if we change the number of servers or if scales/downscales the clients will not be affected. So it gives an elastic nature.


Example of Load balancer proxies: Nginx/ HA proxy
Example of API Gateways proxies (for Routing the requests): Kong Gateway
Example of Db proxies: PoxySQL

Database Proxy can 1. Cache responses 2. pool connections to databases 3. abstracts(elasticity) out database (as explained above)




