# LDBC 1

The results of each query have been arranged as follows:
- The shortest hop path (starting from destination node ID to the source node ID)
- The highest execution time taken out of 5 runs
- The lowest execution time taken out of 5 runs

For the Neo4j queries, total time taken is specified after the _completed after_ part.  
Two executions with the highest and lowest time taken.  

Shortest Path format:
Dest Node | <Rel ID> | Next Node | <Rel ID> | ... | Source Node

## 2-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256530 RETURN a;`  

Shortest Path: 510 <240345> 1701 <210035> 0

Time: 0.71ms (compiling), 2.25ms (executing)  
Time: 0.71ms (compiling), 1.13ms (executing)

### Neo4j

Started streaming 1 records after 12 ms and completed after 38 ms.    
Started streaming 1 records after 2 ms and completed after 12 ms.  

------------------------------------------------------------------

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256668 RETURN a;`  

Shortest Path: 4393 <240346> 1701 <210035> 0

Time: 0.37ms (compiling), 1.17ms (executing)
Time: 0.37ms (compiling), 1.11ms (executing)

### Neo4j

Started streaming 1 records after 11 ms and completed after 19 ms.  
Started streaming 1 records after 1 ms and completed after 8 ms.  

------------------------------

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256816 RETURN a;`  

Shortest Path: 8973 <240347> 1701 <210035> 0

Time: 0.76ms (compiling), 1.69ms (executing)
Time: 0.77ms (compiling), 1.17ms (executing)

### Neo4j

Started streaming 1 records after 11 ms and completed after 17 ms.  
Started streaming 1 records after 1 ms and completed after 9 ms.  

----------------

## 3-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023257255 RETURN a;`  

Shortest Path: 8382 <373978> 8973 <240347> 1701 <210035> 0

Time: 0.82ms (compiling), 15.54ms (executing)
Time: 0.72ms (compiling), 1.68ms (executing)

### Neo4j

Started streaming 1 records after 10 ms and completed after 17 ms.  
Started streaming 1 records after 1 ms and completed after 8 ms.  

----------------

## 4-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257255 RETURN a;`  

Shortest Path: 8382 <373978> 8973 <240347> 1701 <244186> 1907 <210040> 1

Time: 0.71ms (compiling), 14.67ms (executing)
Time: 0.55ms (compiling), 6.77ms (executing)

### Neo4j

Started streaming 1 records after 10 ms and completed after 16 ms.  
Started streaming 1 records after 1 ms and completed after 8 ms.  

------------------

## 5-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256077 RETURN a;`  

Shortest Path: 5712 <385223> 9587 <351914> 7803 <242638> 1809 <240317> 1701 <210035> 0

Time: 0.72ms (compiling), 22.22ms (executing)
Time: 0.69ms (compiling), 18.09ms (executing)

### Neo4j

Started streaming 1 records after 1 ms and completed after 8 ms.  
Started streaming 1 records after 1 ms and completed after 7 ms.  

---------------------

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257716 RETURN a;`  

Shortest Path: 2120 <234702> 1310 <343227> 7298 <240315> 1701 <244186> 1907 <210040> 1

Time: 0.72ms (compiling), 21.11ms (executing)
Time: 0.73ms (compiling), 17.43ms (executing)

### Neo4j

Started streaming 1 records after 8 ms and completed after 18 ms.  
Started streaming 1 records after 1 ms and completed after 7 ms.  

-----------------------

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257939 RETURN a;`  

Shortest Path: 9403 <319998> 6071 <384008> 9505 <387059> 9686 <244184> 1907 <210040> 1

Time: 0.73ms (compiling), 20.47ms (executing)
Time: 0.84ms (compiling), 16.67ms (executing)

### Neo4j

Started streaming 1 records after 10 ms and completed after 15 ms.  
Started streaming 1 records after 1 ms and completed after 8 ms.  

