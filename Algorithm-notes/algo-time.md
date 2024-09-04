# Algorithms

This is using primeagen's kata-machine(algorithm library)

## SEARCH

Means iteration over the data structure and finding the value from it

---

### Linear search

- means searching over a data structure from o to n (index 0 until the last index)
- this is the array.indexOf implementation under the hood
- it has a time complexity of O(n),linear, because as the input grows the iteration and computation grows

#### how the algorithm works?

1. you need to iterate over the array(data structure)
2. 1 by 1 you'll check if the iterated value is equal to the value you're looking for

---

### Binary Search

It is a halving technique of search. It means you need to get the high and the low and go to the mid point and check the value of that mid point if it is the value you are looking for, if it is you got the value, if it isn't then you need to identify if the **value <ins>of</ins> that mid point** is lower or higher **than your value** then choose accordingly. If the midpoint is lower than the value, you will proceed to do "halving" on the high part of the structure, else , go to the lower side.

**REMEMBER**:

- this approach is on the **assumption** that the array is **SORTED**. It wont work if it isn't.
- this approach is a O(logN) time complexity.
- you must not do a linear search in between of halving because that will make it to Big O(N) (worst case scenario = the value isn't there so have to do another halving and have to linear search, thus will grow linearly)

#### how the algorithm works?

1. you need to assign high and low point in order to know where to do the "halving"
2. assign a midpoint base on the high and low which will be, low+ (high - low) / 2
3. Identify if that mid point is higher or lower than the value that we are looking for.

- if the value is higher than the mid point, meaning from low point(index) until the midpoint is all lower than the value, hence you start "halving" from midpoint to the high point. If it is the case, low is now midpoint + 1(because there is not point to start at mid point since we know the value) and highpoint is the same, and start the search from there.
- if the value if lower than the midpoint, meaning from midpoint to highest point(last index) are all higher meaning we **exceeded**. So the midpoint now is the new high point and start halving from low + (high - low)/2

4. keeps on halving until the condition/value is found else return false(not found it)

### O($\sqrt{N}$) (two crystal search)

this search is about an optimized search, this is to solve a linear search(O(n) search). As usual this is only effective for certain condition which is the array must be **sorted**. This is useful for searching the first truthy value of the series of truthy and falsy.

#### how the algorithm works?

1. you need to get square root of the total index (length) of an array. Like:{Math.floor(Math.sqrt(array.length))}
2. we use floor to ensure we are getting the whole number for index
3. we can now iterate over the array by using the sqrt value as an index and as a iterator
   Example:

```js
const jumpIndex = Math.floor(Math.sqrt(array.length))

let i = jumpIndex
(;i<array.length;i+=jumpIndex){
   if(array[i]){break}
}
```

the reason the variable "i" is outside the for loop, is to access the last value of the square root jump instead of only accessing it by its own for loop scope it has to be taken out of the scope. This is important because this will serve as a stopping and reference point to where the iteration found the _truthy_ value.

4. after finding the last square root value on where the truthy value is. We now **have to go back** one square root jump (i -= jumpValue) to go back to the _last known value_ where when the falsy is and start the iteration from there until we find the truthy value.  
   This way the worst case scenario of our **SEARCH** is only O($\sqrt{N}$) because we only iterate from square root to square root(drop constant , hence sqrtN).
   Example:

```js
i -= jumpValue
(let j = 0; j<jumpValue && i < array.length; j++,i++){
   if(array[i]){
      return i
   }
}

```

the reason we need to specify `j < jumpValue` and `i < array.length` is to start over from where the iteration ended where we backtrack and `j++` and `i++` is the normal iteration where we need to check 1 by 1 if we find the value

---

## SORT

By the word itself sorting over the array by using algorithm

### Bubble sort

A sorting technique that will always sort the end of the array in every iteration. Meaning in every iteration of sorting in Bubble sort the end is always the first one that is being sorted, this is important because with this you can just always exclude the last index of the array and as you do the iteration you also increment the exclusion by +1 on every iteration(like length - i) until you reached the first index means everything is sorted.

It has a time complexity of O(n2) since your iteration is N then N-1 until N-N+1(first index). Meaning it will be `n(n+1)/2` because if you reverse the iteration it will be 1,2,3...N

#### how the algorithm woks?

1. iterate over the array
2. inside the iteration of array we iterate again(inner iteration) to compare each values in the array

- we check: if the current value is higher than the next value we switch places

3. in every iteration of the outer , the inner iteration should deduct -1 from the END of its length since the last index is already sorted
   Example:

```js
for (let i = 0; i < arr.length; i++) {
  // -1 - i : reduced in every (i)
  for (let j = 0; j < arr.length - 1 - i; j++) {
    // swapping logic
    if (arr[j] < arr[j + 1]) {
      const tempArr = arr[j]; // save the current value reference
      arr[j] = arr[j + 1];
      arr[j + 1] = tempArr; //since arr[j] have new value we get the reference of old value of arr[j]
    }
  }
}
```

### Quick Sort

A divide and conquer algorithm for sorting. It is somewhat similar to binary search where you eventually have to keep halving the array using the **pivot point** and segregate the low and high of pivot value until it became sorted.
It uses recursion since it have to keep on halving the array using the pivot point

#### how the algorithm woks?

1. Create two function which is the quick sort function and the partitioning, where you segregate the high and low
2. In partitioning function, setup an current low index where it is low - 1. The reason why it is low - 1 for bookkeeping purpose, meaning it is being used to keep track of the current low index.

- iterate over the array and compare every value of the array. If the value is lower than the pivot value increment the current low index and swap the compared value to the current low index. The compared index will now be at 0 index(on first comparison and the following swapped index will be place in consecutive order)
- if the value is higher we skip it.
- lastly, we increment again the current low index and now we swap the pivot value to that index and return the current low index

3. In quick sort function, this is where we do the recursion.

- First the base case is when the high and low is the same, by then , we finish the recursion.
- Then, get the pivot index from our partitioning function
- and now we can do the recursive twice for two sides and the pivot index must not be included since it is already sorted. First recursion is pivot index - 1 and the second recursion is pivot index + 1

![illustration for quicksort](./quicksort.jpg)

---

### Recursion

Think of it as a complicated domino effect

"base case" - you can treat it like a case to stop the recursion. Base Case is not only for when you achieved the goal of a function but it is better to put as much case as you can to stop the recursion in the base case to make the recursion process simple

Have 3 process for recursive case:
pre - logic that you can do before you recurs
recursion - is where you call the function over and over again until the base case got hit/triggered
post - a case/logic that you can do after recursion( this will fire when the recursion hit the base case)

![diagram for recursion example](./recursion-diagram.jpg)

![diagram for maze solver](./maze-solver.jpg)

---

## Tree Algorithms

### Depth-first Search(DFS)

It is a search that goes to the deepest node first, means, it uses a stack or recursion where from root you'll go left(or right) node then traverse down until you hit the last leaf of node and return.

It has three search pattern

- pre order search = this is where the root node will be executed first, since you'll hit the node and travel to left(or right) then after the left(or right) you go to the remaining part of the tree (branch)

[link to the code](../kata-machine/src/day1/BTPreOrder.ts)

- in order search = the root node will be executed at the middle because you'll traverse first in the left then after the left. You'll hit the node and then the right

[link to the code](../kata-machine/src/day1/BTInOrder.ts)

- post order search = the root is in the last, means , you'll traverse in the left then to the right and the root

[link to the code](../kata-machine/src/day1/BTPostOrder.ts)

![diagram for DFS](./DFS-search.jpg)

By doing this search you are retaining the shape of the tree because you have a pattern in searching, thus, DFS is good at comparing trees

### Breadth-First Search(BFS)

This is a tree search that traverse/search by level **(tree level search/traversal)**. It means that from root level then to another level and so on until you hit the last level of the tree. It uses Queue structure because what it does is, every time you visit a level you'll put/push it at the end of your search and you'll search from the start.

![BFS diagram](./BFS.jpg)

### Heap

#### Insertion O(logn)

When inserting a value for Heaps either max or low heap it always follow this pattern:

1. The value being inserted will always be at the end of an array. This makes it constant especially for Array List.
2. To maintain its structure(max/min) You have to bubble it,called Upheap(heapify up), up to/until it met the structure condition.
   - Max Heap: parent must be higher than the value being Upheaped.
   - Min Heap: parent must be lower than the value being Upheaped.

![heap insertion diagram](./MinHeapInsertion.jpg)

#### Deletion O(logN)

Deletion in Heap is the opposite with Insertion, it removes the value of index[0]/root but the implementation is different, and can be harder. Harder than insertion because of the rules/checks that you can to set.

1. First get the reference of the first index value , to be returned.
2. Now swap the first index to the last index, in JavaScript, you can now pop() it.
3. Now in the root (which was the last index value), we can now do bubble down (Down Heap) to maintain the structure of our heap.
4. This is where it became harder than insertion. We now check which value of left and right is the lowest(min heap)/highest(max heap). Since it is a complete Binary tree you can take advantage of its rule where it the filling must start from left to right. So when doing a check(especially for last node) if the Left child is empty, the right child is automatically empty.
5. Swap that value and keep on doing recursion (comparing parent,child and swap) until the structure is maintain or until you hit the leaf.

![heap deletion diagram](./MinHeapDeletion.jpg)

As you can notice the pattern here is mostly if not exactly the same with queue because heap operations is really a Priority queue

---
