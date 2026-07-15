for Binary Heap we first will do something with [[insert]](x), and remove_minimal_element()
Heap(Priority Queue) 
Heap another name is Priority Queue
contains  set of elements 
insert (x)
remove_minimal_element()
___
Heap
___
$1$ st method)
with basic array

![[Pasted image 20260320220931.png]]

when i *insert* something, i will just push_back and increase size of array

when i am *removing*:
![[Pasted image 20260320221024.png]]
first i'll find index of minimal element, then we will swap it with last element, and remove the last element of array. (good tactic btw)

![[Pasted image 20260320221144.png]]

it is first(and correct) [[implementation]] of Binary Heap
inserting is $O(1)$ , removing is $O(N)$
___
$2$ st method)
We will save array [[sorted]] from max to min(bcs mimimum element will be last one).
![[Pasted image 20260320221854.png]]
last one will be smallest.

when i am *removing*:
i'll just do [[pop_back]]

![[Pasted image 20260320222133.png]]


when i am *inserting*:
we will put it at last position(new position), then we will swap it with previous until it is smaller then previus.
![[Pasted image 20260320222303.png]]
[[insertion sort]] or [[bouble sort]] uses similar logic

inserting is $O(N)$, removing is $O(1)$
___
3 rd mehod(correct one):
Binary Heap
inserting and removing will be $O(N)$m

You have a [[Binary Tree]], for Binary Heap, i'll almost be full(expect leafs, from left to right they will be there).
![[Pasted image 20260320222917.png]]

Each node of the tree, will contain some element from set.
And we want to find minimum so we will storage them at almost sorted order, so every node will be`greater or equal` to their *parent* node:

![[Pasted image 20260320223448.png]]
with set:
![[Pasted image 20260320223602.png]]


Now, how can we store this binary tree at our code?
At normal [[Binary Tree]]'s we will have some complex algorithms, example array witch will say what are it's childaren.
but in this case, our tree will be same for fixed $n$, example at $n = 10$
![[Pasted image 20260320223924.png]]
and at every $n=10$, tree's structure will be same with this.
now if we want to storage this tree we will have this array named `h`:
![[Pasted image 20260320224232.png]]

if at tree we want to find number at index 4, it'll be $h[4]$

![[Pasted image 20260320224322.png]]

but how we can move at this array?
*WE WILL CALCULATE*
let's say you are at index $i$ 
left child will be: $2 \cdot i + 1$
right child will be: $2 \cdot i + 2$
parent: $\lfloor \frac{i - 1}{2} \rfloor$
this is true because tree is *full*. 

then if we want to *insert*:
we will add it to last layer's first empty node, and add it back of array `h`
![[Pasted image 20260320230517.png]]

code:
![[Pasted image 20260320230600.png]]

and you see there is broken property at 4-> 10
then we will swap nodes with index 4 and at index 10
after swap#1:
![[Pasted image 20260320230721.png]]

then it we need to fix nodes with index $1$ and $4$,  after swap:
![[Pasted image 20260320230828.png]]
and lastly we will check index $0$ and $1$, it will be fine so we will do nothing
!!!ATENTION!!! in video Pavel Marvin forget to change array but you must change it also
code:
![[Pasted image 20260320230955.png]]
(He inserted $2$ also but i will not write it but i'll give picture:)
![[Pasted image 20260320231157.png]]

then, how to remove minimal element, first it is obvious minimal element will be [[root]], now we need to remove minimal element(it will be more complicated), we will erase root, and say new element is last node we inserted
![[Pasted image 20260320231448.png]]

(last node was 15)

now only problem is you our properties not satisfied, so for fix this, we will select minimal children and swap it with current node(first was root then we will continue) and swap it with it's minimal child until properties satisfied:
![[Pasted image 20260320231848.png]]


code will be:
![[Pasted image 20260320232031.png]]
in the end return $h[n]$
___

Now we will use [[Binary Heap]] to do [[Heap Sort]] 