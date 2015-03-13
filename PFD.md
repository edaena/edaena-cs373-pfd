# Project File Dependencies #

---

The Project File Dependencies problem was taken from the [Sphere Online Judge](http://www.spoj.pl/problems/PFDEP/). It consists on listing several tasks in the order they should be taken according to the tasks they depend on. The context of the problem is set to be on the UNIX utility _make_ and the project file that managers have to make to specify the components that depend on other tasks.


# Algorithm #

---

The main idea of the algorithm is to construct a [graph](http://en.wikipedia.org/wiki/Graph_%28mathematics%29) to keep track of the nodes and their dependencies. We then start with the following actions:

  1. Find the task that has no dependencies
  1. Store this task in a list
  1. Erase the task from the graph
  1. Erase the dependencies other nodes have with such task

Repeat these four tasks until there are no more nodes in the graph.


#### note ####
If there are two tasks with **zero dependencies** we choose the one that has the smallest number (name).



## Implementation ##
We first implemented the graph as an adjacency matrix. Here, both the row and column indexes represent the node number. If the value in position `graph[row][column]` is set to 1, it means that the number in row has a dependency on the column number.

**Disadvantage**: This solution was easy to implement, but it was slow.


The second implementation consisted on representing the graph as a _list_ containing _sets_. The index of the list indicates the number of the task, and the _sets_ in such position are the dependencies that the task has.

### Considerations ###
  * If there are no sets in a given position it means that the task has zero dependencies.
  * If a set at a given position in the list has a **None** value, it means that the task has been stored in the final ordered list.


**Advantage**: We avoided having to look at numerous elements to determine if a given node had no dependencies. This made the solution faster.





### Example ###
There are a total of 5 tasks, the dependencies of each task are as follows:

| **Task** | **Depends on** |
|:---------|:---------------|
| 3 | 1, 5 |
| 2 | 5, 3 |
| 4 | 1, 3 |
| 5 | 1|


As it can be seen, task **1** is not present in the table, this means that it has no dependencies. So this would be the first task to do.

Once task 1 has been finished it means that task 5 can be done. We proceed like this until we get the following result:

1 5 3 2 4

This indicates that task 1 should be done first, followed by 5 then 3 and so on.



### Graph ###
The graph for this problem the graph can be thought of as [acyclic and directed](http://en.wikipedia.org/wiki/Directed_acyclic_graph). That is, there are no cycles and one task1 depends on some other task2 but not vice versa.