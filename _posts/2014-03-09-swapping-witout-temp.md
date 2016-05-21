---
layout: post
category : Algorithms
title: Swapping Without Using A Temp
tagline: XOR
tags : [howto, swapping, xor, exclusiveor, eor, assembly, java]
---
If you have never heard of swapping variable1 to variable2, variable2 to variable1 without using a third variable temporarily, you might find it interesting. When I read about it first, I thought it was impossible but it wasn't.

There is an algorithm which uses XOR operation.


## Background
~~~~
0 XOR 0 >> 0
0 XOR 1 >> 1
1 XOR 0 >> 1
1 XOR 1 >> 0

 A XOR B = B XOR
(A XOR B) XOR C = (A XOR C) XOR B
 A XOR A = 0 and A XOR 0 = A

If your variables has more than one bit, XOR runs for each variable.
~~~~

## Algorithm
- A = A XOR B
- B = A XOR B
- A = A XOR B

## C and java
x and y are integers.

~~~~
x = x ^ y;
y = x ^ y;
x = x ^ y;
~~~~


## Assembly(ARM7)

~~~~
EOR   r1,r0,r1
EOR   r0,r0,r1
EOR   r1,r0,r1
~~~~

## Proof
If we write A' and B' as A and B at the end, by using background info.
- B' = (A XOR B) XOR B = (B XOR B) XOR A = 0 XOR A = A
- A' = (A XOR B) XOR ((A XOR B) XOR B) = (A XOR B) XOR A = (A XOR A) XOR B = 0 XOR B = B
