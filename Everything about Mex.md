[YT tut](https://www.youtube.com/watch?v=JDuVLyKn7Yw)
[[mex]] is an obbreviation for minimum excluded 
mex({1, 2, 3 ,4, 5}) = 0
mex({0, 1, 2, 5, 10}) = 3

If there are N elements at array the mex at maximum can be N because you must have 0, 1, ... N - 1, and N to greater than this but it is impossible
![[Pasted image 20260508001507.png]]
this will help us because if $A[i] > N$ we can ignore it

we can find mex of array in $O(N)$ time with array that marks if we had it or not;

at changing [[set]] or [[multiset]] and with queries we can do:

1) Add $x$ to the set $O(\log n)$
2) Delete $y$ from the set $O(log n)$ 
3) Find the MEX of the set $O(\log n)$ 
we will store map that will say amount of elements(like frequency map)
and set: complement(set that says we don't have at map(multiset))
(NOTE that our set: complement initily stores elements from 0 to N )

when we add $x$:
1) we will increase frequency of $x$
2) if it is frequency was $0$(now it is $1$) we will erase it from our set: complement

when we delete $y$:
1) we will decrease frequency of $y$ 
2) if it is frequency is $0$(before it was $1$) we will insert it to our set: complement 

when we query:
	we will just print set: complements begin element

if we don't now $n$ we can have varebile that says current $n$ and when we add element we can increase it and if we don't have new $n$ at map we can insert it to set: complement 

if we don't have deletions query we can do it in linear time:
we will store unordered_map that is frequency 
and also additionaly we will support with varibile $k$ that says current mex.
when we increase frequency of $k$ we can continue(increase k) at unordered_map  until frequency of $k$ is zero this will be at most $O(\log  n)$ time because we only can increase $k$ at most $n$ times.

if we have complex(like increasing range) queries we can have [[SegmentTree]] rather than set: complement
___

there is also topic [[games_on_graphs]](games on ascylic graphs)

in this theory(Sprague–Grundy theory) we say that every game on ascyclic graph is equivelent to a nim with some number of stones which is called nimber. then the nimber of any vertex can be calculated as the mex of the nimbers of all its children. 

![[Pasted image 20260508003930.png]]


Let's say that we have a game on an a acyclic graph with $n$ vertices and $m$ edges. Then what are the maximum nimber in it? You can probably guess that they will be not bigger than $n - 1$ because any number is mex of no more than $n - 1$ numbers

But this is not the best estimate.
In fact all the game on the graph will be no more than $\sqrt{2 \cdot m}$

it is true because:
1) if the nimber of a vertex is $a$, than this vertex has a degree of at least $a$ because $a$ is the mex of the nimbers of its children, so there must be numbers $0, 1, 2, ... a - 1$ among the children
2) let there be a vertex $v$ with a nimber $k$. Then as we've already understood, it has children $0, 1, 2, ... k - 1$ but these vertices then have degrees of at  least $0, 1, 2, ... k - 1$. and also there is also our vertex v with a degree of at least $k$. so: $$m \geq 0 + 1 + 2 + ... + k = \frac{k \cdot (k + 1)}{2}>\frac{k^2}{2}$$
if we move 2 to the other side and get square root of equation we will get $\sqrt{2 \cdot m}$ and this is what we wanted to proof.

it can be aplaid more generaly to sets that we can say:
![[Pasted image 20260508005300.png]]


---
Mex on a segment of an array
everybody thinks we can only do  it in $O(n \cdot \sqrt{n})$ because it is given as MO's algorithm's practice.
 but we can do it at $O((n + q) \cdot \log n)$ TC using [[scan line]] and [[SegmentTree]].
 