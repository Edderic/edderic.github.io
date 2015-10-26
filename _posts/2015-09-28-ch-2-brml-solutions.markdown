# Personal Solutions to David Barber's Bayesian Reasoning and Machine Learning (Chapter 2)

## Exercise 2.1.

Consider an adjacency matrix A with elements \\([A]_\{i,j\} = 1\\) if one can
reach state \\(i\\) from state \\(j\\) in one timestep, and \\(0\\) otherwise.

Show that the matrix \\([A]_\{i,j\}^k\\) represents the number of paths that
lead from state \\(j\\) to \\(i\\) in \\(k\\) timesteps.  Hence derive an
algorithm that will find the minimum number of steps to get from state \\(j\\)
to state \\(i\\).

### Ans:

An example that satisfies (but does *not* prove) \\([A]_\{i,j\}^k\\) is \\(fig\ 2.2(a)\\).

In order to find the minimum number of steps to get from state \\(j\\) to state
\\(i\\), we should increase \\(k\\) in calculating \\([A]^k\\), such that
\\([A]^k_\{i,j\}\\) becomes non-zero.  \\(k\\) in that case will be the
smallest number of steps needed to get from state \\(j\\) to state \\(i\\).


## Exercise 2.2.
For an \\(N \times N\\) symmetric adjacency matrix \\(A\\), describe an algorithm to find the connected components. You may wish to examine `connectedComponents.m.`

### Ans:

The algorithm is as follows:

Start with an empty collection of connected components. For each row of the
adjacency matrix, find the nodes that are connected. Iterate through the
collection of connected compontents and see if there's a match. If there is
none, put the row's connected components as a new entry. If there are matches,
take the union of the matches along with the connected components specified by
the current row. Remove the components that have a match, and then add the
unioned components (as one big component) into the connected components
collection. At the end, you should have a collection of components, where each
component has nodes that are linked to each other.

See my implementation [here](https://github.com/Edderic/BRML-non-OOP/blob/master/ruby/lib/adjacency_matrix.rb) and tests [here](https://github.com/Edderic/BRML-non-OOP/blob/master/ruby/spec/adjacency_matrix_spec.rb)

## Exercise 2.3.

Show that for a connected graph that is singly-connected, the number of edges \\(E\\)
must be equal to the number of nodes minus \\(1\\), \\(E = V - 1\\). Give an example graph
with \\(E = V - 1\\) that is not singly-connected. Hence the condition \\(E = V - 1\\) is a
necessary but not sufficient condition for a graph to be singly-connected.

### Ans

Need to prove that All singly-connected graphs have the property \\(E = V - 1\\).

|# edges | # vertices | E = V - 1 | example
|------------------------------------------
|   0    |   1        | true      | x
|   1    |   2        | true      | x----y
|   2    |   3        | true      | x----y----z

#### Base case:

Let \\(v\\) be the number of vertices. Let \\(v = 1\\). In this case, the number of
edges must be \\(0\\). \\(0 = 1 - 1\\), so the base case satisfies \\(E = V - 1 \\).

#### Assumption step:

Let \\(V\\) be any arbitrary number \\(k\\). Let's assume that when \\(V\\) is
\\(k\\), the number of edges is \\(k-1\\). In other words:

$$
\begin{align}
E &= V - 1 \\
(k-1) &= (k) - 1
\end{align}
$$

#### Inductive step:

Let \\(V = k + 1 \\):

$$
\begin{align}
(k-1) &= (k) - 1 \\
((k+1)-1) &= ((k+1)) - 1 \\
k &= k
\end{align}
$$

Thus all singly-connected graphs must have the property \\(E = V - 1\\).

An example of a non-singly-connected graph that satisfies \\(E = V - 1\\) is the following:

<figure>
   <img src="/images/multiply-connected-e-equals-v-minus-1.png" alt="Non-singly connected graph">
<figcaption>Non-singly connected graph
</figcaption>
</figure>

In this particular case, we have two components. One component is cyclical
(thus not singly-connected) while the other is an island. Thus \\(E = V - 1\\) property
is necessary but not sufficient to prove that a graph is singly-connected.

## Example 2.4

Describe a procedure to determine if a graph is singly-connected.

### Ans

A graph is singly-connected if any node can reach another (or itself) only one way. An algorithm
to determine a graph's singly-connectedness is by using some tree-traversing algorithm (such as
Depth-First Search or Breadth-First Search).

1. Keep a tally of visited nodes.
2. Traverse the tree, starting at a node.
3. At each node, see if all the adjacent nodes have been visited before.
- If it has, then there is a cycle, so it must not be a singly-connected graph. Return.
- If it hasn't, just add the approached node to the list of visited nodes.
- Keep on going until all nodes have been traversed, or until a cycle has been discovered.

## Example 2.5

