**1. Networking Layer**
  This is usually the first component in a database system. It is responsible for talking to the client.

**2. Database Front End**
  The front end outputs some instructions the rest of the components can understand. This could be byte code or something else.

  **2.1 Tokeniser**
    A tokeniser is responsible for deconstructing the query received by the networking layer into each individual token, or command. This is the first step in understanding the query's contents. 

  **2.1 Parser**
    This step takes the tokens generated before and makes sure their structure and kind form a valid command. Parsers commonly generate a parse tree, a structure representing the instructions the database is supposed to perform.

  **2.3 Optimiser**
    This step receives the parsed input and finds the best way to execute the instructions for the highest speed possible (while maintaining accuracy). For instance, the optimiser tells us that we could use binary search for a particular instruction if the relevant list is sorted.

**3. Execution Engine**
  This is the central element of the system. It performs the functions of the database.

  **3.1 Query Executor**
    This component just takes instructions and executes them.

  **3.2 Cache Manager**
    This improved efficiency by caching often requested information and providing other optimisations.

  **3.3 Utility Services**
    There are often several important services included in the execution engine including, but not limited to, authentication, security, backups, metrics, etc.
  
  **4 \[Name\]**
    This component works closely with the concurrency manager.
  **4.1 Transaction Manager**
    This component makes sure the asset properties are followed. 

  **4.1 Lock Manager**
    This manages locks on the database to avoid inconsistencies.

  **4.2 Recovery Manager**
    This is responsible for recovering from problems like a crash. 

**5 Concurrency Manager**
  This can be something like MVCC. It is important enough to warrant its own component because we want to separate our concerns.

**6 Shard Manager**
  This manages the portion of the database which is on this specific server. Large databases will have multiple servers, each of which have a shard.
  **6.1 Cluster Manager**
    If there are different servers each hosting a shard, they have to be communicated with.
  **6.1 Replication Manager**
    This is responsible for overseeing the process of copying and synchronizing data across multiple database instances or servers. 

**7. Storage Engine**
  This is the core of the database and responsible for storing data. Because disk i/o is very expensive, the speed of the database will often be dependent on the speed of the storage engine.
  **7.1 Disk Storage Manager**
    This part is responsible for reading from - and writing to - disk.

  **7.2 Buffer Manager**
    Because we can't directly modify the disk without addressing the whole page, we use a buffer manager.

  **7.3 Index Manager**
    Indexing is important for increasing efficiency and speed of our disk i/o.
  
**8 OS Interaction Layer**
  This makes the actual system calls to store and read data.