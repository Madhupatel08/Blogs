## What is throttling

Throttling is a technique that ensures that the flow of data being sent at the target machine/service/sub-system can be digested at an acceptable rate.

Throttling is more of a defensive measure
- Throttling could be slowing Eg. the SQS Queue system, if lots of request comes in it will slow down. The requests are kept in the buffer and the server will read those requests based on their speed.
- Throttling could be rejecting Eg. API servers and the client will be informed that the request has been rejected
- Throttling could be ignoring Eg. API servers and the client will be not informed that the request has been ignored

## Why do we need throttling 
1) To prevent System abuse
2) To only allow traffic that could be handled
3) Control consumption cost.
4) To prevent cascading failures.

## Use cases of throttling

1. **Prevents catastrophic DDoS attacks: Distributed Denial of Service (DDoS)**
Strategy to limit the impact of malicious traffic on a targeted system. By throttling or blocking suspicious or excessive requests, the system can maintain availability for legitimate users.
2. **Gracefully handle a surge of users:**
limit the number of requests made by a particular user or application within a specific time frame. This prevents abuse or overloading of the API servers, ensuring fair usage among all users.
3. **Multi-tire Limit:**
For eg. if we have a business model, we charge different amounts from every user based on the plan they have chosen, so we'll have to take note of the number of requests the user has made and Internal Rate-limiter will come to process, and the user will be blocked if he has made request greater than their plan.
4. **We not over-using  a third-party system:** 
Eg: we are consuming an expensive third-party API and their pricing is aggressive. This can be solved by putting an internal rate limiter and pricing can be decided based on that.
5. **Not overwhelming your unprotected system:**
For eg: Hard deleting from DB should be uniformly distributed, Deleting a million rows in one go, can take down your DB, and hence you should streamline the deletions.
