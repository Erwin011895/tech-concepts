# Cache

## Use cases

reduce latency & optimize architecture.

ServerApp <-> cache -> database

- Reduced latency
- Reduced load on DB
- reduce network cost

## Types of Caches by level

- Client caching
- CDN caching
- Web Server caching
- Database caching
- Application caching

## Types of Caches by design

- Global cache

```
App1 <-> cache <-> DB
App2
```

- Distributed cache

```
         Cache Cluster
App1 <-> | cacheNode1 |    <-> DB
App2 <-> | cacheNode2 |
App3 <-> | cacheNode3 |
```

primary for write. replica for read.

## Cache invalidation strategies

### Write Around cache

cache aside, lazy loading, reactive approach

```
       read
Client <-->  Cache      --- Storage
|                       |
-------------------------
        write
```

- Cache stay slim & contains data that it really needs
- Straightforward implementation & immediate gains
- cons: Cache get filled only after cache-miss, meaning 3 trips

### Write Through cache

proactive approach

```
       read        write
Client <-->  Cache <---> Storage
```

- well-synced with database, resulting in fewer reads.
- cons: Infrequently-requested data also written to cache, resulting in a larger cache.

### Write Back cache

```
       read        async write
Client <-->  Cache <----------> Storage
```

- faster response
- cons: cache can out of sync with Storage. when another service update the DB, or cache node is down.

## Eviction policies

- LRU (least recently used)
- LFU (least frequently used)
- LIFO (last in first out)
- RR (random replacement)
- Setting a TTL, self-cleans-up.
- Lazy read repair, randomly pick request, read from DB & write to cache
- Redis SCAN background process, cron job

## How to implement caching

- easy to implement
- existing solution work well
- redis, memcached, varnish, node-cache

## When not to use caching

- add cache layer makes no difference
- high randomness on requests
- frequently updated data
