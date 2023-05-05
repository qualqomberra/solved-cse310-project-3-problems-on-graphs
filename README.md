Download Link: https://assignmentchef.com/product/solved-cse310-project-3-problems-on-graphs
<br>
Problems on graphs are pervasive in computer science, and algorithms for working with them are fundamental. Hundreds of interesting computational problems are expressed in terms of graphs. This project examines the problem of how to compute shortest paths between vertices when each edge has an associated length or weight. Specifically, you will implement Dijkstra’s algorithm to find the shortest paths from a given source vertex to all other vertices in a graph. An efficient implementation of Dijkstra’s algorithm uses adjacency lists to represent the graph, and uses a min-priority queue of vertices, keyed by their current distance. This requires the implementation of a min-priority queue using a min-heap.

This project is an Accreditation Board for Engineering and Technology (ABET) required project as part of the accreditation process for our CS and CSE programs, and is not of my design.

<strong>Note: </strong>This project <strong>must </strong>be completed <strong>individually</strong>. Your implementation <strong>must </strong>use C/C++ and ultimately your code <strong>must </strong>run on the Linux machine general.asu.edu.

<strong>You must build all dynamic data structures, </strong><em>i.e.</em><strong>, the min-priority queue and the adjacency lists, by yourself from scratch. All memory management must be handled using only </strong>malloc <strong>and </strong>free<strong>, or </strong>new <strong>and </strong>delete<strong>. That is, you may not make use of any external libraries of any type for memory management! </strong>You may only use the standard libraries for I/O and string functions (stdio.h, stdlib.h, string.h, and their equivalents in C++). If you are in doubt about what you may use, ask me.

Remember that you <strong>must </strong>use a version control system as you develop your solution to this project. Your code repository must be private to prevent anyone from plagiarizing your work.

<h1>1           Implementation of Dijkstra’s Algorithm</h1>

As already stated, an efficient implementation of Dijkstra’s algorithm uses adjacency lists to represent the graph, and uses a min-priority queue of vertices, keyed by their current distance. Let’s recall the definition of a min-priority queue.

<h2>1.1         Min-Priority Queue</h2>

A priority queue is a data structure for maintaining a set <em>S </em>of elements, each with an associated value called a key. Priority queues come in two forms: Max-priority queues and min-priority queues. Our focus is on a min-priority queue because Dijkstra’s algorithm finds the shortest path to each vertex from a source, <em>i.e.</em>, it works to minimize the path length.

A min-priority queue supports four operations:

<ol>

 <li>Insert(<em>S,x</em>): Inserts the element <em>x </em>into the set <em>S</em>, which is equivalent to the operation <em>S </em>= <em>S </em>∪{<em>x</em>}.</li>

 <li>Minimum(<em>S</em>): Returns the element of <em>S </em>with the smallest key.</li>

 <li>Extract-Min(<em>S</em>): Removes and returns the element of <em>S </em>with the smallest key.</li>

 <li>Decrease-Key(<em>S,x,k</em>): Decreases the value of element <em>x</em>’s key to a new value <em>k</em>, where <em>k </em>is less than or equal to <em>x</em>’s current key value.</li>

</ol>

Not surprisingly, we can use a min-heap to implement a min-priority queue. In a given application, elements of a priority queue correspond to objects in the application. For Dijkstra’s algorithm, an element of a min-priority queue has three fields, corresponding to a vertex <em>v</em>, the predecessor of <em>v</em>, and the current known minimum distance to <em>v</em>. You are to build the priority queue keyed on the distance field of an element.

In this project, you must implement the functions of the min-priority queue using a min-heap. You should be able to adapt the functions of a max-heap discussed in class to implement a min-heap, and from them, the min-priority queue functions.

<h2>1.2         Dijkstra’s Algorithm</h2>

As you know, Dijkstra’s algorithm solves the single-source shortest-paths problem on a weighted, directed graph <em>G </em>= (<em>V,E</em>) for the case in which all edge weights are non-negative. Therefore, we assume <em>w</em>(<em>u,v</em>) ≥ 0 for each directed edge (<em>u,v</em>) ∈ <em>E</em>.

Dijkstra’s algorithm maintains a set <em>S </em>of vertices whose final shortest-path weights from the source <em>s </em>have already been determined. The algorithm repeatedly selects the vertex <em>u </em>∈ <em>V </em>− <em>S </em>with the minimum shortest-path estimate, adds <em>u </em>to <em>S</em>, and relaxes all edges leaving <em>u</em>.

You are to implement Dijkstra’s algorithm using the psuedocode that follows, using a min-priority queue <em>Q </em>of vertices keyed by their distance values, and an adjacency list representation for <em>G</em>. The functions Initialize-Single-Source and Relax were provided and discussed in class.

<strong>Algorithm 1 </strong>Dijkstra(<em>G,w,s</em>)

Initialize-Single-Source(<em>G,s</em>) {Initialize distance and predecessor of each vertex <em>v </em>∈ <em>V </em>}

<em>S </em>= ∅ {<em>S </em>is initially empty because no shortest-paths are determined yet}

