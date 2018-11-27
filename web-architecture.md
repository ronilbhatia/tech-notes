# Web Architecture - Ned's Lecture

## Day 1

* **Amazon Web Services** most popular service is EC2 which allows you to rent computers in the Amazon data center, so that it can run server-side code on those computers
* **Public DNS** - Domain Name Space - essentially a phone book running in the cloud
  * When a computer wants to contact another computer it needs its IP (Internet Protocol) address. Domain name is convenient name to look up (like name in a phone book) whereas IP is the actual address on the internet (like address you get when you lookup in phone book)
  * Have to actually purchase domain name from registrar.
  * Domain name must be associated with IP address for web app to run properly.
  * Same IP Address can serve up multiple hosts, so still need to specify 'Host' in HTTP request header
* **SSH** is a command used to log in to a computer somewhere else in the world
* Databases are run on their own server separate from the application
* One CPU does not have enough power to handle a largely scaled application with lots of users. Having lots of N+1 queries will additionally slow it down. Regardles of how optimized application is, CPU will eventually reach a limit. Potential solutions:
  * Optimize - Eliminate N+1 queries, cache responses for common requests, etc.
  * **Vertical scaling (*Scaling up*)** - Make the single CPU faster and able to handle more. Often the more practical thing to do.
  * **Horizontally Scaling (*Scaling out*)** - Add more computers
    * This adds more complications that make it not so easy. Should try to optimize and scale vertically before doing this
    * Works by having one central cpu that stores the database which all of the separate servers are talking to.
    * **Load Balancer machine** which is what the user will be directed to when they enter the domain name in the browser - this essentially acts as middleware to direct the request to one of the servers. Even though all users will go through this, this doesn't blow up the server because it's job is very simple - redirect to one of the servers to actually process the request. NGINX is example of load balancer.
    * If one of the machines crashes, the load balancer can tell when a machine is down (if it doesn't receive a response promptly) and will instead only direct request to the other machines live in the system, so that the application can continue running. Will take a performance hit, but still be up.
* Reading/writing data to and from the database tends to be the bottleneck in applications that slows it down.
* **Hard disks** take a long time because they are like tapes with spinny things, that require getting to the right point in the drive before you can actually read the data that you want.
* **RAM** allows you to store and get data similar to the hard disk but it is way faster because it will be able to access that exact point where the data you want is stored immediately. RAM is like an electrical circuit, that responds to electrical signals really fast. Therefore way faster than any sort of mechanical thing could work either.
  * One downside to RAM is that it is not persistent, because as soon as the computer is turned off all of that will be lost.
  * Persistence means slow access and writing, but gives data permanence. Hard Disk gives us persistence, RAM gives us speed and performance for things that do not need to be remember forever.
* **Solid State Drive** is somewhat of a hybrid between a hard disk and RAM, in that it has no mechancial components - this makes it way faster than a hard disk. It also allows for persistence of data - not as fast as RAM (RAM still probably 100x faster than solid state drive)
* Data fundamentally needs to live in the disk, so that it is never lost. Write to DB therefore need to be persisted in the disk, however when we read data it would be nice if we didn't have to talk to the disk. What the DB can do once the DB starts up, is take all of the data in the database and if its not too much data can read everything on the disk and then put it onto the RAM - then when somebody needs to read something from the database it can read from the RAM - similar to cacheing in which the RAM is being used as a cache for the disk data.
* One of the simplest ways to improve application performance is to buy more RAM.
* When determining what to store on RAM vs disk if there is not enough space to store everything on RAM you want to prioritize the things that are being looked up the most. A vast majority is probably never being looked at.
* Typically don't have data loss in server crashes
* DBA = Database Administrator who will configure the DB and how it uses RAM in the ability that is most efficient to a Company's specific needs but this requires being in the detail about the database.
* **SPOF** - Single Point of Failure

## Day 2

* DB Leader-Follower Structure
  * **Failover** - if one of the app machines crash, load balancer doesn't propmtly receive response -> excludes that machine from work distribution.
  * All DB writes are done in the leader, whereas reads are done from any of them
  * **Synchronous Replication** - Leader must forward writes to all followers and confirm that they have made the appropriate change - can then tell the Rails application that the DB query is complete once all of the followers have appropriately updated the database.
  * Problem with **asynchronous replication** is that it's possible that after something is updated, data is attempted to be read from separate machine where the data hasn't been replicated yet.
    * Usually this only takes a couple of seconds, so it typically isn't too big of an issue, because likely the user will refresh their page, try again, and in the time that it took them to do that it will now work.
  * **Partitioning** - Solution to breaking out DB over multiple computers is not having all computers have identical copies of the data, but rather to each have one portion of the data. Each portion is known as a **shard**
    * Adding a new shard, results in having to go through all of the data and re-assign it to the new shards since you now have an extra bucket (similar to resizing problem with HashMap - O(n) operation). Solution to this is to make way more shards than you need initially so that you don't run into this issue for a very long time, other solution is to have an extensible hashing function that will seamlessly work when you add an additional shard (look this up, idk how it works)
  * One of the primary functions of databases is accepting multiple requests in parallel but doing so in such a way that it does not accept two conflicting requests - it chooses one to process and one to reject
  * Computers prefer batch processing (multiple units of work) as opposed to processing single units of work.
  * **Promotion** - making one of the followers the leader if the leader goes down (crashes)
    * If leader fails while transferring data to followers, there is a problem if one of the followers who did not receive this data becomes the new leader as they do not have the most up to date writes. There must be some sort of reconciliation process in this case.
  * **Chain Replication** - When instead of the leader telling everybody, tells the first follower, who then tells the next and so on and so forth.
* **Point Queries** - queries that involve a single row
* Common to do both partitioning and leader-follower replication such that you have the benefits of data split out over multiple machines, as well as the leader-follower model so that you have a backup available in case one machine fails.
* **Denormalization** - rather than storing references to other pieces of data in a table, we just store that same data in the table - this is important to do for paritioning, because otherwise we end up having to read across every single shard, and therefore perform a join operation on every single shard, when we require access to data that would typically require a join based on two foreign keys.
  * Tradeoffs
    * copying means that we are taking up more memory/space.
    * Also means that if we update an attribute of something, then we need to update the copies of this data everywhere.
    * With this way, read time is extremely fast, but write time is slow. However, in most cases we care more about read time being fast rather than write time.
  * Typical to start off with a normalized database and see how people use the database, and then later to denormalize it. Normalization tends to be easier as you don't need to worry about keeping data up-to-date/in-sync since all of it is stored in only one place.

## Day 3
* **Log Shipping** - When DB leader sends writes down to follower machines
* When you write/read from a hard drive you want to get stuff that's close together instead of jumping around since you actually have to move the physical device to read/write the data.
* **Concurrency Control** - the process of controlling concurrent modifications to a DB that are non-commutative. Multiple mechanisms to achieve this from
  * **Two-Phase Locking** - Method of concurrency control by which DB will lock modified rows until entire transaction is complete, such that one transaction doesn't affect the other one before it is completed.
    * Two phases of locking are:
      * Acquire locks
      * Release locks
    * Locks are implemented through an atomic *test-and-set* mechanism (atomic instruction) by which the database both reads the row and writes the lock simultaneously
      * Other mechanisms by which this is achieved are Peterson's Algorithm and Deter's Algorithm
  * Concurrency control in partitioned DBs
    * Called *two-phase commit* when dealing with distributed db (essentially same as two-phase locking)
    * Maintain a redo log so that if the DB crashes halfway through the transaction, it can redo the beginning portion of the transaction and complete the remaining portion.  
    * *Idempotent* - can repeat an action and achieve the same result as if it only happened once (assignment is idempotent, incrementation is *not*).
  * *Timeout* - release a lock after a certain amount of time has passed as you realize that the user who sent the request might be 'dead' or something happened where the request was not be able to be completed, and therefore the locks were never able to be released.
* **ACID Database**
  * **A** - Atomicity - when DB processes transactions in an all/none manner
    * **Transactions** in Rails are accomplished through `ActiveRecord.transaction(&blk)`
    * Even if the DB crashes in the middle of the transaction, upon reboot it will either finish the transaction or roll it all back
  * **C** - Consistency - means that database constrains are enforced properly
  * **I** -
  * **D** - Durability - 
