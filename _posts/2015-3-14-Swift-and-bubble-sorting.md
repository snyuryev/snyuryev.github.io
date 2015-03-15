---
layout: post
title: Swift and bubble sorting
---

Today's topic is the simplest sorting algorithm - bubble sort. According to [wiki] (http://wikipedia.org/wiki/Bubble_sort) bubble sort is algorithm that repeatedly steps through the list to be sorted, compares each pair of adjacent items and swaps them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted. The algorithm, which is a comparison sort, is named for the way smaller elements "bubble" to the top of the list. 

Worst case performance O(n^2).

Best case performance	O(n).

Average case performance O(n^2).

Worst case space complexity O(1) auxiliary.

Let's implement bubble sort with Swift. Open XCode and create new playground with Swift (or you may [download] (https://github.com/snyuryev/Swift-Sorting/tree/master/bubbleSort.playground) playground and start playing with bubble sort). 

First of all we are going to start with sorting function - bubbleSort. It takes unsorted array of integers and returns sorted array:

``` swift
func bubbleSort(#unsortedArray: [Int]) ->[Int] {
    var sorted = unsortedArray
    for var i = 0; i < sorted.count-1; i++ {
        for var j = 0; j < sorted.count-i-1; j++ {
            if sorted[j] > sorted[j+1] {
                let a = sorted[j+1]
                sorted[j+1] = sorted[j]
                sorted[j] = a
            }
        }
    }
    return sorted
}
```

So let's use our bubbleSort function. Declare variable with empty array of strings:
``` swift
var unsorted: [Int] = []
```

Fill array with random values:
``` swift
for i in 0...10 {
    unsorted.append(random()%100)
}
```

Print unsorted array - check that values are unsorted:
``` swift
println(unsorted)
```

Declare the constant with the returned value from bubbleSort function:
``` swift
let bubbleSorted = bubbleSort(unsortedArray: unsorted)
```

Print our constant with sorted array:
``` swift
println(bubbleSorted)
```

In your playground you will see something similar with this screenshot:
![Bubble sort playground]({{ site.url }}/image/bubbleSortPlayground.png)

You may find other playgrounds in my [Swift sorting repository] (https://github.com/snyuryev/Swift-Sorting) on GitHub. 
