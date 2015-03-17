---
layout: post
title: Swift and insertion sort
---
Last time we [implemented] (http://yuryev.me/Swift-and-bubble-sort/) the simplest sorting algorithm. Next simple sorting algorithm is insertion sort. According to [wiki] (http://wikipedia.org/wiki/Insertion_sort) insertion sort is a simple sorting algorithm that builds the final sorted array (or list) one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort, heapsort, or merge sort.

Worst case performance О(n2) comparisons, swaps

Best case performance	O(n) comparisons, O(1) swaps

Average case performance О(n2) comparisons, swaps

Worst case space complexity О(n) total, O(1) auxiliary


Let's implement insertion sort with Swift. Open XCode and create new playground with Swift (or you may [download] (https://github.com/snyuryev/Swift-Sorting/tree/master/insertionSort.playground) playground and start playing with insertion sort). 

First of all we are going to start with sorting function - insertionSort. It takes unsorted array of integers and returns sorted array:

``` 
func insertionSort(#unsortedArray: [Int]) ->[Int] {
    var sorted = unsortedArray
    for var i = 1; i < sorted.count; i++ {
        var currentElement = sorted[i]
        var j = i - 1
        while j >= 0 && sorted[j] > currentElement {
            sorted[j+1] = sorted[j]
            sorted[j] = currentElement
            j--;
        }
    }
    return sorted
}
```

So let's use our insertionSort function. Declare variable with empty array of integers:

```
var unsorted: [Int] = []
```

Fill array with random values:

```
for i in 0...10 {
    unsorted.append(random()%100)
}
```

Print unsorted array - check that values are unsorted:

```
println(unsorted)
```

Declare the constant with the returned value from insertionSort function:

``` 
let insertionSorted = insertionSort(unsortedArray: unsorted)
```

Print our constant with sorted array:

``` 
println(insertionSorted)
```

In your playground you will see something similar with this screenshot:

![Insertion sort playground](https://raw.githubusercontent.com/snyuryev/snyuryev.github.io/master/images/insertionSortPlayground.png)



You may find other playgrounds in my [Swift sorting repository] (https://github.com/snyuryev/Swift-Sorting) on GitHub. 



