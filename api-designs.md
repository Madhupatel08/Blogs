## Monolithic and Microservices 
A monolithic architecture is one in which all the components of an application, such as, frontend, backend, databases, and any other component, are embedded in a single codebase. The application is developed, updated, and deployed as a monolith.

| Advantages    | Disadvantages |
| -------- | ------- |
|  Easy to develop and deploy as the application is developed as a single executable app with fewer components to manage during deployment | Hard to scale a monolithic application because all the components are coupled; to make changes, we need to update the whole system or application    |
| Simple to test and maintain the application because all the components are coupled together | Need to deploy the complete application after the update     |
| Fewer security issues because the data is processed within a single unit, producing a response with low latency    | Limitation of size and complexity    |
| Low initial cost of the system | CI/CD is difficult |
| Resources for development are less costly | Problems with reliability—the whole application can be down because of an issue |

A microservice is an architecture in which an application is divided into smaller services. These services handle smaller functionalities and data of the application by communicating with each other using defined protocols. They can be physically separated but connected through protocols.

| Advantages    | Disadvantages |
| -------- | ------- |
|  Easy to manage larger applications due to decoupled services | Costly in terms of services, development, and networking  |
| Easy development and deployment strategy as each microservice is updated individually | More complex to manage due to its distributed attributes  |
| Reliable as a single service failure can’t bring down the whole application    | Security issues as communication between services can make data vulnerable    |
| CI/CD is easier than monolithic | 	Less secure than monolithic |

<img width="624" alt="Screenshot 2024-07-26 at 5 00 38 PM" src="https://github.com/user-attachments/assets/20db1b76-8e64-49ce-b802-e2799451b26c">

## Difference between API and endpoint 

APIs and endpoints are two different entities. An API is the method by which two software applications communicate, and an endpoint is a component of the API. Endpoints define the exact location of the available resources. In contrast, API uses these endpoint URLs to make its resources available to its users.

Examples of Endpoints within the GitHub API:
1) List Repositories
Endpoint: https://api.github.com/user/repos
Method: GET
Description: This endpoint lists all repositories for the authenticated user.

2) Create a Repository
Endpoint: https://api.github.com/user/repos
Method: POST
Description: This endpoint creates a new repository for the authenticated user.

3) Get a Single Issue
Endpoint: https://api.github.com/repos/:owner/:repo/issues/:issue_number
Method: GET
Description: This endpoint retrieves a specific issue by its number from a repository.

*API Design LifeCycle:* 
<img width="695" alt="Screenshot 2024-07-26 at 5 08 32 PM" src="https://github.com/user-attachments/assets/c07c6fb5-2b29-44ad-832e-54113d7d4b5f">

*Approaches of API Design:*
<img width="427" alt="Screenshot 2024-07-26 at 5 09 35 PM" src="https://github.com/user-attachments/assets/fb38d9bb-f893-4430-a852-a5a80d073c42">

*API design considerations*
<img width="527" alt="Screenshot 2024-07-26 at 5 10 29 PM" src="https://github.com/user-attachments/assets/46fb361e-5090-4875-8ac6-d6fb1d36b18e">

*API requirements*
<img width="712" alt="Screenshot 2024-07-26 at 5 11 05 PM" src="https://github.com/user-attachments/assets/536f0532-02e3-4d91-8866-5240f9e9d369">

- Dynamic Rate Limiting
- Security
- Error Warnings and Handling
- Fault tolerance
- performance measurement

 *Why does a large proportion of API calls converge to use REST over HTTPS?*
 
Data transfer through different layers of the OSI Model

<img width="706" alt="Screenshot 2024-07-26 at 5 29 36 PM" src="https://github.com/user-attachments/assets/af382ea9-b1d3-47cb-986a-4e945f2e5ee5">

Step 1) When a user sends an email, it first interacts with the application layer, which is responsible for data manipulation.
Step 2) Next, the email's data is forwarded to the presentation layer, which adds the presentation layer header (PH).
Step 3) The session layer adds the session layer header (SH) and manages the session during the communication.
Step 4) The transport layer adds the transport layer header (TH), divides the data into segments, and adds the sender and receiver port numbers.
Step 5) The network layer converts the segments into packets and adds the IP addresses of the sender and receiver.
Step 6) The data link layer converts the packets into frames, adds the MAC address of the immediate next hop in the path and passes them to the physical layer. This layer adds a data layer header (DH) and a data trailer (DT) to define the boundaries of a frame on the wire.
Step 7) The physical layer converts the frames into the bitstreams and sends it to the receiver side.
Step 8) The bit stream propagates to the physical layer of the receiving machine through the transmission medium.
Step 9) The physical medium sends the data to the data link layer, which reads the header of the frame at the data link layer.
Step 10) The data link layer hands over the packet to the appropriate network layer protocol after removing the data link layer header (DH) and trailer (DT).
Step 11) The network layer forwards the packets to the transport layer after reading the network layer header (NH).
Step 12) The transport layer header (TH) is used to forward data to the session layer.
Step 13) The session layer header (SH) contains information that is used to forward the packet to the correct presentation layer protocol.
Step 14) The presentation layer header (PH) forwards the data to the email client running on the application layer.






