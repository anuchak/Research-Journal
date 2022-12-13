# LDBC 0.1

The results of each query have been arranged as follows:
- The shortest hop path (starting from destination node ID to the source node ID)
- The highest execution time taken out of 5 runs
- The lowest execution time taken out of 5 runs

For the Neo4j queries, total time taken is specified after the _completed after_ part.  
Two executions with the highest and lowest time taken.  

## 1-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256077 RETURN a;`  

866->0  
Time: 12.78ms (compiling), 15.01ms (executing)  
Time: 0.70ms (compiling), 28.77ms (executing)  
Time: 0.34ms (compiling), 6.15ms (executing)  

### Neo4j

Started streaming 1 records after 2 ms and completed after 4 ms.  
Started streaming 1 records after 1 ms and completed after 2 ms.  

------------------------

## 2-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256530 RETURN a;`  

70->866->0  
Time: 0.82ms (compiling), 14.50ms (executing)  
Time: 0.88ms (compiling), 7.19ms (executing)  

### Neo4j

Started streaming 1 records after 1 ms and completed after 5 ms.  
Started streaming 1 records in less than 1 ms and completed after 2 ms.  

-------------------------

## 3-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256668 RETURN a;`  

653->70->866->0  
Time: 0.78ms (compiling), 14.65ms (executing)   
Time: 0.39ms (compiling), 6.66ms (executing)  

### Neo4j

Started streaming 1 records after 7 ms and completed after 15 ms.  
Started streaming 1 records after 1 ms and completed after 5 ms.  

--------------------------

## 4-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256816 RETURN a;`  

1385->653->70->866->0  
Time: 0.32ms (compiling), 16.22ms (executing)  
Time: 0.96ms (compiling), 8.02ms (executing)  

### Neo4j

Started streaming 1 records after 9 ms and completed after 19 ms.  
Started streaming 1 records in less than 1 ms and completed after 5 ms.  

--------------------------

## 5-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256862 RETURN a;`  

1284->1385->653->70->866->0  
Time: 0.74ms (compiling), 13.02ms (executing)  
Time: 0.74ms (compiling), 6.17ms (executing)  

### Neo4j

Started streaming 1 records after 9 ms and completed after 18 ms.  
Started streaming 1 records after 1 ms and completed after 4 ms.  

