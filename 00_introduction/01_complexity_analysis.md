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

In the context of HackTrack, there are some common assumptions that we make. When dealing with integers, the larger 
the integer, the more time operations like addition, multiplication, or printing will take. While this is relevant 
in theory, we typically ignore this fact because the difference is practically very small, and treat all integers 
the same. If you are given an array of integers as an input, the only variable you would use is `n` to denote the 
length of the array. Technically, you could introduce another variable, let's say `k` which denotes the average 
value of the integers in the array. However, nobody does this.

When written, the function is wrapped by a capital O. Here are some example complexities:
- _O(n)_
- _O(n^2)_
- _O(2^n)_
- _O(log(n))_
- _O(n * m)_

> You might be thinking, what is _m_ ? Remember: we define the variables. As these are simply examples with no 
> associated problem, _m_ could denote any arbitrary variable. For example, we could have a problem where the input 
> is two arrays. _n_ could denote the length of one while _m_ could denote the length of the other.

These functions represent the complexity. For example, you would say "the time complexity of my algorithm is O(n)" 
or "The space complexity of my algorithm is O(n^2)".

## Calculating Complexity

Roughly, your function calculates the number of operations or amount of memory (depending on if you're analyzing 
time or space complexity, respectively) your algorithm consumes relative to the input size. Using the example from 
above (find largest in `nums`), we have a time complexity of _O(n)_. The algorithm involves iterating over each 
element in `nums`, so if we define _n_ as the length of `nums`, our algorithm uses approximately _n_ steps. If we 
pass an array with a length of `10`, it will perform approximately `10` steps. If we pass an array with a length of 
`10,000,000,000` it will perform approximately `10,000,000,000` steps.

> Time complexity is not meant to be an **exact** representation of the number of operations. For example, we needed to 
> initialize `max_num = 0` and we also needed to output `max_num` at the end. This, you could argue that for an 
> array of length `10`, we need to `12` operations. This is **not the point** of time complexity. The point of time 
> complexity is to describe how the number of operations changes as the input changes. The number of iterations we 
> do depends on `nums`, but initializing `max_num = 0` doesn't. Thus, we ignore it.

Being able to analyze an algorithm and calculate its time and space complexity is a crucial skill. Interviewers will 
**almost always** ask you for your algorithm's complexity to check that you actually understand your algorithm and 
didn't just memorize/copy the code. Being able to analyze an algorithm also enables you to determine what parts of 
it can be improved.

### Rules

There are few rules when it comes to calculating complexity. First, **we ignore constants**. That means _O(9999999n) 
= O(8n) = O(n) = O(n/500)_. Why do we do this ? Imagine you had two algorithms. Algorithm A uses approximately _n_ 
operations and algorithm B uses approximately _5n_ operations.

When _n_ = 100, algorithm A uses 100 operations and algorithm B uses 500 operations. What happens if we double _n_? 
Then A uses 200 operations and B uses 1000 operations. As you can see, when we double the value of _n_, both 
algorithms require double the amount of operations. If we were to 10x the value of _n_, then both algorithms would 
require 10x more operations.

Remember: the point of complexity is to analyze the algorithm **as the input changes**. We don't care that B is 5x 
slower than A. For both algorithms, as the input size increases, the number of operations increases **linearly**. 
That's what we care about. This, both algorithms are _O(n)_.

The second rule is that we consider the complexity as the variables **tend to infinity**. When we have 
addition/subtraction between terms of the **same** variable, we ignore all the terms except the most powerful one. 
For example, _O(2^n + n^2  - 500n) = O(2^n)_. Why ? Because as _n_ tends to infinity, _2^n_ becomes so large that 
the other two terms are effectively zero in comparison.

Let's say we had an algorithm that required _n + 500_ operations. It has a time complexity of _O(n)_. When _n_ is 
small, let's say _n = 5_, the _+500_ term is very significant - but we don't care about that. We need to perform the 
analysis as if _n_ is tending towards infinity and in that scenario, the _500_ is nothing.

> The best complexity possible is _O(1)_, called as "constant time" or "constant space". It means that the algorithm 
> ALWAYS uses the same amount of resources, regardless of the input.
> 
> Note that a constant time complexity doesn't necessarily mean that the algorithm is fast _(O(5000000) = O(1))_, it 
> just means that its runtime is independent of the input size.

When talking about complexity, there are normally three cases:
- Best case scenario
- Average case
- Worst case scenario

In most algorithms, all three of these will be equal, but some algorithms will have them differ. If you have to 
choose only one to represent the algorithm's time or space complexity, never choose the best case scenario. It is 
most correct to use the worst case scenario, but you should be able to talk about the difference between the cases.

## Analyzing time complexity

Let's look at some example algorithms in pseudocode and talk about their time complexities.

