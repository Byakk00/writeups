# Loops and Iterations

We look at how Python repeats statements using looping structures.

## References

- https://www.py4e.com/lessons/loops (Slides and Videos)
- https://www.py4e.com/html3/05-iterations (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 5.2

Write a program that repeatedly prompts a user for integer numbers until the user enters 'done'. Once 'done' is entered, print out the largest and smallest of the numbers. If the user enters anything other than a valid number catch it with a try/except and put out an appropriate message and ignore the number. Enter 7, 2, bob, 10, and 4 and match the output below.

Desired Output:

Invalid input
Maximum is 10
Minimum is 2

```py
largest = None
smallest = None
while True:
    num = input("Enter a number: ")
    if num == "done":
        break
    print(num)

print("Maximum", largest)
```

## Solution

### Exercise 5.2

```py
def computepay(h, r):
    if h<=40:
        return h*r
    else:
        return (r*40)+((h-40)*r*1.5)

hrs = input("Enter Hours:")
h = float(hrs)
rph = input("Enter Rate")
r = float(rph)
p = computepay(h, r)
print("Pay", p)
```

Output: Pay 498.75

Updated the code to properly input rate per hour and hours, and take dynamic variables for computepay rather than hardcoded values, and declare computepay function to calculate pay as per the logic given to get the desired output.

## Learning

Learnt about functions, arguments, parameters, void, and some examples of in-built functions like type conversion and max functions.
