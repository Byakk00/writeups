# Variables, Expressions and Statements

We learn how to make variables and store data in those variables.

## References

- https://www.py4e.com/lessons/memory (Slides and Videos)
- https://www.py4e.com/html3/02-variables (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 2.2: 

Write a program that uses input to prompt a user for their name and then welcomes them. Note that input will pop up a dialog box. Enter Sarah in the pop-up box when you are prompted so your output will match the desired output. Output: Hello Sarah

```py
# The code below almost works

name = input("Enter your name")
print("Howdy")
```

### Exercise 2.3

Write a program to prompt the user for hours and rate per hour using input to compute gross pay. Use 35 hours and a rate of 2.75 per hour to test the program (the pay should be 96.25). You should use input to read a string and float() to convert the string to a number. Do not worry about error checking or bad user data. Output: Pay: 96.25

```py
# This first line is provided for you

hrs = input("Enter Hours:")
```

## Solution

### Exercise 2.2

```py
name = input("Enter your name")
print("Hello", name)
```

Output: Hello Sarah

Updated print statement to print("Hello", name) to get the desired output.

### Exercise 2.3

```py
hrs = float(input("Enter Hours:"))
rph = float(input("Enter rate per hour: "))
pay = hrs * rph
print("Pay:",pay)
```

Output: Pay: 96.25

Updated hrs (hours) to do float type conversion and added another float input rph (rate per hour). Then used pay variable to calculate pay using hrs * rph and then used a print statement to get the desired output.

## Learning

Learnt variables and constants, how to make a comment, numeric expressions, data types, type conversion, reserved words, good and bad variable names, and input statement.