```python
# Given an integer array "arr" with length n
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in arr:
    print(num)
```
This algorithm has a time complexity of _O(n)_. In each for loop iteration, we are performing a print, which costs _O
(1)_. The for loop iterates _n_ times, which gives a time complexity of _O(1 * n) = O(n)_.

---

```python
# Given an integer array "arr" with length n
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
n = 10
for num in arr:
    for i in range(500000):
        print(num)
```
This algorithm has a time complexity of _O(n)_. In each inner for loop iteration, we are performing a print, which 
costs O(1). This for loop iterates 500,000 times, which means each outer for loop iteration costs _O(500000) = O(1)_.
The outer for loop iterates _n_ times, which gives a time complexity of _O(n)_.

Even though the first two algorithms _technically_ have the same time complexity, in reality the second algorithm is 
**much** slower than the first one. It's correct to say that the time complexity is _O(n)_, but it's imporatant to be 
able to discuss the differences between practicality and theory.

---

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
n = 10
for num in arr:
    for num2 in arr:
        print(num * num2)
```
This algorithm has a time complexity of _O(n^2)_. In each inner for loop iteration, we are performing a 
multiplication and print, which both cost O(1). The inner for loop runs _n_ times, which means each outer for loop 
iteration costs _O(n)_. The outer for loop runs _O(n)_ times, which gives a time complexity of _O(n*n) = O(n^2)_.

---

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr2 = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]

for num in arr:
    print(num)

for num in arr:
    print(num)

for num in arr2:
    print(num)
```
This algorithm has a time complexity of _O(n + m)_. The first two for loops both cost _O(n)_, whereas the final for 
loop costs _O(m)_. This gives a time complexity of _O(n + n + m) = O(2n + m) = O(n + m)_.

---

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for i in range(len(arr)):
    for j in range(i, len(arr)):
        print(arr[i] + arr[j])
```
This algorithm has a time complexity of _O(n^2)_. The inner for loop is dependent on what iteration the outer for 
loop is currently on. The first time the inner for loop is run, it runs _n_ times. The second time, it runs _n-1_ 
times, _n - 2_, _n -3_, and so on.

That means the total iterations is 1 + 2 + 3 + 4 + ... + n, which is the partial sum of this series which is equal 
to (n.(n+1))/2 = (n^2 + n)/2. In big O, this is _O(n^2)_ because the addition term in the numerator and the constant 
term in the denominator are both ignored.

---

### Logarithmic Time

A logarithm is the inverse operation to exponents. The time complexity _O(log n)_ is called logarithmic time and is 
**extremely** fast. A common time complexity is _O(n log n)_, which is reasonably fast for most problems and also 
the time complexity of efficient sorting algorithms.

Typically, the base of the logarithm will be `2`. This means that if your input is size `n`, then the algorithm will 
perform `x` operations where _2^x = n_. However, the base of the logarithm doesn't actually matter for big O, since 
all logarithms are related by a constant factor.

_O(log n)_ means that somewhere in your algorithm, the input is being reduced by a percentage at every step. A good 
example of this binary search, which is a searching algorithm that runs in _O(log n)_ time (there is a chapter 
dedicated to binary search later on). With binary search, we initially consider the entire input (`n` elements). 
After the first step, we only consider `n / 2` elements. After the second step, we only consider `n / 4` elements 
and so on. At each step, we are reducing out search space by 50%, which gives us a logarithmic time complexity.

---

## Analyzing Space Complexity

When you initialize variables like arrays or strings, your algorithm is allocating memory. We never count the space 
used by the input itself (it is bad practice to modify the input), and usually don't count the space used by the 
output (the answer) unless an interviewer asks us to.

> In the below examples, the code is only allocating memory so that we can analyze the space complexity, so we will 
> consider everything we allocate as part of the space complexity (there is no "answer")

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in arr:
    print(num)
```
This algorithm has a space complexity of _O(1)_. The only space allocated is an integer variable `num`, which is a 
constant relative to _n_.

---

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
doubled_arr = []
for num in arr:
    doubled_arr.append(num * 2)
```
This algorithm has a space complexity of _O(n)_. The array `doubled_arr` stores _n_ integers at the end of the 
algorithm.

---

```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr2 = [11, 12, 13, 14, 15, 16, 17, 18, 19, 20]
grid = []

for i in range(len(arr)):
    for j in range(len(arr2)):
        grid[i][j] = arr[i] * arr2[j]
```
This algorithm has a space complexity of _O(n * m)_. We are creating a `grid` that has dimensions _n * m_.

> In this course, we will talk extensively about time and space complexity. If it's a new concept to you, don't 
> worry - with practice, you will become more and more comfortable with analyzing algorithms on your own.
