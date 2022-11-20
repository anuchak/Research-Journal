## Query Syntax

`MATCH path=(n {id: 0})-[:CloseTo *WSHORTEST (r, n | n.total_USD)]-(m {id: 15}) RETURN path;`

`WSHORTEST` keyword being specified to indicate weighted shortest path algorithm to be applied.  
The return value is being bound to a variable of type `Path`. The property to be used as weight can be a _node property_ or _edge property_.  
In this query it is a node property `(r, n | n.total_USD)`. This leaves out the final target node's weight out.   

`MATCH path=(n {id: 0})-[:Type *WSHORTEST (r, n | r.weight)]-(m {id: 9}) RETURN path;`

The weight property here is the edge property `r.weight`. And a different edge being specified here.
Multiple relationships can be traversed by using `|`, the weight property needs to be there for all the edge types.  
For traversing over all relationships (homogeneous) the relationship label can be left out.

`MATCH path=(n {id: 0})-[:CloseTo *WSHORTEST (r, n | 1)]-(m {id: 15}) RETURN path;`

A weight of `1` is being assigned as de facto weight here, this is for _unweighted shortest path_.

`MATCH (n {id: 0})-[relationships:CloseTo *WSHORTEST (r, n | n.total_USD)]-(m {id: 9}) RETURN relationships;`

This query is returning the edges (relationships) and it has to be specified in the query pattern.

`MATCH path=(n {id: 0})-[relationships:CloseTo *WSHORTEST (r, n | n.total_USD)]-(m {id: 9}) UNWIND (nodes(path)) AS node RETURN node.id;`

This returns the nodes in the shortest path between source and target, `nodes(path)` is the notation.

`MATCH path=(n {id: 0})-[relationships:CloseTo *WSHORTEST (r, n | n.total_USD) total_weight]-(m {id: 9}) RETURN nodes(path), total_weight;`

To calculate the `total_weight` of the path, specify the variable in the match pattern (here the weight leaves out the last node's weight).

`MATCH path=(n {id: 0})-[:CloseTo *WSHORTEST 4 (r, n | n.total_USD) total_weight]-(m {id: 46}) RETURN path,total_weight;`

This notation `WSHORTEST 4 ` is used to limit the path's length, indicates 4 is the max len allowed.

`MATCH path=(n {id: 0})-[*WSHORTEST (r, n | n.total_USD) total_weight (r, n | r.eu_border = false AND n.drinks_USD < 15)]-(m {id: 46}) RETURN path,total_weight;`

To traverse with arbitrary filters applied to the relationship predicate can have additional filter lambdas added. Such as here it is,  
`(r, n | r.eu_border = false AND n.drinks_USD < 15)`. This is supposed to limit the graph expansion while traversal (otherwise they will enumerate and then filter).  

## Edge and Weight

Edge can be directed or undirected as specified in the pattern. Arbitrary edges can also be part of the shortest path, since the node property can be used as weight.  
Only +ve weight is supported since internally the function implements Dijkstra. Unweighted SP doesn't have any explicit function, just assign `1` to the edge.
No on the fly definition for the weight but both node property and edge property is supported.

## Algorithms supported

Apart from `WSHORTEST` another algo supported is `ALLSHORTEST` that finds all the shortest paths of same minimum weight between source and target.

## Query type allowed (sssd, ssad, etc.)

single source-single target, single source-all targets, all sources-all targets, arbitrary nodes & edges supported  

## Return type (`Path` or `Double`)

returns a `Path` type, the weight of the path can be calculated separately by specifying in the query
