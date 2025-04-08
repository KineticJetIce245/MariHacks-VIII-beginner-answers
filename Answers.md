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
Ascii Code is how computers store letters. Learn more about it on 
[Wikipedia](https://en.wikipedia.org/wiki/ASCII) 
and [Ascii Code Table](https://www.ascii-code.com). In Python, we can use `ord` to get
Ascii Code of a letter and `chr` to get a letter from the Ascii Code.

## Question 7 - Is this a Prime Number?
```python
import math
n = int(input())
is_prime = True

for i in range(2, int(math.sqrt(n)) + 1):
    if (i != 2 and i % 2 == 0):
        continue
    if (n % i == 0):
        print("false")
        is_prime = False
        break

if (is_prime):
    print("true")
```

## Question 8 - Balanced Parentheses Checker
```python
brackets = input()
stack = []
is_wrong = False

# Returns True if char is an opened bracket
# Returns False if char is not an opened bracket
def checkBracketType(char: str): 
    return ((char == "{") or (char == "[") or (char == "("))

# Returns if two bracket match, order matters
def checkBracketMatch(char1: str, char2: str):
    if (char1 == "{"): return char2 == "}"
    if (char1 == "["): return char2 == "]"
    if (char1 == "("): return char2 == ")"

for char in brackets:
    if (checkBracketType(char)):
        stack.append(char)
    else:
        if (len(stack) == 0):
            print("false")
            is_wrong = True
            break
        poped_bracket = stack.pop()
        if not checkBracketMatch(poped_bracket, char):
            print("false")
            is_wrong = True
            break

        
if (not is_wrong):
    if (len(stack) == 0):
        print("true")
    else:
        print("false")
```
To solve this question, we have to introduce the notion of stack (yes, that is
where *StackOverflow*'s name comes from). It is a data structure like a 
bucket. You can put element only on the top of the stack (**push**) and you can only 
retrieve element at the top of the stack (**pop**). 

In python you can simulate a stack using a list, for instance:
```python
stack = []
stack.append("a") # now "a" is pushed and it is on the top of the stack
stack.append("b") # now "b" is pushed and it is on the top of the stack
x = stack.pop() # now "b" is popped and the value "b" is removed from stack and is given to x
# a is on the top of the stack
```

## Question 9 - Frequency Counter and Mode Finder
```python
arr = input().split(", ")
arr = [int(c) for c in arr]
arr = sorted(arr)
map = {}

for n in arr:
    if n in map.keys():
        map[n] += 1
    else:
        map[n] = 1

max_keys = []
max = 0

for n in map.keys():
    if map[n] > max:
        max = map[n]
        max_keys = [n]
    elif map[n] == max:
        max_keys.append(n)
    else:
        continue

print(str(map)[1:-1])
print(str(sorted(max_keys))[1:-1])
```

## Question 10 - Array Rotation
```python
arr = input().split(", ")
arr = [int(c) for c in arr]
shift = int(input())

result = []

shift = shift % len(arr)

if (shift > 0):
    for i in range(shift):
        result.append(arr[-shift + i])
    index = 0
    while len(result) < len(arr):
        result.append(arr[index])
        index += 1
elif (shift < 0):
    for i in range(-shift, len(arr)):
        result.append(arr[i])
    index = 0
    while len(result) < len(arr):
        result.append(arr[index])
        index += 1
else:
    result = arr

print(str(result)[1:-1])
```
