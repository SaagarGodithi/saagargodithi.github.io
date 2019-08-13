---
layout: post
title: Documenting is the new procrastination
---

# Primitive Types 
> Today I will document relearning primitive types and my attempt to solve the first problem in EPI. I really don't want to do this. But I have to, so I might as well write about it to make the process take a lot longer than it should. 


```python
def count_bits(x):
    num_bits = 0
    while x: 
        # if last bit is 1 increment
        num_bits += x & 1 
        # shift right
        x >>= 1
    return num_bits
```


```python
count_bits(11) # 1011 
```




    3



**Built-in types**: numerics, sequences, mappings, classes, instances and exceptions
    

### Bitwise Operations


```python
6&4 # 110&100
```




    4




```python
8>>1 #1000>1
```




    4




```python
-16>>2 # 110000>>2 = 111100
```




    -4




```python
1<<10 
```




    1024




```python
~0 # ~0000 = 1111
```




    -1




```python
15^5 # 1111 ^ 0101 = 1010 
```




    10



**Crucial**: bitwise operations, masks, clear lowermost set bit, signedness, shifting


```python
# Setting a bit with a bit mask
def set_bit(position, binary):
    # create mask
    bit_mask = 1<<position
    # OR'd 
    return binary | bit_mask 
```


```python
# make 1010 to 1110
set_bit(2, 0b1010)
```




    14



**Functions to remember**: `abs(x)`, `math.ceil(x)`, `math.floor(x)`, `min(x,y)`, `max(x,y)`, `pow(x,2)`, `math.sqrt(x)`

**Convert string to float/int and vice versa**: `str(43)`, `int('42')`, `float('3.14')`

**Random**: `random.randint(1,4)`, `random.random()`, `random.shuffle(A)`, `random.choice(A)`

#### 4.1 Computing the parity of a word
> The parity of a binary word is 1 if the number of 1s in the word is odd; otherwise, it is 0. For example, the parity of 1011 is 1, and the parity of 10001000 is 0. Parity checks are used to detect single bit errors in data storage and communication. It is fairly straightforward to write code that computes the parity of a single 64-bit word.
> How would you compute the parity of a very large number of 64-bit words?


```python
# My Brute Force Solution
# Count bits and check if bit number is odd

def parity(x):
    num_bits = 0
    while x:
        num_bits += x & 1
        x >>= 1
    return num_bits % 2
```


```python
# checks 
parity(0b01011)
```




    1



*How do we optimize this solution?*
 **Hint**: Use a look-up table... how *TF* am I supposed to cache 2**64 words


<p class="message"> At this point I am completely bamboozled so I take a peek at the solution. This is my first problem so I don't feel too bad about it. </p>


```python
# EPI's brute force solution
def parity(x):
    result = 0
    while x:
        result ^= x & 1
        x >>= 1
    return result 
```

###### Tracing this solution
Let's choose `x = 1111`

_<u>loop 1:</u>_

`result= 0000 ^ 0001` therefore `result = 0001`

`x = 0111`

_<u>loop 2:</u>_

`result= 0001 ^ 0001` therefore `result = 0000`.

`x = 0011`

... **result tracks mod 2 of count!**


The complexity of both our algorithms is *O(n)*. Let's follow EPI to see how they bring that down. 

##### First Improvement: Drop the lowest set bit trick!
###### Memorize: `x&(x-1) equals x with lowest set bit erased` AND `x&~(x-1) isolates lowest bit`
 

Drop the lowest set bit to improve our best case performance. 
For example let's drop `0b01011000` to `0b01010000`: 


```python
x = 0b01011000
```


```python
bin(x-1)
```




    '0b1010111'




```python
bin(x&(x-1))
```




    '0b1010000'



We can write a *O(k)* solution now where k is number of set bits.


```python
# Optimizing my solution using lowest set bit trick
def parity(x):
    num_bits = 0
    while x:
        x &= x - 1
        num_bits += 1
    return num_bits % 2 
```


```python
# checks 
parity(0b01011)
```




    1




```python
# Using both mod 2 and lowest set bit trick
def parity(x):
    result = 0
    while x:
        result ^= 1 # goes to 0 every other time
        x &= x - 1
    return result 
```


```python
# checks 
parity(0b01011)
```




    1



##### Second Improvement: Cache!

For big improvements, we need to **cache**! We can compute the parity of 16 bit non-overlapping subgroups and easily cache its results. *64-bit word = 4 non-overlapping 16 bit words!*


```python
def maskgen(bits):
    x = 0
    for i in range(bits):
        x <<= 1
        x += 1
    return x
```


```python
parity_cache = {}

parity_cache[0] = 0
parity_cache[1] = 1

mask_1bit = maskgen(1)
mask_2bit = maskgen(2)
mask_4bit = maskgen(4)
mask_8bit = maskgen(8)
mask_16bit = maskgen(16)

for i in range(mask_1bit+1, mask_2bit+1):
    parity_cache[i] = parity_cache[((i >> 1)&mask_1bit)] ^ parity_cache[(i&mask_1bit)]
    
for i in range(mask_2bit+1, mask_4bit+1):
    parity_cache[i] = parity_cache[((i >> 2)&mask_2bit)] ^ parity_cache[(i&mask_2bit)]

for i in range(mask_4bit+1, mask_8bit+1):
    parity_cache[i] = parity_cache[((i >> 4)&mask_4bit)] ^ parity_cache[(i&mask_4bit)]

for i in range(mask_8bit+1, mask_16bit+1):
    parity_cache[i] = parity_cache[((i >> 8)&mask_8bit)] ^ parity_cache[(i&mask_8bit)]

```


```python
def parity(x):
    return parity_cache[((x>>(3 * 16))&mask_16bit)]^parity_cache[((x>>(2 * 16))&mask_16bit)]^parity_cache[((x>>(1 * 16))&mask_16bit)]^parity_cache[(x&mask_16bit)]
```


```python
# check
parity(0b101001010100100100101001010100101001011)
```




    1



What is the complexity? If N is the size of the word and L is the size of the smaller portion we look up, we have an *O(N/L)* algorithm. 

##### Third Improvement: XOR is cray cray

**Fun Fact**: the XOR of a group of bits is its parity.

We can exploit this:

Let's calculate the parity of a 4-bit word using this.

For a word `b1 b2 b3 b4` we want `b1^b2^b3^b4`.

let `x = b1 b2 b3 b4`

`x ^= x >> 2` is the same as `x = b1 b2 b3 b4 ^ 0 0 b1 b2` which makes `x = b1 b2 b1^b3 b2^b4`.

`x ^= x >> 1` is the same as `x = b1 b2 b1^b3 b2^b4 ^ 0 b1 b2 b1^b3` which makes `x = b1 b1^b2 b1^b2^b3 b1^b2^b3^b4`.

Therefore the parity of the 4-bit word is the last bit of `x` or `x&1`


```python
def parity(x):
    x ^= x >> 32
    x ^= x >> 16
    x ^= x >> 8
    x ^= x >> 4
    x ^= x >> 2
    x ^= x >> 1
    return x&1
```


```python
# check
parity(0b101001010100100100101001010100101001011)
```




    1



New better time complexity is *O(log N)*!

That was so much work for nothing....
