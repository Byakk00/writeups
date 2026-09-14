# Files

We learn how to open data files on your computer and read through the files using Python.

## References

- https://www.py4e.com/lessons/files (Slides and Videos)
- https://www.py4e.com/html3/07-files (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 7.2

Write a program that prompts for a file name, then opens that file and reads through the file, looking for lines of the form:
  
```
X-DSPAM-Confidence:    0.8475
```
  
Count these lines and extract the floating point values from each of the lines and compute the average of those values and produce an output as shown below. Do not use the sum() function or a variable named sum in your solution.
You can download the sample data at http://www.py4e.com/code3/mbox-short.txt when you are testing below enter mbox-short.txt as the file name.
  
Desired Output:

Average spam confidence: 0.7507185185185187

```py
# Use the file name mbox-short.txt as the file name
fname = input("Enter file name: ")
fh = open(fname)
for line in fh:
    if not line.startswith("X-DSPAM-Confidence:"):
        continue
    print(line)
print("Done")
```

## Solution

### Exercise 7.2

```py
text = "X-DSPAM-Confidence:    0.8475"
pos = text.find(":")
text = text[pos+1:]
text = text.strip()
print(float(text))
```

Output:

Average spam confidence: 0.7507185185185187

Updated the code to get the desired output.

## Learning

Learnt about files and operations on it.
