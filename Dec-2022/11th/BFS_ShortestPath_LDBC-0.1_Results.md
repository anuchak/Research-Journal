# LDBC 0.1

The results of each query have been arranged as follows:
- The shortest hop path (starting from destination node ID to the source node ID)
- The highest execution time taken out of 5 runs
- The lowest execution time taken out of 5 runs

## 1-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256077 RETURN a;`  

866->0  
Time: 12.78ms (compiling), 15.01ms (executing)  
Time: 0.70ms (compiling), 28.77ms (executing)  
Time: 0.34ms (compiling), 6.15ms (executing)  

## 2-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256530 RETURN a;`  

70->866->0  
Time: 0.82ms (compiling), 14.50ms (executing)  
Time: 0.88ms (compiling), 7.19ms (executing)  

## 3-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256668 RETURN a;`  

653->70->866->0  
Time: 0.78ms (compiling), 14.65ms (executing)   
Time: 0.39ms (compiling), 6.66ms (executing)  

## 4-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256816 RETURN a;`  

1385->653->70->866->0  
Time: 0.32ms (compiling), 16.22ms (executing)  
Time: 0.96ms (compiling), 8.02ms (executing)  

## 5-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256862 RETURN a;`  

1284->1385->653->70->866->0  
Time: 0.74ms (compiling), 13.02ms (executing)  
Time: 0.74ms (compiling), 6.17ms (executing)  
