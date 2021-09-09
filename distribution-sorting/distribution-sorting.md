
# Distribution Sorting

## Learning Objectives
<br>

- Students Will Be Able To:
	- Explain the concept of distribution sorts
    - Explain how buckets sorts work
    - Explain how radix sorts work
    - Explain the time complexity of bucket sorts
    - Explain when one would want to use a bucket sort

---
## Roadmap

* Setup
* Comparison vs Distribution Sorts
* Bucket Sorts
* Radix Sorts
* When to Use Bucket Sorts

___

## Setup

* Clone down the starter code, install dependencies, and cd into project:
```
    $ git clone https://git.generalassemb.ly/shaw-kitajima/GA-Post-Course-CS.git
    $ cd GA-Post-Course-CS/
    $ npm i
    $ cd distribution-sorting/
```

* run the tests
```
    $ npx mocha
```

* Open the project's folder in your code editor

---

## Comparison and Distribution Sorts

### Comparison Sorts

``Comparison Sorts`` are sorts in which you compare two items and decide which one to put first. When you compare, you will have to choose what to compare against the other, ex: the values for numbers, the alphabet for words, or even the sizes for legos like below:

![lego comparison sort](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/intro-sorting/comparison.gif)

## Distribution Sorts
``Distribution Sorts`` are sorts in which you use some property of the item to decide where it fits. This usually results in us dividing items into groups based on some characteristic of the item. Back to lego blocks, we could group them by color:

![lego comparison sort](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/intro-sorting/distribution.gif)

***There is no better or worse for distribution and comparison sorts. They simply do different things, so what type of sorting method you use would be based on the data you are sorting, and the output you want***


___

## Bucket Sorts

Can you believe we are finally covering an actual distribution sort? Bucket sorts are a sorting algorithm that depends on splitting the data into buckets, sorting each bucket, and then gathering back everything from the buckets into a sorted list!

Let's look at an example and then review the mechanics at hand:

1. Let's start off with an array of ``[29, 25, 3, 49, 9, 37, 21, 43]``
2. We would now create an array of our buckets. We have eight elements in our array, so why don't we come up with 3 buckets: ``[[], [], []]``
3. Now let's figure out what to put in each bucket. Why don't we put the ranges of ``0-16`` in our first bucket, ``17-32`` in our second, and ``33-49`` in our third?
4. Placing our data into the buckets should yield ``[[3, 9], [29, 25, 21], [49, 37, 43]]``
5. Now we can sort each bucket to yield ``[[3, 9], [21, 25, 29], [37, 43, 49]]``
6. Finally, we can gather everything back into a single array ``[3, 9, 21, 25, 29, 37, 43, 49]``

### Visualizing our Bucket Sort

![bucket sort](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/distribution-sorts/diagram.png)

### The Mechanics of a Bucket Sort

When we are creating our bucket sort, some natural questions that we should ask are:
1. How many buckets am I creating?
2. How do I determine which bucket an item goes into?
3. How can I guarantee that combining the buckets will yield a sorted list?

Let's answer them one at a time:

<br>

***How many buckets am I creating***:

This question depends entirely on the data you are working with. If you are sorting alphabetically, why don't you create 26 buckets for each letter? If you are doing a ``radix`` sort (which will be discussed later), you would probably make ten buckets from ``0-9``. However, if you don't know what kind of data to always expect, a good rule of thumb is to use the square root of the number of items you are sorting.

<br>

***How do I determine which bucket an item goes into***:

Mathematics! You want to find out the range of numbers that each bucket should accept. The range of numbers for a bucket should always be lower than the range for its proceeding bucket! If you know the minimum and maximum numbers in the list, the range of each bucket would be: ``((max - min) / bucketCount) + 1``, rounded down. The first bucket would accept all numbers starting from the minimum value, up to the minimum value plus the range. The second bucket include the next ``range`` numbers, and so on!

Why do we add ``1`` to the end of the range? That's how we guarantee that the maximum value is within range of all of the buckets. Otherwise, the maximum value would not have a bucket to go to!

Now that you know the ranges for each button, you can do some arithmetic to figure out which index of your array of buckets to place an item into. Since the starting number for the buckets is not 0, but rather, the minimum value, the index would be ``(item - min) / range``, rounded down!

**Want proof?**

![Imgur](https://imgur.com/6BfPMZF.png)

<br>

***How can I guarantee that combining the buckets will yield a sorted list?***:

This all boils down to whether or not you placed your items in the appropriate buckets. The rule is that every item in a bucket should be less than every item in a proceeding bucket. Once every bucket is sorted, you will see that the last item in every bucket is always less than the first item in the next bucket!

<br>

### The Pseudocode for a Bucket Sort

```js
    // if the array has one or less element, return it (it is sorted)
    // calculate the count of buckets
    // create an array containing the count number of arrays
    // calculate the minimum value of the array
    // calculate the maximum value of the array
    // calculate the range
    // for each number in the array
        // calculate the index to push the number to
        // push the number to the index array of your array of arrays
    // sort each array within the parent array
    // combine the sorted arrays into one and return!
```

**❓ What is the time complexity of calculating the appropriate bucket to place a number into?**

**❓ What is the time complexity of a bucket sort?**


## Radix Sorts

This lesson will not go heavily into radix sorts, as they are pretty complicated (and the detailed mechanics are beyond the scope for most, if not all interviews). So without too far into the details, radix sorts work by placing items based on the individual digits in each number of your list. Then by starting at either the first digit (the ``most significant digit``), or the last digit (the ``least significant digit``), it sorts the values based on the digits until it's reached the other end of each number. Magically, when you have reached the end, your values are sorted

Let's take a look at this through an example:

1. Let's started off with an array: ``[270, 65, 30, 603, 3, 84]``, and start with their least significant digit: the ones' place
2. Sorting by the ones' place will yield: ``[270, 30, 603, 3, 84, 65]``
3. Then sort by the tens' place: ``[603, 3, 30, 65, 270, 84]``
4. Finally, sort by the hundreds' place: ``[3, 30, 65, 84, 270, 603]``

Absolute witchcraft.

The actual mechanics can be **visualized** [here](https://www.cs.usfca.edu/~galles/visualization/RadixSort.html)


___
## When To Use Bucket Sorts

Bucket Sorts are good for situations where:
* The data that you are sorting is uniformly distributed:
    * The more evenly the data is distributed between the buckets, the faster our algorithm is!
    * Conversely, clustered data is bad bad bad for bucket sorts!
* In situations where you have so much data, that you cannot store it in memory at one time
    * You can then store the items in different buckets (external files), and then sort those files independently


___
## Essential Questions
1. Is the bucket sort considered a comparison or a distribution sort?
2. Why would you want to evenly distribute your data into your buckets in a bucket sort?
