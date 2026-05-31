# Capacity Estimations

Below is a Generic Back of the Envelope estimations template:

## Considerations

| Zeroes | in Latency | In Storage |
| ------ | ---------- | ---------- |
| 3      | T          | KB         |
| 6      | M          | MB         |
| 9      | B          | GB         |
| 12     | T          | TB         |

1. Discuss total users
2. Consider taking 25% as DAU and 9:1 read:write operations


## Latency and Server Estimates
1. Let's say 1B users
2. DAU = 250M users
3. QPS = 250M x 10  = 2500 / 86400 = 2500 M / ~0.1M = 25000 QPS
4. Let's say we own CPUs with 8 cores. Each CPU providing 1s CPU time /second . Also, let's consider each Q takes 20 ms of CPU time
5. Servers needed:
	1. 1 server can give 8s CPU time /sec.
	2. 1 server can serve = 8 /0.02 = 400 QPS
	3. Total servers  = 25K /400 = 65 servers
6. Latency = CPU time + I/O Op + Network delay + Queuing time =  20ms + 20 ms + 5 ms = 45 ms ~50 ms


## Storage Estimates

Stored Entity:
text = 250 chars ( 1 `char` = 2B)
video = 50MB
image = 300KB
numbers =  1 integer(long/double) = 8B

1. Let's say 1 write op takes 250 chars = 250 x 2 =500B = 0.5KB
2. Out of 25K QPS, 10% is write op = 2.5K WQPS
3. Total storage req/s = 2.5K x 0.5 KB = 2500 x 0.5KB = 1250 KB
4. Yearly = 1250KB x 0.1M (1 day) x 365 = 125 GB x 365 = 45 TB/yr ~50TB/yr

> Can add replication estimate as well


## Bandwidth Estimates

- Response payload = 200KB
- We have 25K QPS; Bandwidth = 200 x 25K= 5GB/s
-  Important for  CDN , Streaming, APIs, Media Systems


## Memory/Cache Estimates

- Hot data = 10M objects
- Each object = 500B
- RAM needed = 10M  x 500B = 5 GB

> Can add replication estimate as well


## Database Capacity
Estimate:
	-  read/s
	- write/s
	- index size
	- shard count

Let's say 1 shard handles 20k writes/s
We need 100k writes/s
need 10  shards
