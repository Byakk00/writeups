# Regular Expressions

Regular Expressions allow us to search for patterns in strings and extract data from strings using the regular expression programming language.

## References

- https://www.py4e.com/lessons/regex (Slides and Videos)
- https://www.py4e.com/html3/11-regex (Theory)
- https://www.py4e.com/lectures3/Pythonlearn-11-Regex-Handout.txt

## Notes

Just using reference material for this module especially the slide.

## Autograder: Regular Expressions

### Finding Numbers in a Haystack

In this assignment you will read through and parse a file with text and numbers. You will extract all the numbers in the file and compute the sum of the numbers.

### Data Files

We provide two files for this assignment. One is a sample file where we give you the sum for your testing and the other is the actual data you need to process for the assignment.

Sample data: http://py4e-data.dr-chuck.net/regex_sum_42.txt (There are 90 values with a sum=445833)
Actual data: http://py4e-data.dr-chuck.net/regex_sum_2465902.txt (There are 96 values and the sum ends with 926)
These links open in a new window. Make sure to save the file into the same folder as you will be writing your Python program. Note: Each student will have a distinct data file for the assignment - so only use your own data file for analysis.

### Handling The Data

The basic outline of this problem is to read the file, look for integers using the re.findall(), looking for a regular expression of '[0-9]+' and then converting the extracted strings to integers and summing up the integers.

## Solution

```py
import re

fname = input("Enter file name: ")
if len(fname) < 1:
    fname = "regex_sum_2465902.txt"
handle = open(fname)
total = 0
for line in handle:
    numbers = re.findall('[0-9]+', line)
    for num in numbers:
        total += int(num)
print(total)
```

Output: 424926

## Learning

Learnt about RegEx.
