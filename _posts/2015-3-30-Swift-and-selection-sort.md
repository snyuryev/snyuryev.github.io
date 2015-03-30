---
layout: post
title: Swift and selection sort
---
Last time we implemented [insertion sort] (http://yuryev.me/Swift-and-insertion-sort/) - simple sorting algorithm. Next  simple sorting algorithm is selection sort. According to [wiki] (http://wikipedia.org/wiki/Selection_sort) selection sort is a sorting algorithm, specifically an in-place comparison sort. The algorithm divides the input list into two parts: the sublist of items already sorted, which is built up from left to right at the front (left) of the list, and the sublist of items remaining to be sorted that occupy the rest of the list. Initially, the sorted sublist is empty and the unsorted sublist is the entire input list. The algorithm proceeds by finding the smallest (or largest, depending on sorting order) element in the unsorted sublist, exchanging it with the leftmost unsorted element (putting it in sorted order), and moving the sublist boundaries one element to the right.

Worst case performance О(n2)

Best case performance	О(n2)

Average case performance О(n2)

Worst case space complexity О(n) total, O(1) auxiliary


Let's implement selection sort with Swift. Open XCode and create new playground with Swift (or you may [download] (https://github.com/snyuryev/Swift-Sorting/tree/master/selectionSort.playground) playground and start playing with selection sort). 

First of all we are going to start with sorting function - selectionSort. It takes unsorted array of integers and returns sorted array:

``` 
func selectionSort(#unsortedArray: [Int]) ->[Int] {
    var sorted = unsortedArray
    for var i = 0; i < sorted.count-1; i++ {
        var indexMin = i
        for var j = i+1; j < sorted.count; j++ {
            if sorted[j] < sorted[indexMin] {
                indexMin = j
            }
        }
        if indexMin != i {
            let a = sorted[i]
            sorted[i] = sorted[indexMin]
            sorted[indexMin] = a
        }
    }
    return sorted
}
```

So let's use our selectionSort function. Declare variable with empty array of integers:

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

Declare the constant with the returned value from selectionSort function:

``` 
let selectionSorted = selectionSort(unsortedArray: unsorted)
```

Print our constant with sorted array:

``` 
println(selectionSorted)
```

In your playground you will see something similar with this screenshot:

![Selection sort playground](https://raw.githubusercontent.com/snyuryev/snyuryev.github.io/master/images/selectionSortPlayground.png)



You may find other playgrounds in my [Swift sorting repository] (https://github.com/snyuryev/Swift-Sorting) on GitHub. 



