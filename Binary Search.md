#topic #binary_search 

It allows us to quickly find a number(some target value) in a sorted array of numbers, or if there is a dictionary of words in dictionary we can look up a word.

Idea
---
Idea is ask about the middle element, if it's equal to the target value return its position, and terminate, otherwise go to left/right 

let say we have a sorted array 
```
a[] = {2, 3, 5, 6, 8, 10, 12}
```
with indexed from 0, and we are trying to find 10, we want to position of 10 at the array.

in our example first we have an array:
```
{2, 3, 5, 6, 8, 10, 12}
```
middle element is *6*, so it is smaller than *10* and our array sorted non-decreasing so our target must be at the right(if it exists). 

then our remaining array is:
```
{8, 10, 12}
```
our middle element is *10* so we will return our middle position.

if our array becomes empty target is not in the array.

there is example code of binary search:
```cpp
int x = 10; /// NOTE: our target
int a[] = {2, 3, 5, 6, 8, 10, 12};
int l = 0, r = n - 1, mid;
while (l <= r) {
	mid = l + (r - l) / 2;
	if (a[mid] == x) {
		return mid;
	}
	if (a[mid] < x) {
		l = mid + 1;
	} else {
		r = mid - 1;
	}
}
return -1; 
```

A problem:
---
you are given $x$ you must find is $x$ a square?

answer:
we can binary search value of square root of $x$, start from range $[0, x]$, at each step of binary search check if middle's square is equal to $x$ or not.

Time Complexity
---
At each step we are doing half of remaining job, so time camplexity is $\log(n)$ 

Harder problem
---
find smallest value that is greater or equal to $x$.

example :
$x = 4$ 
```
{2, 3, 5, 6, 8, 10, 12}
```
then answer is $5$.
if we do it like before, then when we check $6$, we will return it because it is greater/equal to $x$

note: some hacky fix is we can check previus number(because if it is not greater/equal than $x$ then we found it).

Real answer: 
you can restore one more verabile `ans`(it will store our best value that we met) and when we meet a position/value that satisfies condition we store it at ``ans`` .

at here when we check $6$ we will store it at `ans` and we will go on left side(because they are smaller than $6$) of $6$ and we will note terminate while, we will continue to searching better answer.

```cpp
int x = 4; /// NOTE: our target
int a[] = {2, 3, 5, 6, 8, 10, 12};
int l = 0, r = n - 1, mid, ans = -1;
while (l <= r) {
	mid = l + (r - l) / 2;
	if (a[mid] >= x) {
		ans = mid;
		r = mid - 1;
		/// return x; we will not return
	} else if (a[mid] < x) {
		l = mid + 1;
	} else {
		r = mid - 1;
	}
}
return ans; 

```

or better version:
```cpp
int x = 4; /// NOTE: our target
int a[] = {2, 3, 5, 6, 8, 10, 12};
int l = 0, r = n - 1, mid, ans = -1;
while (l <= r) {
	mid = l + (r - l) / 2;
	if (a[mid] >= x) {
		ans = mid; /// or a[mid] if it asks for value
		r = mid - 1;
	} else {
		l = mid + 1;
	} 
}
return ans; 

```

Rotated(shifted) array problem
---

somebody rotated(shifted) the sorted array, and you need to find the smallest element.

example we had an array:
```
a[] = {2, 3, 6, 7, 9, 16, 19}
```

then it is shifted 2 times to left:
```
a[] = {6, 7, 9, 16, 19, 2, 3}
```

answer:
for each number we can say it is True if it is greater than last one, and False if it smaller/equal
then we need to find first False in array that have True prefix.

Find Peak
---
The array increases and then decreases, Find the maximum.

example:
```
a[] = {2, 3, 4, 6, 9, 12, 11, 8, 4, 1}
```

we can say true, if is greater than previus, and false if it is not, and we can find last true.


sqrt(x) 2
---
Find sqrt(x) with some precision.

```cpp
int x = 7; /// NOTE: our target
float l = 0, r = n - 1, mid;
while (r - l > eps) {
	mid = l + (r - l) / 2;
	if (mid * mid < x) {tt
		l = mid;
	} else {
		r = mid;
	} 
}
return l + (r - l) / 2 ; 
```