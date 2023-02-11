# Design Data Intensive Applications





 We call an application data-intensive if data is its primary challenge—the quantity of data, the complexity of data, or the speed at which it is changing—as opposed to compute-intensive, where CPU cycles are the bottleneck.


 ## Chapter 3 - Storage & Retrival

 Log is used in the more general sense: an append-only sequence of records. It doesn’t have to be human-readable; it might be binary and intended only for other programs to read.


##### Hash Indexes


### LSM Trees
- Write is fast
- Read is slow 
- High write throughput due to (Write amplification)
- Compressed better
- 
- Lower s;

## B Tree
- Head log 
- Entire page to be written always
- Leaves space ( unfragemented)
