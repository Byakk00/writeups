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
name = input("Enter file:")
if len(name) < 1:
    name = "mbox-short.txt"
handle = open(name)

counts = dict()

for line in handle:
    if not line.startswith('From '):
        continue
    words = line.split()
    email = words[1]
    counts[email] = counts.get(email, 0) + 1

bigcount = None
bigword = None

for word, count in counts.items():
    if bigcount is None or count > bigcount:
        bigword = word
        bigcount = count

print(bigword, bigcount)
```

Output:

cwen@iupui.edu 5

Updated the code to add lines for things asked in question to get the desired output.

## Learning

Learnt about dictionaries.
