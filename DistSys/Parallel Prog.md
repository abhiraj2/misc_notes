# Parallel

### Caching
A method to overcome the Von Neumann bottleneck
Cache is basically a collection of memory locations which are closer and faster to access by the CPU than some other memory locations

Main funda is that more often than not, the immediate execution is generally of the next mem location
`for(int i=0; i<n; i++) printf("%d\n", a[i])`

* *locality*: Principle that the access of one location is generally followed by th access of a nearby location
* Two types of localities: Spatial and Temporal 
* Spatial: Nearby location
* Temporal: Nearby future

Cache can be thought of as a one monolithic memory but in reality it is divided into parts. 
L1 is the smallest and the fastest part. The higher levels are larger but slower. The lower level cache can be thought of as a cache for the higher level cache itself.


### Virtual Memory
It makes the main memory act as a cache for the secondary memory. The part of the main memory that is idle is swapped with a piece of secondary memory, so that even large of amount of data can be processed simulataneously. Acts on the principle of spatial or temporal locality.
Vitual memory also works with blocks of data also called <b>Pages</b>. When the program is run, a Page table is created that maps all the page numbers to the physical addresses. 

So basically, the program has access to the virtual address which gets translated to physical address using Page Table. But Page table can actually increase the overall run time of your program. This is why <b>transition-lookaside buffer</b> is used.In the TLB we store a small number of entries in a really fast memory. Due to temporal and spatial locality we can expect most of the entiries to be requested by the program should be present in the TLB alone.


### Instruction Level Parallelism
#### Pipelining
Suppose we want to add two floating point exponent numbers
* Read
* Compare exponents
* Shift
* Add
* Normalize
* Round
* Store
So a total of 7 operations. If each operation takes 1 ns. The entire addition takes 7ns and with a for loop for adding to arrays of say size 1000, it would take 7000ns.

So one approach to make this faster is Pipelining. We distribute all the 7 operations into 7 different functional units. Still 1 addition operation would takr 7ns. But with an array, as soon as one floating point goes to the second pipeline. The second number is read by the first one. So at one point 7 different numbers are being processed, due to the number of pipelines.
Buuuuttt.... ILP is hard af to exploit, because not everything can be broken down into several different independent processes, specifically recurring mathematical functions

## Hardware Multithreading
It makes more sense, that when a process is consuming time, like waiting for data to load or something like that another process should be run at the same time for efficiency.

Flynn's Taxonomy is used for classification of these system
SISD, SIMD, MISD, MIMD

### SIMD
One CU, multiple ALUs
#### Vector Processors
These processors have the ability to directly operate on arrays and vectors instead of operating on individual scalars. Same operation is applied throughout the array

#### GPUs
Since graphics processing makes use of small reusable C code called Shader functions, and since these shader functions can be applied to multiple vertices/elements in teh space, GPUs make use of SIMD. 

### MIMD
Multiple cores, each with its own ALU and CU
Unless pressed and forced upon by the programmer, MIMD systems are asynchronous, i.e. there is no relation between working of two different processors
There are two types of Memory archs
* Shared Memory System: Memory is connected to the processors via an interconnect and all the processors have access to all the locations of the memory
* Distributed Memory System: Each processor has its own private memory, therefore processors need to communicate explicitly

#### Shared Memory Systems
Typically each core has a private Level 1 cache whereas other level caches may or may not be shared between the different cores. Based on the fact that the cores can be either connected to Main Memory using an interconnect or directly, SMS are divided into UMA and NUMA (Uniform Memory Access and Nonuniform respectively)

#### Distributed Memory Systems
These are composed of systems like different PCs, and are called clusters, connected by something like Ethernet for communication. **o7 is a DMS**
Actually when clusters are made many multicore processors are used together, so the system is actually **hybrid**

### Interconnects
#### Shared Memory Interconnect
Main devices used in parallel connections are buses and controllers. 

**Bus** is a collection of parallel communication wires together with some hardware that controls access to the bus. Since access to the main memory using a bus is shared, therefore if we connect large number of devices to a bus, processors would have to wait. 
Therefore Buses are nowadays being replaced with switched interconnects

**Switches** are used to control the routing of data among the connected devices. They can have two configs, either straight or turn. With at least as many memory modules as processors only time we can have a conflict is if, two different cores try to access the same memory at the same time. Switches are part of the system also known as **Crossbars**

#### Distributed-memory Interconnect
Further divided into **Direct** and **Indirect** 

##### Direct
Each switch is directly connected to a Processor-Memory Pair

















