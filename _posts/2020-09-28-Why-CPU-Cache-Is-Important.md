---
layout: post
title: Why is CPU cache important?
date: 2020-09-28
---

A while back, I answered a question on Reddit about why CPU cache was important.
This was on the /r/buildapc subreddit when the Ryzen CPUs were being released.
The poster was wondering why the large amounts of cache on these newly released
CPUs was such a big deal; After all, their programs were much larger than the
36.5 MB of cache on the 3700X. The answer to the poster's question was that
temporal and spacial locality meant that only a small portion of the program
needed to be cached at a time, but I decided to go a little more in depth and
talk about why CPU cache was even important to begin with. Below is a copy of my
comment on this topic.

---

To answer your question, spatial and temporal locality mean that only a small
subset of the program is needed at a time. Here's an extremely detailed
explanation of cache and why it is so important:

---

## Feeding a Giant with a Spoon

Modern CPUs are incredibly fast and can operate at billions of cycles per
second. Within each cycle they need to fetch instructions, decode them, and
execute them. Fetching instructions and possibly executing instructions requires
a memory access. The problem is that memory hasn't kept up with the speed of
CPUs. Although memory might have high bandwidth (GB/s), the problem is latency.
Accessing memory could take over 10,000 clock cycles. While the CPU is waiting
on memory, it is not doing anything else. This means that no matter how fast the
CPU can execute instructions, it will be bottlenecked by memory. It is analogous
to feeding a giant with a spoon. No matter how big and powerful a giant is, it
will starve if you try to feed it with a normal spoon.

## Temporal and Spatial Locality

If you analyze the execution of code, you will notice two phenomenon: temporal
and spatial locality.

* Temporal Locality: Code and data that have been accessed are likely to be
  accessed again in the very near future
* Spatial Locality: Memory around code and data that have been accessed recently
  is likely to be accessed itself in the very near future

Although you may need all the code and data in a program eventually, you can
view the memory needed currently as a window that slowly moves across the
program.

## Adding a Layer of Cache

Cache is fast and low latency, but also expensive. It takes up space on the CPU
that could be used for other hardware and because of this is usually small. This
is actually not an issue because of the locality discussed above. The cache
represents the window moving across your program. Memory in your cache is likely
to be accessed again, meaning that the entire program does **not** need to be in
cache to reap the majority of the benefits of cache. Rather than having to wait
100+ cycles for most memory requests, it could be below 10.

## Hit or Miss

The CPU cache won't always have what it needs. As the window moves across the
program, the cache will need to drop some of the cached memory and add new
memory to cache. These are referred to as cache hits and cache misses:

* Cache hit: The memory requested is in cache
* Cache miss: The memory requested is not in cache and must be fetched from main
  memory^(or the next layer of cache; more on that later)

Cache misses are expensive. They require that the CPU go out to memory which
could take 100+ memory cycles or more. Obviously, increasing the hit ratio could
dramatically increase the performance of the CPU. There are several strategies
for doing so. Here are a couple:

* Add more cache: This is by far the simplest solution. The larger the cache,
  the more likely the memory you want is in it. The downside is that cache is
expensive. It takes up space on the CPU that could be used for other hardware.
* Be better at predicting what needs to be in cache. This includes things like
  drop policy: When something needs to be added to the cache, what should be
dropped to make space? If something that will be needed soon is dropped, it will
result in another cache miss.

Cache design also plays a role in hit ratio. Look up fully associative, direct
mapped, and set associative cache if you are interested (spoilers: pretty much
everything uses a set associative cache these days).

## Cache Hierarchy

So far, only one layer of cache has been discussed. If cache is fast but small
and DRAM is large but slow, why not just add more layers of cache that get
progressively larger, but slower? That is exactly what modern CPUs do. Many CPUs
will have L1, L2, and L3 cache, with L1 being the fastest but smallest, and L3
being the largest but slowest. L1 cache is usually further split into
instruction and data cache, allowing instructions and data to be accessed
simultaneously. The roles of each layer of cache depend on the CPU design. For
example, Ryzen's L2 cache is per core, while the L3 cache is shared between all
cores on the CCX.

## Key Takeaways

* Cache is the only reason modern CPUs are able to run as quickly as they do
* Temporal and spatial locality make even small caches effective
* Cache designs balance trade-offs between hit ratio, cache size, latency, and
  space on the CPU
