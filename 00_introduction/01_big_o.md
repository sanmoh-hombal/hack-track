# Introduction to Big O

> If you already understand big O notation, you can skip this article.

Before we talk about big O, it's important that we first understand what exactly an "algorithm" is, especially in 
the context of HackTrack.

An algorithm can be seen as a recipe for a computer to follow. It's a set of instructions that a computer will 
follow step-by-step to solve a problem.

Algorithms take an input and produce an output. The output will be the answer to a question regarding the input. 
For example, let's say you had a non-empty array of positive integers called `nums`, and you wanted to answer the 
question: "What is the largest number in `nums`?"

To answer this question, you would write an algorithm that takes an array called `nums` as **input**, and 
**outputs** the largest number in `nums`. Here is an example of such an algorithm:
    
1. Create a variable `max_num` and initialize it to `0`
2. Iterate over each element `num` in `nums`
3. If `num` is greater than `max_num`, update `max_num = num`
4. Output `max_num`

Here, we have written down a set of instructions that when followed, will solve the problem. We can now implement 
these instructions in code so that a computer can quickly solve the problem. There are some important requirements 
for algorithms in the context of HackTrack:

- Algorithms should be *deterministic*. Given the same **input**, the algorithm should **always** produce the same 
  **output**. Basically, there should be no randomness.
- The algorithm should be correct for any arbitrary valid **input**. In our example, we stated that `nums` is a 
  non-empty array of positive integers. There are infinitely many such arrays, and our algorithm works for **all** 
  of them. However, if nums contained negative numbers, the input would be invalid since we specifically required 
  positive integers. In face, our algorithm would break in such a case because we initialized `max_num` to `0`. If 
  `nums` were entirely negative, `max_num` would remain `0` since no negative number would be greater than `0`, 
  leading to an incorrect result. Instead, we should initialize `max_num` to the first element of `nums` to ensure 
  the maximum value is always selected from the array itself. 

---

## Big O

Big O is a notation used to describe the computational complexity of an algorithm. The computational complexity of 
an algorithm is split into two parts: time complexity and space complexity. The time complexity of an algorithm is 
the amount of time the algorithm needs to run relative to the input size. The space complexity of an algorithm is 
the amount of memory allocated by the algorithm when run relative to the input size.

> Typically, people care about the time complexity more than the space complexity, but both are important to know

Time complexity: as the input grows, how much longer does the algorithm take to complete ?

Space complexity: as the input grows, how much more memory does the algorithm use ?

## How complexity works

Complexity is described by a function (math formula). What should the arguments to this function be ?

The arguments are variables defined by the programmer, but they should represent values that change between 
different inputs, and these values should affect the algorithm. For example, the most common variable you'll see is 
n, which usually denotes the length of an input array or string. In the example above, we could say that n is equal 
to the length of `nums`

Here, "the length of `nums`" is a value that changes between inputs, and it directly affects the algorithm. The 
longer `nums` is, the more elements we need to iterate through, and thus the longer our algorithm will take to complete.

> Note that choosing the letter *n* to denote the value is arbitrary. There is no requirement that we use *n*, it's 
> just that *n* is commonly accepted standard that everyone uses. If you wanted, you could use a banana to represent 
> the length of `nums`. The programmer is the one who decides which variables represent what values.