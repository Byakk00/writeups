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
largest = None
smallest = None

while True:
    num = input("Enter a number: ")
    if num == "done":
        break
    try:
        num = int(num)
    except:
        print("Invalid input")
        continue
    if largest is None and smallest is None:
        largest = num
        smallest = num
    else:
        if num > largest:
            largest = num
        if num < smallest:
            smallest = num

print("Maximum is", largest)
print("Minimum is", smallest)
```

Output:

Invalid input

Maximum is 10

Minimum is 2

Updated the code with try, except and proper conditionals to get the desired output.

## Learning

Learnt about loops, None, break and continue.
