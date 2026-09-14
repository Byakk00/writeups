# Strings

We look at how Python stores and manipulates textual data using string variables and functions.

## References

- https://www.py4e.com/lessons/strings (Slides and Videos)
- https://www.py4e.com/html3/06-strings (Theory)

## Notes

Just using reference material for this module especially the slide.

## Autograder:

### Exercise 6.5

Write code using find() and string slicing (see section 6.10) to extract the number at the end of the line below. Convert the extracted value to a floating point number and print it out.

Desired Output:

0.8475

```py
text = "X-DSPAM-Confidence:    0.8475"
```

## Solution

### Exercise 6.5

```py
text = "X-DSPAM-Confidence:    0.8475"
pos = text.find(":")
text = text[pos+1:]
text = text.strip()
print(float(text))
```

Output:

0.8475

Updated the code to get the desired output.

## Learning

Learnt about strings, slicing, indexing and other functions on strings.
