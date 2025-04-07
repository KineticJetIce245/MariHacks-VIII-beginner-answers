# Answers to the First 20 Questions in the Beginner Section

## Question 1 - Sum It Up!
```python
a = input()
b = input()
a = int(a) # now a is an integer
b = int(b) # now b is an integer
print(a + b)
```
One can condense the code by doing
```python
a = int(input())
b = int(input())
print(a + b)
```

## Question 2 - Reverse a String
```python
string = input()
print(string[::-1])
```
In python, one can access the elments in a list
using the slice notation `[start:end:jump]`. This
means getting elements from `start` (included) 
to `end` (not included) and skip `jump - 1` elements 
after each element.

For example
```python
a = [0, 1, 2, 3, 4, 5, 6, 7]
print(a[1:4])
print(a[:7])
print(a[::2])
print(a[::-1])
```
gives
```
[1 ,2, 3]
[0, 1, 2, 3, 4, 5, 6]
[0, 2, 4, 6]
[7, 6, 5, 4, 3, 2, 1, 0]
```

## Question 3 - Factorial Calculator
```python
n = int(input())
product = 1
for i in range(n):
    # from 0 to n - 1, thus, we have to add 1
    product *= (i+1)

print(product)
```
`product *= (i+1)` is a condense way to write `product = product * (i+1)`

## Question 4 - Palindrome Checker
```python
a = input().lower()
if (a == a[::-1]):
    print("true")
else:
    print("false")
```
For a string `a`, `a.lower()` turns every letter in `a` to lower case.
