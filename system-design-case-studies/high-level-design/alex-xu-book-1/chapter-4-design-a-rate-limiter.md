### Step-1: Understand problem and design scope 
* what kind of rate limiter we are going to design? is It server side or client side rate limiter?
    * server side
* Systems should throttle API request, how do we throttle the request? based on IP or User-ID?
    * user-id
* Admin should be able to add some kind of rate limiting rules? do we need to focus on that also?
    * yes
* System should have some kind of error handling mechanism.
* what is the scale of the system? is it for startup or large company?
    * large-scale
* will system work in a distributed environment.
Requirements:
* server side rate limiter
* throttle API based on user-Id
* add rate-limiting configuration
* error-handling 
* distributed
* low latency
* high availability 
* fault tolerant

### Step-2: Propose high level design and get buy-in

![[system-design-case-studies/high-level-design/diagrams/design-rate-limiter-excalidraw.excalidraw]]

### Step-3: Deep dive
#### algorithms
1. **fixed window**
	-  The algorithm divides the timeline into fix-sized time windows and assign a counter for each window. Once the counter reaches the pre-defined threshold, new requests are dropped until a new time window starts
	- Spike in traffic at the edges of a window could cause more requests than the allowed quota to go through.
	- Redis single value required for implementation.
1. **leaky bucket**
	- The leaking bucket algorithm is similar to the token bucket except that requests are processed at a fixed rate. It is usually implemented with a first-in-first-out (FIFO) queue.
	- when new request comes it put in the bucket if it is not null, and requests are removed form bucket at fixed rate.
	- suitable for stable overflow.
	- A burst of traffic fills up the queue with old requests, and if they are not processed in time, recent requests will be rate limited.
	- two params to be adjusted.
	- redis sorted set required for implementation.
	- NGINX default rate limiter algorithm.
1. **token bucket**
	- A token bucket is a container that has pre-defined capacity. Tokens are put in the bucket at preset rates periodically. Once the bucket is full, no more tokens are added. when new request comes it checks if token available in the then request goes otherwise dropped.
	- in Redis we need two value - counter, last refill time.
	- amazon gateway, stripe use this algorithm
	- Token bucket allows a burst of traffic for short periods. A request can go through as long as there are tokens left
	- cons: two parameters to be tuned.
2. **sliding log window**
	- The algorithm keeps track of request timestamps. Timestamp data is usually kept in cache, such as sorted sets of Redis
	- It keeps a sliding window, removes all the log which are older, if current windows have more log then drops the request otherwise request goes.
	- very accurate
	- not memory efficient as keeps dropped requests log also.
	-  can handle burst of request.
1. **sliding window counter**
	- Assume the rate limiter allows a maximum of 7 requests per minute, and there are 5 requests in the previous minute and 3 in the current minute. For a new request that arrives at a 30% position in the current minute, the number of requests in the rolling window is calculated using the following formula:
		1. Requests in current window + requests in the previous window * overlap percentage of the rolling window and previous window
	- It smooths out spikes in traffic because the rate is based on the average rate of the previous window.
	- According to experiments done by Cloudflare, only 0.003% of requests are wrongly allowed or rate limited among 400 million requests.
#### db choice and performance optimization
- for speed we need NOSQL in memory database, Redis can handle = 1 / 100 ns = 10M request,
  while in SQL we might can handle only 1000 requests, 1ms for each request.
- race condition (Redis is single threaded)
#### distributed scaling 
1. I will go with distributed key value storage like Redis. We many need different type of distributed consensus (Raft, Paxos), transaction(leader-election, zoo-keeper), consistency 
#### error handling
- we can return some header in response so that client can handle properly.
- x-rate-limit-retry-after
- x-rate-limit-left
