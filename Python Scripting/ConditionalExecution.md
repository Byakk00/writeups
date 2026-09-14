# Conditional Execution

We look at how Python executes some statements and skips others.

## References

- https://www.py4e.com/lessons/logic (Slides and Videos)
- https://www.py4e.com/html3/03-conditional (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 3.1 

Write a program to prompt the user for hours and rate per hour using input to compute gross pay. Pay the hourly rate for the hours up to 40 and 1.5 times the hourly rate for all hours worked above 40 hours. Use 45 hours and a rate of 10.50 per hour to test the program (the pay should be 498.75). You should use input to read a string and float() to convert the string to a number. Do not worry about error checking the user input - assume the user types numbers properly. Output: 498.75

```py
hrs = input("Enter Hours:")
h = float(hrs)
```

### Exercise 3.3

Write a program to prompt for a score between 0.0 and 1.0. If the score is out of range, print an error. If the score is between 0.0 and 1.0, print a grade using the following table:

Score Grade
- `>= 0.9 A`
- `>= 0.8 B`
- `>= 0.7 C`
- `>= 0.6 D`
- `< 0.6 F`

If the user enters a value out of range, print a suitable error message and exit. For the test, enter a score of 0.85. Output: B

```py
score = input("Enter Score: ")
```

## Solution

### Exercise 3.1

```py
hrs = input("Enter Hours:")
h = float(hrs)
rph = input("Enter rate per hour:")
r = float(rph)
if (h<=40):
    print(r*h)
elif (h>40):
    print((r*40)+(1.5*r*(h-40)))
```

Output: 498.75

Updated the code with conditionals and input rate per hour to get the desired output.

### Exercise 3.3

```py
score = float(input("Enter Score: "))
if (score>1 or score<0):
    print("Error")
elif (score>= 0.9):
    print('A')
elif (score>= 0.8):
    print('B')
elif (score>= 0.7):
    print('C')
elif (score>= 0.6):
    print('D')
else:
    print('F')
```

Output: B

Updated the code with multiple conditions, error handling for out of range and float conversion of input to get the desired output.

## Learning

Learnt about conditionals, indentation, comparison operators, different ways to use conditionals, try/except method etc.
