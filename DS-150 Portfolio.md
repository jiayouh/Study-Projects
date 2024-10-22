# DS-150 Portfolio
## Table of Contents
- Assignment 6a, Task 5 Plotting some functions
    - Explanation of Code
    - Results of polynomial function
- Assignment 4, Task 2 (Computing): Collatz Sequences
    - What is the Collatz Sequence?
    - Explanation of Code 
    - Results of Collatz Sequence Function
- Assignment 3b, Task 5: Solving equations using bisection
    - What is the bisection method?
    - Explanation of Code 
    - Results of Bisection Methood
    
## Assignment 6a, Task 5 (Computing) Plot some functions
This block of code plots 5 different polynomial functions using NumPy and Matplotlib to do so. 

### Explanation of Code 
- import relevant libraries 
	- NumPy
	- Matplotlib
- Variable Initialization
	- `num_x` is set to 100 as the number of points on the x-axis
	- `x`  creates an array of 100 equally spaced points between 0 and 1
	- `function_values` creates an empty array with a shape (5,100) to store function values
	- `num_polys` represents the number of polynomials (we have 5 polynomials)
	- `y` creates an empty array with a shape (5,100) to store the polynomial function values
- Calculating polynomials and storing
	- the loop calculates the values of each polynomial function
	- the results are stored in `function_values` array
	- each row calculates a different polynomial function
-Plotting
	-using Matplotlib, iterate through each polynomial in `y` and plot correspondingly to `x` value 
	-add a legend to the plot
	-save the plot as an image file 
```
import numpy as np
import matplotlib.pyplot as plt

num_x = 100
x = np.linspace(0,1,100)
function_values = np.empty((5,100))
num_polys = 5
y = np.empty((num_polys,num_x))

  

for p in  range(0, num_polys):
function_values[0,:] = 2*(x-(1/2))
function_values[1,:] = ((3**2)/2)*(x-(1/3))*(x-(2/3))
function_values[2,:] = ((4**3)/(2*3))*(x-(1/4))*(x-(2/4))*(x-(3/4))
function_values[3,:] = ((5**4)/(2*3*4))*(x-(1/5))*(x-(2/5))*(x-(3/5))*(x-(4/5))
function_values[4,:] = ((6**5)/(2*3*4*5))*(x-(1/6))*(x-(2/6))*(x-(3/6))*(x-(4/6))*(x-(5/6))

y[p, :] = function_values[p, :]

#plotting
fig, ax = plt.subplots(1,1)
for p in  range(0,num_polys):
ax.plot(x,y[p,:],label=f'$x^{p}$')
ax.legend()
fig.savefig("DOLNY_plot_assign6a_task5.png")
```
### Results of Plotting Polynomial Functions
![Alt text](DOLNY_plot_assign6a_task5.jpg)

## Assignment 4, Task 2 (Computing): Collatz Sequences
This block of code computes the Collatz sequence if the user were to enter any positive arbitrary number and then returns those values in a list for the user starting from the number that the user inputs. 

#### What is the Collatz Sequence?
The Collatz Sequence is a sequence of numbers that can be generated from any positive number and follows two rules:

- if the number is even, divide by 2 
	- n/2
- if the number is odd, triple it and add one
	- n*3 + 1
Eventually, if one keeps following this pattern, then you will end on the number 1. 

### Explanation of Code 
- Parameters
	- `n` - a positive arbitrary integer
- Errors
	- TypeError is raised if n is not an integer
	- ValueError is raised if n is not positive 
	
- `def collatz_sequence(n)`
	- define the function
- `invalid(n)` 
	- raises errors in the case user input isn't correct
- `collatz_list = []`
	- create an empty list 
- `collatz_list.append(n)`
	- append the user input to the empty list that will be returned later
- While n is greater than 1 
	- if the number is odd, we will divide `n` by 
	- but if the number is even, then we will triple `n`  and add 1
