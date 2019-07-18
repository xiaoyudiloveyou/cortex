# Running Cortex in Production

This document assumes you have read the
[architecture](architecture.md) document.

## Planning

### Storage

Cortex requires a scalable storage back-end.  Commercial cloud options
are DynamoDB and Bigtable: the advantage is you don't have to know how
to manage them, but the downside is they have specific costs.
Alternatively you can choose Cassandra, which you will have to install
and manage.

### Ingester replication factor

The standard replication factor is three, so that we can drop one
sample and be unconcerned, as we still have two copies of the data
left for redundancy. This is configurable: you can run with more
redundancy or less, depending on your risk appetite.

### Index schema

Choose schema version 9 in most cases; version 10 if you expect
hundreds of thousands of timeseries under a single name.  Anything
older than v9 is much less efficient.

### Chunk encoding

Standard choice would be Bigchunk, which is the most flexible chunk
encoding. You may get better compression from Varbit, if many of your
timeseries do not change value from one day to the next.

### Sizing



###

Don't run multiple ingesters on the same node, as that raises the risk
that you will lost multiple replicas of data at the same time.
