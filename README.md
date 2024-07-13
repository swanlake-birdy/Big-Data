# Big-Data (Trendy-Tech by Sumit Mitthal)

# Week 3: Distributed Computing

## Overview

This repository contains notes and examples on distributed computing and the MapReduce programming model. These notes are part of a learning module on big data.

## MapReduce Overview

1. **MapReduce Usage**:
   - Although not widely used in the industry today, MapReduce is fundamental for understanding the theory of distributed computing.
   - It is designed for processing large datasets that are distributed across multiple machines in a cluster.
   - Running MapReduce on small datasets is inefficient due to its computational overhead and setup time.

2. **How Distributed Computing Works**:
   - Distributed computing divides tasks into smaller subtasks that can be processed concurrently across multiple machines.
   - This parallel processing approach helps in handling large volumes of data efficiently.

3. **MapReduce Process**:
   - **Map Phase**: Processes data on individual machines, providing parallelism. Each mapper operates on a different part of the data.
   - **Reduce Phase**: Aggregates and processes the output from the map phase. Minimizing work in the reduce phase is crucial to avoid it becoming a bottleneck.
   - For optimal performance, developers should aim to perform more computation during the map phase and less during the reduce phase. This approach leverages the parallel nature of mappers and prevents overloading the reducers.

### Key Concepts
- **Parallelism**: Achieved through multiple mappers running simultaneously on different machines.
- **Scalability**: By increasing the number of mappers, the system can handle larger datasets more efficiently.
- **Efficiency**: Reducing the workload on the reducer phase ensures faster overall processing time.

## Example: LinkedIn Profile Views

### Dataset
This example demonstrates how to interpret who viewed whose profile.

ID, From-Member, To-Member
1, Manasa, Sumit
2, Deepa, Sumit
3, Sumit, Manasa
4, Manasa, Deepa
5, Deepa, Manasa
6, Shilpy, Manasa


### Objective
Calculate total views for each profile using MapReduce.

### Mapper Input
The record reader provides key-value pairs to the mapper:

(0, [1, Manasa, Sumit])
(1, [2, Deepa, Sumit])
(2, [3, Sumit, Manasa])
...


### Mapper Output
The mapper outputs key-value pairs where the key is the profile and the value is 1:

(Sumit, 1)
(Sumit, 1)
(Manasa, 1)
(Deepa, 1)
(Manasa, 1)
(Manasa, 1)


### Reducer Input
The reducer receives shuffled and sorted output from the mapper:

(Deepa, [1])
(Manasa, [1, 1, 1])
(Sumit, [1, 1])


### Reducer Output
The reducer aggregates the counts:

(Deepa, 1)
(Manasa, 3)
(Sumit, 2)


### Explanation
- The mapper phase processes the data in parallel, emitting key-value pairs for each profile view.
- The shuffle and sort phase organizes the data for the reducer.
- The reducer then aggregates the results, providing the total view count for each profile.

## Determining the Number of Mappers and Reducers

### Mappers
- The number of mappers is determined by the number of data blocks.
- Example: For a 1 GB file with a block size of 128 MB, there will be 8 blocks, resulting in 8 mappers.

### Reducers
- The number of reducers is controlled by the developer.
- By default, there is only one reducer, but the number can be increased as needed.
- Reducing the number of reducers too much can lead to inefficiency, while increasing it too much may lead to underutilization of resources.

### Example Configuration
- For a cluster with 3 nodes, if the data is divided into 8 blocks, there will be 8 mappers running in parallel.
- The number of reducers should be set based on the desired level of parallelism and resource availability.

## Conclusion

Understanding MapReduce is crucial for grasping the principles of distributed computing. 
Although not as widely used today, the concepts and techniques are foundational for working with large datasets and distributed systems.

---

