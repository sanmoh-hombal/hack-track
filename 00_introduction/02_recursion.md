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
