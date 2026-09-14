# Dictionaries

The dictionary data structures allows us to store multiple values in an object and look up the values by their key.

## References

- https://www.py4e.com/lessons/dictionary (Slides and Videos)
- https://www.py4e.com/html3/09-dictionaries (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 9.4

Write a program to read through the mbox-short.txt and figure out who has sent the greatest number of mail messages. The program looks for 'From ' lines and takes the second word of those lines as the person who sent the mail. The program creates a Python dictionary that maps the sender's mail address to a count of the number of times they appear in the file. After the dictionary is produced, the program reads through the dictionary using a maximum loop to find the most prolific committer.

Desired Output:

cwen@iupui.edu 5

```py
name = input("Enter file:")
if len(name) < 1:
    name = "mbox-short.txt"
handle = open(name)
```

## Solution

### Exercise 9.4

```py

```

Output:

cwen@iupui.edu 5

Updated the code with try, except and proper conditionals to get the desired output.

## Learning

Learnt about loops, None, break and continue.