<em>Q </em>= <em>V </em>{Use Insert(<em>Q,v</em>) to insert each vertex <em>v </em>∈ <em>V </em>into the min-priority queue <em>Q</em>} <strong>while </strong>( <em>Q </em>6= ∅ ) <strong>do</strong>

<em>u </em>= Extract-Min(<em>Q</em>) {Extract the vertex <em>u </em>with current minimum distance from <em>Q</em>} <em>S </em>= <em>S </em>∪{<em>u</em>} {Add <em>u </em>into the set <em>S </em>of vertices whose final shortest-path has been determined} <strong>for </strong>each vertex <em>v </em>adjacent to <em>u </em><strong>do</strong>

Relax(<em>u,v,w</em>) {If the distance to <em>v </em>decreases to <em>d</em><sup>0</sup>, then Decrease-Key(<em>Q,v,d</em><sup>0</sup>)} <strong>end for</strong>

<strong>end while</strong>

You are responsible for defining the structure (<em>i.e.</em>, struct) for the elements in the min-heap (and hence the min-priority queue), and the structure for the adjacency list representation of the graph. Be sure to place your definitions in appropriately named include files as described in §1.4.

<h2>1.3         Input and Output Format</h2>

First, your program is to read in a graph from stdin and construct its adjacency list representation. Recall that the adjacency list representation of a graph is an array (indexed by vertex), where the list for vertex <em>v </em>corresponds to a singly linked list of outgoing neighbours of <em>v </em>(the list of neighbours need not be ordered; you should be able to repurpose some of the you code for the hash table in Project 2).

In order to read the graph, the first line of input contains two integers <em>n </em>and <em>m</em>, which correspond to the number of vertices and the number of edges of the graph, respectively. This line is followed by <em>m </em>lines, where each line contains three integers: <em>u</em>, <em>v</em>, and <em>w</em>. These three integers indicate the information associated with an edge, <em>i.e.</em>, that there is a directed edge from <em>u </em>to <em>v </em>with weight <em>w</em>. Note that the vertices of the graph are indexed from 1 to <em>n </em>(and not from 0 to <em>n </em>− 1).

Following the input describing the graph, your program now processes commands, one per line. There are three commands:

<ul>

 <li>stop. On reading stop, your program must exit gracefully, with a return code of zero. Recall that, by convention, a return value of zero signals that all is well; non-zero values signal abnormal situations.</li>

 <li>write. On reading write, your program must write the graph to stdout. The output format of the write command is as follows: The first line should contain two integers, <em>n </em>and <em>m</em>, where <em>n </em>is the number of vertices and <em>m </em>is the number of edges in the graph, respectively. This line must be followed by <em>n </em>lines, one for each vertex. If vertex <em>u </em>has <em>k </em>neighbours (<em>u,v<sub>i</sub></em>) with weight <em>w<sub>i</sub></em>, 1 ≤ <em>i </em>≤ <em>k</em>, then for each vertex <em>u</em>, output:</li>

</ul>

<em>u </em>: (<em>v</em><sub>1</sub>;<em>w</em><sub>1</sub>);(<em>v</em><sub>2</sub>;<em>w</em><sub>2</sub>);<em>…</em>;(<em>v<sub>k</sub></em>;<em>w<sub>k</sub></em>)

<ul>

 <li>find s t flag, where flag is either zero or one.</li>

</ul>

On reading find s t 1, your program runs Dijkstra’s shortest path algorithm to compute the shortest path from s to t, and prints out the length of this shortest path to stdout. The information output format is:

LENGTH:<em>` </em>where <em>` </em>is the shortest path length.

On reading find s t 0, your program runs Dijkstra’s shortest path algorithm to compute a shortest path from s to t, and prints the actual path (sequence of vertices) to stdout. The information output format is:

PATH:<em>s</em>;<em>v</em><sub>1</sub>;<em>v</em><sub>2</sub>;<em>…</em>;<em>v<sub>k</sub></em>;<em>t</em>

where the sequence of vertices listed corresponds to the shortest path (<em>s,v</em><sub>1</sub>);(<em>v</em>1<em>,v</em><sub>2</sub>)<em>…</em>(<em>v<sub>k</sub>,t</em>) computed of length <em>k</em>.

While your program reads in only one graph, it may be asked to compute <em>s</em>–<em>t </em>shortest paths for many different source-destination pairs <em>s </em>and <em>t</em>. Therefore, during the computation of the <em>s</em>–<em>t </em>shortest path, your program must not modify the given graph.

<h2>1.4         Modular Design</h2>

You should use modular design for this project. At the minimum, you must have:

<ul>

 <li>the main program in the file cpp (and corresponding include file main.h),</li>

 <li>the implementation of the min-priority queue using a min-heap in the file cpp (and corresponding include file heap.h),</li>

 <li>the graph functions in the file cpp (and corresponding include file graph.h),</li>

 <li>any utility functions in the file cpp (and corresponding include file util.h),</li>

 <li>a makefile named makefile that compiles and links the individual executables into a single executable named dijkstra, when the command make dijkstra is executed.</li>

</ul>