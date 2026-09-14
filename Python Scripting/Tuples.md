# Tuples

The tuple is a Python data structure that is like a simple and efficient list.

## References

- https://www.py4e.com/lessons/tuples (Slides and Videos)
- https://www.py4e.com/html3/10-tuples (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 10.2

Write a program to read through the mbox-short.txt and figure out the distribution by hour of the day for each of the messages. You can pull the hour out from the 'From ' line by finding the time and then splitting the string a second time using a colon.
```
From stephen.marquard@uct.ac.za Sat Jan  5 09:14:16 2008
```
Once you have accumulated the counts for each hour, print out the counts, sorted by hour as shown below.

Desired Output:

```
04 3
06 1
07 1
09 2
10 3
11 6
14 1
15 2
16 4
17 2
18 1
19 1
```

```py
name = input("Enter file:")
if len(name) < 1:
    name = "mbox-short.txt"
handle = open(name)
```

## Solution

### Exercise 10.2

```py
name = input("Enter file:")
if len(name) < 1:
    name = "mbox-short.txt"
handle = open(name)

counts = dict()
for line in handle:
    if not line.startswith("From "):
        continue
    words = line.split()
    time = words[5]
    hour = time.split(":")[0]
    counts[hour] = counts.get(hour, 0) + 1

for hour, count in sorted(counts.items()):
    print(hour, count)
```

Output:

```
04 3
06 1
07 1
09 2
10 3
11 6
14 1
15 2
16 4
17 2
18 1
19 1
```

Updated the code to add lines for things asked in question to get the desired output.

## Learning

Learnt about tuples.
