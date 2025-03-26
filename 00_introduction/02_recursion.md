# Introduction to Recursion

> If you already understand recursion, you can skip this article.

Recursion is a problem-solving method. In code, recursion is implemented using a function that calls itself.

The opposite of a recursive algorithm would be an iterative algorithm. There is a branch of study that proves that 
any iterative algorithm can be written recursively. While iterative algorithms use for loops and while loops to 
simulate repetition, recursive algorithms use function calls to simulate the same logic.

Let's say that we wanted to print the numbers from 1 to 10. Here's some code for an iterative algorithm:
```python
arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
for num in arr:
    print(num)
```

Here's some code for an equivalent recursive algorithm:
```python
def print_num(num: int):
    print(num)
    print_num(num + 1)
    return

print_num(1)
```

Each call to `print_num` first prints `num` (which starts at 1), and then calls `print_num` again, but incrementing 
`i` (to print the next number).
> The first function call prints `1`, then calls `print_num(2)`. In `print_num(2)`, we print `2`, then call 
> `print_num(3)`, and so on.

However, this code is actually wrong. Do you see the problem ? The function calls will never stop! Running this code 
would print natural numbers infinitely (or until the computer exploded). The `return` line never gets reached 
because `print_num(num + 1)` comes before it.

We need what is called a **base case** to make the recursion stop. Base cases are conditions at the start of 
recursive functions that terminate the calls.
```python
def print_num(num: int):
    if num > 10:
        return

    print(num)
    print_num(num + 1)
    return

print_num(1)
```

> After we call `fn(10)`, we print `10` and call `fn(11)`. In the `fn(11)` call, we trigger the base case and return. So now 
> we are back in the call to `fn(10)` and move to the next line, which is the return statement. This makes us return 
> back to the `fn(9)` call and so on, until we eventually return from the `fn(1)` call and the algorithm terminates.

An important thing to understand about recursion is the order in which the code runs - the order in which the 
computer executes instructions. With an iterative program, it's easy - start at the top and go line by line. With 
recursion, it can get confusing because calls can cascade on top of each other. Let's print numbers again, but this 
time only up to 3. Let's also add another print statement and number the lines:
```python
def print_num(num: int):
    if num > 3:
        return

    print(num)
    print_num(num + 1)
    print(f"End of call where num = {num}")
    return

print_num(1)
```

If you ran this code, you would see the following in the output:
```text
1
2
3
End of call where num = 3
End of call where num = 2
End of call where num = 1
```

As you can see, the line where we print text is executed in reverse order. The original call `print_num(1)` first 
prints `1`, then calls to `print_num(2)`, which prints `2`, then to `print_num(3)`, which prints `3`. then calls to 
`print_num(4)`. Now, **this is the important part**: how recursion "moves" back "up". `print_num(4)` triggers the 
base case, which returns. We are now back in the function call where `num = 3` and **line 4** has finished, so we 
move to the **line 5** which prints `"End of call where num = 3"`. One that line runs, we move to the next line, 
which is a `return`. Now, we are back in the function call where `num = 2` and **line 4** line has finished, so 
again we move to the next line and print `"End of the call where num = 2"`. This repeats until the original 
function call to `print_num(1)` returns.

> Every function call "exists" until it returns. When we move to a different function call, the old one waits until 
> the new one returns. The order in which the calls happens is remembered, and the lines within the functions are 
> executed in order
> 
> Note that each function call also has its own local scope. So in the example above, when we call `print_num(3)`, 
> there are 3 "versions" of `num` simultaneously. The first call has `num = 1`, the second call has `num = 2`, and 
> the third call has `num = 3`. Let's say that we were to do `num += 1` in the `print_num(3)` call. Then `num` 
> becomes `4`, but only in the `print_num(3)` call. The other 2 "versions" of `num` are unaffected because they are 
> in different scopes.

### Breaking problems down

This printing example is pretty pointless - it's easier to use a for loop if you just want to print numbers. Where 
recursion shines is when you use it to break down a problem into "sub-problems", whose solutions can then be combined 
to solve the original problem.

Let's look at the Fibonacci numbers. The fibonaci numbers are a sequence of numbers starting with `0, 1`. Then, each 
number is defined as the sum of the previous two numbers. The first few Fibonacci numbers are `0, 1, 1, 2, 3, 5, 8`. 
More formally we have
```text
Fn = Fn-1 + Fn-2
```

This is called a **recurrence relation** - it's an equation that connects the terms together.

Let's use pseudocode to write a function `F(n)` that returns the nth fibonacci number (0 indexed). Don't forget we 
need base cases with any recursive function. In this case the base cases are explicitly defined:
`F(0) = 0` and `F(1) = 1`
```python
def F(n):
    if n <= 1:
        return n

    one_back = F(n - 1)
    two_back = F(n - 2)
    return one_back + two_back
```

Let's say that we wanted to find `F(3)`. Upon calling `F(3)`, we would see the following flow, with each indentation 
level representing a function call's scope:
```text
one_back = F(2)
    one_back = F(1)
        F(1) = 1
    two_back = F(0)
        F(0) = 0
    F(2) = one_back + two_back = 1
two_back = F(1)
    F(1) = 1
F(3) = one_back + two_back = 2
```

As you can see, we took the original problem `F(3)`, and broke it down into two smaller sub-problems - `F(2)` and `F
(1)`. By combining the recurrence relation and base cases, we can solve the sub-problems and use those solutions to 
solve the original problem.

This is the most common use of recursion - you have your recursive function **return the answer to the problem you're 
trying to solve for a given input**. In this example, the problem we're trying to solve for a given input is "With 
is the nth Fibonacci number?" As such, we designed our function to return a Fibonacci number, according to the input 
_n_. By determining the base cases and a recurrence relation, we can easily implement the function.

By following this idea, solving the sub-problems is easy - if we wanted the 100th Fibonacci number, we know by 
definition that it is the sum of the 99th and 98th Fibonacci number. On the function call to `F(100)`, we know that 
calling `F(99)` and `F(98)` will give us the answer.