# LDBC 1

The results of each query have been arranged as follows:
- The shortest hop path (starting from destination node ID to the source node ID)
- The highest execution time taken out of 5 runs
- The lowest execution time taken out of 5 runs

## 2-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256530 RETURN a;`  

510->1701->0  
Time: 0.71ms (compiling), 73.31ms (executing)  
Time: 0.89ms (compiling), 67.10ms (executing)  

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256668 RETURN a;`  

4393->1701->0  
Time: 0.70ms (compiling), 140.01ms (executing)  
Time: 0.70ms (compiling), 66.74ms (executing)  

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256816 RETURN a;`  

8973->1701->0  
Time: 0.68ms (compiling), 137.45ms (executing)  
Time: 0.67ms (compiling), 66.16ms (executing)  

## 3-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023257255 RETURN a;`  

8382->8973->1701->0  
Time: 0.75ms (compiling), 73.77ms (executing)  
Time: 0.71ms (compiling), 66.87ms (executing)  

## 4-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257255 RETURN a;`  

8382->8973->1701->1907->1  
Time: 0.74ms (compiling), 79.11ms (executing)  
Time: 0.76ms (compiling), 63.67ms (executing)  

## 5-hop query

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 933 and b.ID = 2199023256077 RETURN a;`  

5712->9587->7803->1809->1701->0  
Time: 0.74ms (compiling), 120.23ms (executing)  
Time: 0.74ms (compiling), 54.98ms (executing)  

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257716 RETURN a;`  

2120->1310->7298->1701->1907->1  
Time: 0.72ms (compiling), 65.15ms (executing)  
Time: 0.71ms (compiling), 59.27ms (executing)  

`MATCH (a:Person)-[r:KNOWS*1..30]->(b:Person) WHERE a.ID = 1129 and b.ID = 2199023257939 RETURN a;`  

9403->6071->9505->9686->1907->1  
Time: 0.33ms (compiling), 67.27ms (executing)  
Time: 0.70ms (compiling), 56.52ms (executing)  

