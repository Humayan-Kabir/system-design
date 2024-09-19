### Back of the envelope

#### data volume calculation
![[estimation-with-power-of-two.png]]
#### [latency comparison number](https://github.com/donnemartin/system-design-primer?tab=readme-ov-file#latency-numbers-every-programmer-should-know)
![[estimate-latency.png]]
#### visualization
![[estimation-visualization.png]]

Handy metrics based on numbers above:
- Read sequentially from HDD at 30 MB/s
- Read sequentially from 1 Gbps Ethernet at 100 MB/s
- Read sequentially from SSD at 1 GB/s
- Read sequentially from main memory at 4 GB/s
- 6-7 world-wide round trips per second
- 2,000 round trips per second within a data center
### Availability numbers
High availability is the ability of a system to be continuously operational for a desirably long
period of time. High availability is measured as a percentage, with 100% means a service that
has 0 downtime. Most services fall between 99% and 100%.
**SLA: service level agreement**
![[estimate-availability.png]]
#### Example: Estimate Twitter QPS and storage requirements
**Assumptions:**
1. 300 million active users monthly 
2. 50% of users use twitter daily
3. avg each user post 2 tweet per day
4. 10 % tweet contains media files
**QPS**
$$
\text{Tweets QPS} = \frac{300M \times 50\% \times 2}{24 \times 3600} = \frac{300M}{24 \times 3600} \approx 3500
$$
$$
\text{Peak QPS} = 2 \times 3500 \approx 7000
$$
**Data storage for 5 years**
average tweet side
- tweet_id : 64 bytes
- text : 140 bytes
- media: 1MB
$$
\text{Media Storage} = 300M \times 50\% \times 2 \times 10\% \times 1 \, \text{MB} = 30M \, \text{MB}
$$
$$
\frac{30M \, \text{MB}}{10^6 \, \text{MB}} = 30 \, \text{TB}
$$
$$
\text{5 years data storage} = 30 \, \text{TB} \times 5 \times 365 \approx 55\, \text{PB}
$$
