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
For a string `a`, `a.lower()` turns every letter in `a` to lower case

## Question 5 - Second Largest Number
```python
arr = input().split(", ")
arr = [int(c) for c in arr]
arr = sorted(arr)
found = False

max = arr[-1] 

for n in range(2, len(arr) + 1):
    if arr[-n] != max:
        found = True
        print(arr[-n])
        break

if (not found):
    print("The second largest number does not exist in this array.")
```
`split(", ")` splits a string to an array using `", "`, for example,
`"1, 2 ,4, 5"` becomes an array like this: `["1", "2", "3", "4"]`.
However this is not enough, we have to make the elements in that array
into integers. In python, if you want to make some change to every
element in an array and make a new array, you can use this notation 
`[some action on e for e in arr]`

For instance,
```python
arr = [1, 3, 4, 5, 1]
arr2 = [i - 1 for i in arr]
print(arr2)
```
gives you
```
[0, 2, 3, 4, 0]
```

## Question 6 - Caesar Cipher Encoder
```python
message = input()
shift = int(input())

encrypted_message = ""
# A - Z ascii codes are 65 to 90
# a - z ascii codes are 97 to 122

for char in message:
    ascii_code = ord(char)
    if (65 <= ascii_code) and (ascii_code <= 90): # A - Z
        ascii_code -= 65 # A is now 0
        ascii_code = (ascii_code + shift) % 26 # goes back between [0, 25] if is more than 26
        ascii_code += 65 # put it back to the right start 65
        encrypted_message += chr(ascii_code)
    elif (97 <= ascii_code) and (ascii_code <= 122): # a - z
        ascii_code -= 97 # A is now 0
        ascii_code = (ascii_code + shift) % 26 # goes back between [0, 25] if is more than 26
        ascii_code += 97 # put it back to the right start 97
        encrypted_message += chr(ascii_code)
    else: # not letters, ignore
        encrypted_message += char
        continue
        
print(encrypted_message)
```