Describe a procedure to determine all the ancestors of a set of nodes in a DAG.

### Ans

For each node in the set of nodes, keep a list of "branches" that lets a root
node reach each node in that set of nodes. Starting from a node in the set of
nodes, we traverse the parent recursively until we reach a root node. When we
reach a root node, then we have one full traversed branch. We keep a running
list of traversed branches. We are done once we've traversed all the paths up
to root node(s) for each node in the nodes of interest.

## Example 2.6

`WikiAdjSmall.mat` contains a random selection of \\(1000\\) Wiki authors, with
a link between two authors if they ‘know’ each other (see
[snap.stanford.edu/data/wiki-Vote.html](snap.stanford.edu/data/wiki-Vote.html)).
Assume that if \\(i\\) ‘knows’ \\(j\\), then \\(j\\) ‘knows’ \\(i\\). Plot a
histogram of the separation (the length of the path between two users on the
graph corresponding to the adjacency matrix) between all users based on
separations from \\(1\\) to \\(20\\).  That is the bin \\(n(s)\\) in the histogram contains
the number of pairs with separation \\(s\\).

### Ans

The problem is essentially asking us to compute \\(A^k\\) where \\(k\\) is in
the range \\([1..20]\\).

$$
A^k_{i,j}
$$

lets us know how many paths one could take in order to get from \\(i\\) to
\\(j\\) in \\(k\\) steps.

When calculating the histogram, if \\(A^k_\{i,j\}\\) is greater than zero, then
we increase the \\(k^{th}\\) bin. Otherwise, we don't increase the latter.

<figure>
<img src="/images/degrees-of-separation-among-wikipedia-authors.png" alt="Degrees of Separation Among Wikipedia Authors">
<figcaption>Degrees of Separation Among Wikipedia Authors</figcaption>
</figure>

The S-shaped curve does not look surprising. The graph is most likely cyclical
and thus an arbitrarily-chosen author \\(i\\) and arbitrarily-chosen author
\\(j\\) might have several degrees of separation.  For example, let's say that
\\(i\\) and \\(j\\) are separated by one edge. It's also very likely that they
might know someone in common, author \\(l\\), so that \\(i\\) and \\(j\\) can
also be reached in two steps, etc.

## Example 2.7

The file `cliques.mat` contains a list of \\(100\\) cliques defined on a graph
of \\(10\\) nodes. Your task is to return a set of unique maximal cliques,
eliminating cliques that are wholly contained within another. Once you have
found a clique, you can represent it in binary form as, for example
(\\(1110011110\\)) which says that this clique contains variables \\(1, 2, 3, 6, 7, 8,
9\\), reading from left to right. Converting this binary representation to decimal
(with the rightmost bit being the units and the leftmost \\(29\\)) this corresponds
to the number \\(926\\). Using this decimal representation, write the list of unique
cliques, ordered from lowest decimal representation to highest. Describe fully
the stages of the algorithm you use to find these unique cliques. Hint: you may
find examining `uniquepots.m` useful.

### Ans

I was able to find 15 unique maximal cliques. They are

$$
[1,2,3,5,6,7,9]
$$

$$
 [4,5,6,8,9,10]
$$

$$
 [1,3,5,6,7,8,9,10]
$$

$$
 [1,2,5,6,7,8,9,10]
$$

$$
 [1,2,4,5,6,7,8,10]
$$

$$
 [1,2,4,5,6,8,9]
$$

$$
 [2,3,5,6,7,8,9,10]
$$

$$
 [2,3,4,5,8,9,10]
$$

$$
 [1,3,4,5,6,9,10]
$$

$$
 [1,2,4,6,7,8,9,10]
$$

$$
 [2,3,4,7,8,9,10]
$$

$$
 [1,2,3,4,5,7,8,9]
$$

$$
 [1,2,3,4,6,8,9,10]
$$

$$
 [1,3,4,5,7,8,9,10]
$$

$$
 [1,3,4,5,6,7,8,10]
$$

When sorted in decimals, they are: \\(119\\), \\(447\\), \\(463\\), \\(487\\),
\\(703\\), \\(751\\), \\(755\\), \\(765\\), \\(831\\), \\(863\\), \\(886\\),
\\(893\\), \\(954\\), \\(983\\), \\(1006\\).

My steps for finding the unique maximal cliques were as follows.

     For each clique,
       see if is a subset of another.
       if not a subset, then
         it must be a maximal clique.
         store this clique.

     To see if a clique is a subset of another,
        Take the intersections of the two cliques.
        If the intersection length is the same as
          the current clique, and
          the clique we are comparing to is not
          the same as the current clique, then
          the current clique is a subset
          (and is not a maximal clique.)

