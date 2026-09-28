# More on Sums
This supplemental material covers summation and is intended to help you understand how they work and how you can implement a loop to solve problems using summation.

## General Math Information
The symbol $$\sum$$ is the capital Greek letter sigma. Sigma is the Greek letter with the same sound as s. In math, $$\sum$$ is used to indicate summation - adding things together.

The summation operator often appears with an index (`i` in this example):

$$\sum_i$$

The index indicates a value that changes in each term of the summation (the subscript of `x` in this example):

$$\sum_{i}x_i=x_1+x_2+x_3+...$$

We can have a start and stop to the summation (`i=1` for start and `n` for stop in this example):

$$\sum_{i=1}^{n}i=1+2+...+n$$

The limits can include infinity:

$$\sum_{i=0}^{\infty}x_i=x_0+x_1+x_2+...+x_n+...$$

We can approximate functions using infinite sums:

$$\sin(x)=\sum_{n=0}^{\infty}\frac{(-1)^nx^{2n+1}}{(2n+1)!}=x-\frac{x^3}{3!}+\frac{x^5}{5!}-\frac{x^7}{7!}+...$$

$$\cos(x)=\sum_{n=0}^{\infty}\frac{(-1)^nx^{2n}}{(2n)!}=1-\frac{x^2}{2!}+\frac{x^4}{4!}-\frac{x^6}{6!}+...$$

Note: the above summations may only work for a specific range of `x`

Another note: Python uses infinite sums to approximate all of its special functions (in general, more complicated formulae than this)

## Using a Loop to Calculate a Sum
We can use a for loop to add up finite sums. A finite sum has finite (known) starting and stopping points.

Example: use Python code to calculate

$$\sum_{i=1}^{5}x^2$$
```python
s = 0
for i in range(1, 6):    # start at i=1, stop at i=5
    s_term = i ** 2      # calculate the ith term
    s += s_term          # add the term to the summation
print(s)
```

We can't add terms in an infinite sum forever - that would create an infinite loop! Instead we can take advantage of the fact that for these infinite summations to work (converge to a value) the terms must eventually become vanishingly small. For example, as $$n\rightarrow\infty$$ we have $$x_n\rightarrow0$$.

We stop a summation when some value is less than some tolerance. Sometimes this value is the absolute value of the *i*th term, sometimes it's the difference between the estimate and the true value. Either way, the tolerance is a small value specified by the programmer or user and determines the stopping point of an infinite summation. It's usually recommended to use absolute values because terms and differences may be positive or negative.

We can use a `while` loop when we don't know ahead of time how many terms we need to add, which means we don't know how many iterations we will need for the loop. The tolerance is used in the stopping (or continuation) condition of the while loop.

## Example
It can be shown that

$$\sum_{n=0}^{\infty}\frac{3}{(n+1)(2n+1)(4n+1)}=\pi$$

Write Python code that will use this series to calculate pi to within `1e-8` of the true value. We can use the math module to obtain the "true" value of $$\pi$$, but we won't always have a "true" value to compare with.

As described in lecture 5, start with comments of pseudocode:
```python
# get true value of pi

# get tolerance from user

# set up loop variables
# start loop
    # do math
    # check if we should stop

# print output
```

Then fill in the gaps with Python code. Use the pyramid style of programming and run / test / debug your code every few lines.
```python
# get true value of pi
from math import pi

# get tolerance from user
tol = float(input("Please enter a tolerance: "))

# set up loop variables
s = 0 # the summation
n = 0 # the index variable
keep_adding = True

# start loop
while keep_adding:
    # do math
    s_term = 3 / ((n + 1) * (2 * n + 1) * ( 4 * n + 1))
    s += s_term
    n += 1

    # check if we should stop
    if abs(s - pi) < tol:
        # we are done
        keep_adding = False

# print output
print(f"After {n} iterations, our value of pi is {s} while the true value is {pi}")
```

Using an input of `0.00000001`, the code above will produce the following output:
```
Please enter a tolerance: 0.00000001
After 4331 iterations, our value of pi is 3.1415926435942056 while the true value is 3.141592653589793
```
