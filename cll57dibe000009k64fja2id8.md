---
title: "Slice() and Splice(): Let's Break It Down Like I'm Twelve"
datePublished: Thu Aug 10 2023 13:36:33 GMT+0000 (Coordinated Universal Time)
cuid: cll57dibe000009k64fja2id8
slug: slice-and-splice-lets-break-it-down-like-im-twelve
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1691679535577/4107e8aa-faec-4b81-8817-52da225e4bc7.png
tags: javascript, beginners, array, 2articles1week, javascript-splice

---

Imagine you have a basket of apples, and you want to share them with your friends. You might need to cut the apples into smaller pieces or take out a few slices. Well, in JavaScript, we have something similar called **slice** and **splice** methods. Don't worry if you're new to coding – these are your trusty tools to quickly chop up and rearrange lists of things, just like those apples. So, grab your coding apron, and let's start slicing and splicing arrays in JavaScript!

%[https://media.giphy.com/media/HPMAJ3Ezff9TfnDClQ/giphy.gif] 

### Prerequisites

While you don't need to be a coding expert, a few prerequisites will help you grasp the concepts more effectively.

1. Basic understanding of concepts like variables, variable assignment
    
2. Curiosity and willingness to experiment
    

## What is the slice( ) method in JavaScript?

The slice() method creates a new array by extracting a section from the current array. The original array remains untouched; instead, a new array holding the selected items is returned.

Picture cutting an apple into smaller pieces. You can apply slice() to separate a portion of an array, much like the apple, and move it to a new plate(). Nonetheless, the original array stays unaffected.

**Syntax:**

```javascript
array.slice(startIndex, endIndex);
```

**Parameters:**

* The startIndex is the point at which to start extracting items. It is optional and if omitted, will start from index 0 (Zero). If the startIndex is negative, it starts from the end of the array.
    
* The endIndex is the point up to which elements will be extracted. It extracts up to, but does not include the end index. Say the startIndex and endIndex are 1 and 3 respectively, the slice method extracts items from index 1 to index 2 but not index 3. The endIndex is optional. If omitted, the default is the length of the array.
    

```javascript
let fruits = ['apple', 'orange', 'banana', 'avocado', 'raspberry']
let slicedFruits1 = fruits.slice(1, 3) // Take out pieces from index 1 to 2
let slicedFruits2 = fruits.slice(2) // Take out pieces from index 2 to the end of the array
let slicedFruits3 = fruits.slice(-3, -1) // Extracts elements counting from the end, resulting 
                                         //in elements at index -3 and -2 from the end.

console.log(slicedFruits1) // The result is ['orange', 'banana']
console.log(slicedFruits2) // The result is ['banana', 'avocado', 'raspberry']
console.log(slicedFruits3) // The result is ['banana', 'avocado']
```

## Getting Started with Splice

The splice( ) method mutates the array it is called on. That is, it will change the original array and not return a new array like the slice( ) method. Say you have a string of beads and you want to add or remove some beads. The splice( ) method works the same way.

Unlike the slice ( ) method, the splice ( ) method can be used to remove or insert elements into an array

**Syntax:**

```javascript
array.splice(startIndex, deleteCount, item1, item2, ...);
```

**Parameters:**

* startIndex: This is the index at which to start modifying the array
    
* deleteCount: This is the number of items to be removed from the array starting from the startIndex. If set to 0 (Zero) nothing will be removed.
    
* item1, item2,...(optional): These are the items to be added to the array, starting from the startIndex. The items are included in the syntax for when you want to add items to the array
    

Usage:

```javascript
let fruits = ['apple', 'orange', 'banana', 'avocado', 'raspberry']

let splicedfruits1 = fruits.splice(1, 3);
let splicedfruits2 = fruits.splice(1, 0, 'mango', 'pear');
let splicedfruits3 = fruits.splice(2, 2, 'peach', 'melon');

console.log(splicedfruits1); //['orange', 'banana', 'avocado']
console.log(fruits); // ['apple', 'raspberry']

console.log(splicedfruits2); // []
console.log(fruits); //['apple', 'mango', 'pear', 'orange', 'banana', 'avocado', 'raspberry']

console.log(splicedfruits3); //['banana', 'avocado']
console.log(fruits); //['apple', 'orange', 'peach', 'melon', 'raspberry']
```

In the first example, splice(1, 3) removes 3 elements starting from index 1 and modifies the `fruits` array. In the second example, `splice(1, 0, 'mango', 'pear')` adds 'mango' and 'pear' without removing any element. In the third example, `splice(2, 2, 'peach', 'melon')` removes 2 elements starting from index 2 and adds 'peach' and 'melon'.

### Comparison between slice ( ) and splice ( ) methods

| slice ( ) | splice ( ) |
| --- | --- |
| Creates a new array and leaves the original array untouched | Modifies the original array by adding, removing or replacing items within the array |
| It takes two parameters: `startIndex` (where to start) and `endIndex` (where to stop, not included). | It takes at least three parameters: `startIndex`,`deleteCount` and `item1, item2, ...` |
| Use when you want to keep the original array intact and work with the subset of its element | Use it when you want to make direct changes to the array |

### Common Mistakes

One common error I used to make was neglecting to consider the return value. I think many beginners fall into this trap. The functions slice() and splice() actually have return values. Not realizing that can lead to using the wrong array in subsequent codes.

```javascript
const originalArray = [10, 20, 30, 40, 50];

originalArray.slice(1, 4); // Extracts elements [20, 30, 40], but result is not stored

originalArray.splice(2, 2); // Removes elements [30, 40], but result is not stored

console.log("Original Array:", originalArray); // Original array is: [10, 20, 50]
```

In this code, we use `slice()` and `splice()` methods without capturing their return values by assigning them to variables. As a result, the extracted elements from `slice()` and the removed elements from `splice()` are lost.

To avoid this, always capture the return value of these methods if you intend to work with the modified or extracted array. Here's the corrected code with return values captured:

```javascript
const originalArray = [10, 20, 30, 40, 50];

const slicedElements = originalArray.slice(1, 4); // Capture the result of slice()
const removedElements = originalArray.splice(2, 2); // Capture the result of splice()

console.log("Original Array:", originalArray); // Original array remains unchanged
console.log("Sliced Elements:", slicedElements); // [20, 30, 40]
console.log("Removed Elements:", removedElements); // [30, 40]
```

### **Key Takeaways:**

* Slice ( ): It's like taking a slice of a pizza. You get a piece, but the whole pizza stays as it is.
    
* Splice ( ): It's like rearranging beads on a string. You can add, remove, or replace beads, and the string changes.
    

### Practice Makes Perfect

Here is an exercise you can try:

Imagine you're building a simple to-do list application. Use the following array to represent tasks:

```javascript
let tasks = ['Buy groceries', 'Write report', 'Exercise', 'Read book', 'Call friend'];
```

1. Use the `slice()` method to extract tasks 2 to 4 (inclusive) and display them.
    
2. Use the `splice()` method to remove tasks 1 and 3, then add 'Go to the bank' and 'Plan weekend' at the end.
    
3. Print the modified `tasks` array.
    

Good luck!!

## Conclusion

In this article, we've met two handy helpers: Slice ( ) and `splice()`. Slice( ) is like getting apple slices without changing the apple itself – it extracts parts of arrays. On the other hand, splice( ) is like moving beads on a string, directly changing arrays by adding, removing, or replacing elements.

When you need a new array piece, go for `slice()`. When you want to shake things up in an array, use `splice()`. With these tools, you're good to go. Happy splicing and slicing!

Like and leave a comment. If you have questions, I'd be delighted to answer them.

## Additional Resources

* [Array.prototype.splice() - JavaScript | MDN (](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)[mozilla.org](http://mozilla.org)[)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/splice)
    
* [Array.prototype.slice() - JavaScript | MDN (](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)[mozilla.org](http://mozilla.org)[)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
    
* [JavaScript Array Slice vs Splice: the Difference Explained with Cake (](https://www.freecodecamp.org/news/javascript-array-slice-vs-splice-whats-the-difference/)[freecodecamp.org](http://freecodecamp.org)[)](https://www.freecodecamp.org/news/javascript-array-slice-vs-splice-whats-the-difference/)