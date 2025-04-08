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
`%` is taking the mod of two numbers.

## Question 11 - First Unique Character Finder
```python
string = input()
found = False
frequency = {}

for c in string:
    if c in frequency.keys():
        frequency[c] += 1
    else:
        frequency[c] = 1

for k in frequency.keys():
    if (frequency[k] == 1):
        print(k)
        found = True
        break
if (not found):
    print("Every character in the string appears at least twice.")
```

## Question 12 - Base Convertor
```python
ori_number = input()
ori_base = int(input())
tar_base = int(input())


has_output = False

let_to_num = {
    "1": 1, "2": 2, "3": 3, "4": 4,
    "5": 5, "6": 6, "7": 7, "8": 8,
    "9": 9, "A": 10, "B": 11, "C": 12,
    "D": 13, "E": 14, "F": 15, "0": 0}

# No need for a dictionary since its index corresponds directly to the string
num_to_let = ["0", "1", "2", "3", "4", "5", "6", "7", "8",
             "9", "A", "B", "C", "D", "E", "F"]


# Convert to decimal
degree = 0
dec_number = 0
for i in range(len(ori_number)):
    char = ori_number[-(i+1)] # get char from right to left
    dec_number += let_to_num[char] * (ori_base ** degree)
    degree += 1

if (tar_base == 10):
    print(dec_number)
    has_output = True

# Convert to target base
tar_number = ""
while dec_number > 0:
    remainder = dec_number % tar_base
    tar_number = num_to_let[remainder] + tar_number
    dec_number //= tar_base # Floor division
    
if (not has_output):
    print(tar_number)
```
`dec_number //= tar_base` means `dec_number = int(dec_number / tar_base)`.

## Question 13 - Roman Numerals
```python
value = input()
is_number_to_roman_numeral = value.isnumeric()

# This is a hard question if you do not find the method
# The translation from numbers to roman numerals can actually be done digit by digit
# 
# For instances,
#   M | CCC | XC | VIII => 1000 + 300 + 90 + 8 = 1398
#   1494 => 1000 + 400 + 90 + 4 => M | CD | XC | IV => MCDXCIV
# More over, every digit follows the same pattern.
# If X represents the ones, Y represents the fives, and Z represents the tens in the digit,
# Then, 1 is X, 2 is XX, 3 is XXX, 4 is XY, 5 is Y, 6 is YX, 7 is YXX, 8 is YXXX, 9 is XZ, and we skip 0
# 
# Let's replace X, Y, Z by 0, 1, 2. We get the following list
# If we call reference_table[4], we get "01" => and we can translate this to XY
# This give us a convenient way to turn a digit to the right pattern.
# All we need to do is replace the pattern by the right letters.
reference_list = ["", "0", "00", "000", "01", "1", "10", "100", "1000", "02"]

# Since the maximum number is 2000, we only need to deal with unit, 10th and 100th place
letter_for_digits = [
    ["M", "_", "_"], # 1000th
    ["C", "D", "M"], # 100th
    ["X", "L", "C"], # 10th
    ["I", "V", "X"] # unit
]

val = {"M": 1000, "D": 500, "C": 100, "L": 50, "X": 10, "V": 5, "I": 1}

result = ""
if (is_number_to_roman_numeral):
    for i in range(0, len(value)):
        pattern = reference_list[int(value[i])] # get patterns, like "01"
        for index in pattern: # convert pattern to a string
            # based on the lenth of value, get the right list
            # if len(value) is 4, we want from 0 (4 - 4) to 3 (i = 0, 1, 2, 3)
            # if len(value) is 3, we want from 1 (4 - 3) to 3 (i = 0, 1, 2)
            # if len(value) is 2, we want from 2 (4 - 2) to 3 (i = 0, 1)
            # ...
            # the pattern is (4 - len(value)) + i
            right_list = letter_for_digits[(4-len(value)) + i]
            result += right_list[int(index)] # from list get the right letters
            
else: # Roman numeral to numbers
    # read from right to left
    # if a the next number is smaller than the current number, make the next number negative
    result = 0 # redefine result as number
    current_digit = 0
    for char in value[::-1]:
        if (current_digit <= val[char]):
            current_digit = val[char]
            result += current_digit
        else:
            result -= val[char]

print(result)
```
