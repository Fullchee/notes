## How to scale up database writes? (4)

1. Is the app making a ton of unnecessary writes or unnecessary indexes?
   (duplicate API calls)

2. upgrade your machine

3. Primary/secondary replication so that reads are handled by another machine so the main machine only deals with writes

4. Horizontal Partitioning
5. Last resort: Sharding

will have multiple machines you can write to

eg: US database, Australia database

split tables into separate machines
join will be tough
put users tweets into specific machines
