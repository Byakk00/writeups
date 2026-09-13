# Conditional Execution

Take a brief look at how Python implements the 'store and use later' programming pattern.

## References

- https://www.py4e.com/lessons/functions (Slides and Videos)
- https://www.py4e.com/html3/04-functions (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 4.6

Write a program to prompt the user for hours and rate per hour using input to compute gross pay. Pay should be the normal rate for hours up to 40 and time-and-a-half for the hourly rate for all hours worked above 40 hours. Put the logic to do the computation of pay in a function called computepay() and use the function to do the computation. The function should return a value. Use 45 hours and a rate of 10.50 per hour to test the program (the pay should be 498.75). You should use input to read a string and float() to convert the string to a number. Do not worry about error checking the user input unless you want to - you can assume the user types numbers properly. Do not name your variable sum or use the sum() function. 

Output: Pay 498.75

```py
def computepay(h, r):
    return 42.37

hrs = input("Enter Hours:")
p = computepay(10, 20)
print("Pay", p)
```

## Solution

### Exercise 4.6

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
