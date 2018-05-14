# Instance Types

Below you can find our current list of instance types. A fully dynamically updated list can also be fetched using the DescribeVmTypes API call. The different types offer different performance profiles:

* Balanced: A standard configuration with a good mix of Memory and Compute.
* Max: Powerful configuration when maximum Memory is required.
* Core: Useful for applications that require more Compute.


Name | Cores | Memory | Disk | Bandwidth | Performance type
---- | ----- | ------ | ---- | --------- | ----------------
gcl.1 | 1 | 1024 | 30 | 1 TB | Balanced
gcl.2 | 1 | 2048 | 60 | 1 TB | Balanced
gcl.4 | 2 | 4096 | 90 | 5 TB | Balanced
gcl.8 | 4 | 8192 | 120 | 5 TB | Balanced
gcl.core.2 | 2 | 2048 | 60 | 5 TB | Core
gcl.core.4 | 4 | 4096 | 90 | 5 TB | Core
gcl.core.8 | 8 | 8192 | 180 | 5 TB | Core
gcl.max.8 | 2 | 8192 | 180 | 5 TB  | Max
gcl.max.16 | 4 | 16384 | 360| 5 TB | Max

