
# Sets

## Learning Objectives 

- Students Will Be Able To:
    - Explain what a set is
	- Explain when one would want to use a set
    - Identify the common methods associated with sets

---
## Roadmap

* Setup
* Defining sets
* Why sets?
* Common set methods
* A practical use of sets for interviews
___

## Setup

* Clone down the starter code, install dependencies, and cd into project:
```
    $ git clone https://git.generalassemb.ly/shaw-kitajima/GA-Post-Course-CS.git
    $ cd GA-Post-Course-CS/
    $ npm i
    $ cd sets/
```

* run the tests
```
    $ npx mocha
```

* Open the project's folder in your code editor

---

## Sets

Welcome to sets, the blazingly fast cousins to arrays that are mega popular in data science and large scale applications! Sets, like arrays, are list-like data structures, but unlike arrays, sets ***cannot*** have duplicate values. 

Due to this requirement, sets are extremely useful in checking for inclusion of items.

Here is a silly, but practical example. Let's pretend we live in a world where we only have access to arrays and sets. If we created a shopping list, our set would like like:

```js
const set = ["loaf of bread", "yogurt", "carton of eggs", "lettuce", "scallions", "grapes", "tomato", "spaghetti"];
```

whereas our array would look like:

```js
const array = ["loaf of bread", "loaf of bread", "yogurt", "yogurt", "yogurt", "yogurt", "carton of eggs", "lettuce", "scallions", "grapes", "tomato", "tomato", "tomato", "spaghetti", "spaghetti"];

```

**❓ What is the benefit of the array?**

**❓ What is the benefit of the set?**

___ 

## Why Sets

### Unique Items

Let's say you created a new website, and you tracked all of the visits for your site. When we talk about user growth, we often want to track unique visitors to our site. If we tracked our logins via an array, we could see the same user multiple times. However, with sets, duplicate users would be removed:

![sets versus arrays](https://ga-instruction.s3.amazonaws.com/assets/tech/computer-science/sets/english/set1.png)

The set would make it very obvious who the unique visitors are!

### Inclusion

Additionally, as we discussed earlier, sets are great for checking for membership. Common uses for this might be checking:

* Is this username you are trying to create already taken in your database? 
* Can I add this tag to my blog post?

But don't arrays have an ``includes`` method? What' the point of using sets if you can already check for inclusion with arrays? The answer is speed.

When you are running an inclusion method on an array, the time complexity is based on iterating across the array to find the value.

However, in most programming languages, sets are not based on arrays, so the inclusion check for sets are on average, much faster than arrays. In fact, in Python, the membership check for a set has on average a O(1) time complexity using a data structure that we are already familiar with.

**❓ What data structure have we covered with, on average, O(1) search time complexity?**

___ 

## Common Set Methods

The following methods are commonly built into sets:

| Method | Description   |
| --------- |-----------| 
| ``length``      | Returns the length of the set. | 
| ``insert(value)``      | Adds a value to the set, unless it’s already present. | 
| ``remove(value)``      | Removes and returns a value from the set. | 
| ``has(value)``      | 	Returns true if the value is already in the set. | 
| ``union(set)``      | Returns a new set comprising the union between two previous sets (i.e., the combined values of both sets). | 
| ``intersect(set)``      | 	Returns a new set comprising the intersection between two previous sets (i.e., the values in both sets).| 
| ``difference(set)``      | Returns a new set comprising the difference between two sets (i.e., the values that only appeared in one of the two previous sets).| 

___

## Sets in Interviews

In most interviews, you won't be tasked in creating sets, but rather, using sets to solve a problem. Luckily, we won't need to create sets to solve set problems, because most languages, including Javascript, have Sets built into them

Sets in JS were added in ECMA2015, and the documentation for them can be found [here](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)!

So what kind of questions would we see in an interview? The typical questions are inclusion algorithms with a twist.

A classic example of this is any kind of algorithm where you have to find two things in a list that match some kind of criteria. Some examples would include: the two sum algorithm in [Leetcode](https://leetcode.com/problems/two-sum/) and the Inflight Entertainment algorithm in [Interviewcake](https://www.interviewcake.com/question/javascript/inflight-entertainment)

Let's talk about the two sum algorithm in [Leetcode](https://leetcode.com/problems/two-sum/)

The brute force approach for this problem would likely be to iterate across the nums array, and then for each element, iterate across the nums array again. If the elements on both iterations sum up to the target, and the indexes are not the same, we could return the indexes!

That code would probably look a little bit like:

```js
var twoSum = function(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = 0; j < nums.length; j++) {
      if (i !== j && nums[i] + nums[j] === target) {
          return [i, j];
      };
    }
  }
};
```

However, when we look at this, we already know that it would be ``O(N^2)`` time complexity. This doesn't sound good, does it?

In fact, Leetcode's results will us just how slow this is:

![Brute Force Leetcode Runtime](https://imgur.com/tMFgjZu.png)

 If an interviewer were to ask you this question, they don't really want to know if you can identify the brute force solution to this. Between us, it's not a particularly difficult question. Instead, they want to see if you can find a faster approach. 

Let's look at the pseudo-code now for a set approach and discuss how it works:

```
Create an empty set
For every element in the nums array:
    Calculate the element to look for
    If the set has the element:
        Return an array: [the current idx, the index of the element to look for]
    Add the element to the set
```

The core mechanics behind this solution rely on two things: knowing the value to look for if you know one value and the target, and taking the "look backwards" approach to the set

If two numbers add up to the target, basic algebra would also tell us that one of the numbers is the target minus the other number. 

The second thing we have to think about is how do we go about our set. The trick is to remember that sets are very fast for figuring out if a value is included - and we also could have duplicate values. By adding every element to the set after checking for the corresponding value, you can take advantage of set speed, without having to worry about mistakenly disqualifying duplicate values in different indexes!

Lo and behold, the Set solution on LeetCode yielded us:

![Set Leetcode Runtime](https://imgur.com/4fkLKGb.png)

Viva sets!

___
## Essential Questions

1. What is the number one rule for sets?
2. Why is searching for a value in a set faster than using the array.includes method to search for a value in an array?