*NOTE 
the condition is set as n is greater than 1 because we know that 1 is the last number of the collatz sequence, so this loop will continue until `n = 1`
- Finally, we return the list of the collatz sequence
```
def  invalid(n):
	if n != int(n):
	raise  TypeError ('n is not an integer')

if n <= 0:
	raise  ValueError('integer is not positive')

def  even_odd(n):
	if n%2==0:
		return  True
	else:
		return  False
def  collatz_sequence(n):
invalid(n)
collatz_list = []
collatz_list.append(n)
while n > 1: #trying to emulate do-while loop
	if even_odd(n):
		n = n//2
	else:
		n = 3*n+1
collatz_list.append(n)
return collatz_list
```

### Results of Collatz Sequence Function
#### Calling the Collatz Sequence Function
```
collatz_sequence(13)
collatz_sequence(50)
collatz_sequence(37)
```
#### Output
```
[[1], [2, 1], [3, 10, 5, 16, 8, 4, 2, 1]]
```
## Assignment 3b, Task 5: Solving equations using bisection
The bisection method finds the roots of a function by repeatedly dividing the interval where the root lies in half, and then checking to see if the midpoint if the interval is the root. This process repeats itself until the root is found within the desired tolerance.

### What is the bisection method?
The bisection method finds the roots of a function by repeatedly dividing the interval where the root lies in half, and then checking to see if the midpoint if the interval is the root. This process repeats itself until the root is found within the desired tolerance.


### Explanation of Code 
- Parameters
	- `desired_output`
	- `f`
	- `x0` lower bound of interval
	- `x1` upper bound of interval
	- `tolerance` desired range that we want the root to be within
- Errors
	- `if x0 > x1`
		- raises a ValueError that the interval x0 and x1 is out of order
	- if not is_inside_interval
		- raises a ValueError that the interval doesn't contain a root or there are 			multiple roots
		
#### Core Loop
- While the absolute value of `x0-x1` is greater than the tolerance
	- Cut the interval between `x0` and `x1` in half 
		- `xmid = (x0+x1)/2`
- Check if the desired output is within the left or right sub-interval 
		-`x0` or `x1` updates to become `xmid` as the interval narrows down
- We exit the loop once the difference between `x0` and `x1` is within the desired tolerance and returns the root as `xmid`
	


```
def is_inside_interval (n, a, b): #bool = is_inside_interval(n, a,b)
    def proper_interval(n,a,b):
        if n >= a and n <= b:  
            return True
    def improper_interval(n,a,b):
        if n <= a and n >= b:
            return True
    
    if proper_interval(n,a,b) or improper_interval(n,a,b): 
        return True 

def  bisection(desired_output, f, x0, x1, tolerance):
	if x0 > x1: 
		raise  ValueError("Interval is out of order")
	if  not is_inside_interval(desired_output,f(x0),f(x1)): 
		raise  ValueError("Interval doesn't contain a solution or has multiple roots")

#core loop
while  abs(x0-x1)>tolerance: 
	xmid = (x0+x1)/2
	if is_inside_interval(desired_output,f(x0),f(xmid)): #go left
		x1 = xmid #left bound becomes the midpoint
	else:
		x0 = xmid
	return xmid
```

### Results of Bisection Methood
#### Calling the Bisection Method
```
#can call a linear function
bisection(0,lambda x: x , -1, 1, 0.01)
#doesn't contain a solution 
bisection(0, lambda x: x**2-2, 10, 12, 0.0001) 
bisection(1/2, math.sin, 0.1, 0.2, 0.0001)
#raise out of order interval
bisection(1/2, lambda x: x**2, 3, -1, 0.0001)
```
#### Output
```
  File "/data/users/dolnyaj9975/my_ds150/lesson3b/assignment3b.py", line 155, in <module>
    bisection(0, lambda x: x**2-2, 10, 12, 0.0001) 
  File "/data/users/dolnyaj9975/my_ds150/lesson3b/assignment3b.py", line 139, in bisection
    raise ValueError("Interval doesn't contain a solution or has multiple roots")
ValueError: Interval doesn't contain a solution or has multiple roots
```