For more details, see this [notebook](https://github.com/Edderic/BRML-julia/blob/master/Cliques.ipynb)

## Example 2.8

Explain how to construct a graph with \\(N\\) nodes, where \\(N\\) is even, that contains
at least \\((N/2)^2\\) maximal cliques.

### Ans

When there are two nodes, it is very simple. Connecting the two nodes satisfies
the \\((N/2)^2\\) maximal cliques constraint, where the maximal clique length for
all cliques is 1.

When there are more than two nodes, we create an \\(N\\)-gon. In the case of \\(4\\) nodes,
we create a square, and that is enough to satisfy the constraint.

| \\(N\\) | \\((N/2)^2\\) |
| 2 |    1    |
| 4 |    4    |
| 6 |    9    |
| 8 |   16    |

Having even number of nodes greater than four makes the arrangement more interesting.
We still create \\(N\\)-gons, but we also connect nodes to form trapezoids
inside the \\(N\\)-gons. See the third and fourth example below.

<figure>
   <img src="/images/n-over-2-squared-cliques.svg" alt="Examples of graphs that satisfy the maximal cliques constraint">
<figcaption>Examples of graphs that satisfy the maximal cliques constraint
</figcaption>
</figure>


## Exercise 2.9

Let \\(N\\) be divisible by \\(3\\). Construct a graph with \\(N\\) nodes by partitioning the
nodes into \\(N/3\\) subsets, each subset containing \\(3\\) nodes. Then connect all nodes,
provided they are not in the same subset. Show that such a graph has \\(3N/3\\)
maximal cliques. This shows that a graph can have an exponentially large number
of maximal cliques.

### Ans

When \\(N\\) is greater than \\(3\\) and is divisible by \\(3\\), for any arbitrary graph,
it seems that we will have \\(3N/3\\) maximal cliques. One can see that the second and third
examples below show the exponential growth.

<figure>
   <img src="/images/exponential-growth-of-maximal-cliques.svg" alt="Exponential growth of maximal cliques">
<figcaption>Exponential growth of maximal cliques
</figcaption>
</figure>

## Exercise 2.10

A jewel was stolen from a room during a party. Each of the guests
(\\(A\\),\\(B\\),\\(C\\),\\(D\\),\\(E\\),\\(F\\)) enters the room, stays for
some time, and leaves. The testimonies they gave to the police are:

1. \\(A\\): I was present in the room with \\(E\\), \\(B\\)
2. \\(B\\): I was present in the room with \\(A\\), \\(F\\) and \\(E\\)
3. \\(C\\): I was present in the room with \\(F\\) and \\(D\\)
4. \\(D\\): I was present in the room with \\(A\\) and \\(F\\)
5. \\(E\\): I was present in the room with \\(C\\)
6. \\(F\\): I was present in the room with \\(C\\) and \\(E\\)

One of the statements in the testimonies is false. Which is it?

Notes:

If any two people are present in the room at the same time, then at least one
of them will report the fact that he was present in the room with the other
person. Each above testimony should be interpreted as, for example:

\\(A\\): I was present in the room with \\(E\\). I was present in the room with
\\(B\\). It does not necessarily mean that A was simultaneously present in the
room with both \\(E\\) and \\(B\\) (so \\(A\\) and \\(B\\) could have been
present in the room at some time \\(t_1\\), and \\(A\\) and \\(E\\) present in
the room at some other time \\(t_2\\). The other testimonies have a similar
interpretation.

The testimonies could be partially false. If \\(X\\) says that he was present in the
room with \\(Y\\) and \\(Z\\), it could be that the statement \\(X\\) was present in the room
with \\(Y\\) is true, but X was present in the room with \\(Z\\) is false.

<figure>
   <img src="/images/all-testimonies-jewelry.svg" alt="All testimonies">
<figcaption>All testimonies</figcaption>
</figure>

The direction of an arrow depicts who is claiming to have been with whom.
For example, \\(A\\) pointing to \\(B\\) means that \\(A\\) claimed to
be with person \\(B\\).

Since we know that only one statement is false, we can assume that
bidirectional edges are true (e.g. both \\(A\\) and \\(B\\) were definitely
together). Both statements have to be true because if one person were lying,
then the other person must have lied too, which violates the constraint that
only one statement is false. Thus, we know that \\(A\\) must have been in the
room with \\(B\\), and \\(F\\) and \\(C\\) must also have been together.


<figure>
   <img src="/images/d_lied_about_being_with_a_and_f.svg" alt="D lied about being with A and F">
<figcaption>D lied about being with A and F</figcaption>
</figure>

We know that \\(D\\) lied about being with \\(A\\) and \\(F\\) because if \\(D\\)
was actually with \\(A\\) and \\(F\\), then \\(D\\) would have to have been in
the room with \\(B\\) and \\(E\\) as well, but \\(D\\) did not say anything
about being with those two, and vice versa. Therefore, we should be more
suspicious of \\(D\\).
