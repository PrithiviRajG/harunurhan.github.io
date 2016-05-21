---
layout: post
title: Greatest Common Divisor in ARM Assembly
---
ARM(specifically ARM7) doesn't have a division instruction (UDIV or SDIV), at least I've never seen any.
That's why we do it like the above (higher level understandable code)

~~~~
int divide(int input, int divisor)
{
  int result = 0;
  while(input >= divisor)
  {
    input = input - divisor;
    result++;
  }
  return result;
}
~~~~

Even though this is not a short and simple code for an easy operation, Finding gcd is not really more
difficult than that. I used an approach which includes both iteration and recursion.

~~~~
int gcd(int x,int y){
  while(x!=y)
  {
    if(x>y)
      return gcd(x-y,y);
    else
      return gcd(x,y-x);
  }
  return x;
}
~~~~

That last thing converting this to assembly code which is complicated and not understandable enough.

~~~~
AREA gcdcalc, CODE, READWRITE
       ENTRY
       MOV	R0,#30 ; test values
       MOV R1,#45 ; test values
gcd
while  CMP R0,R1
       BEQ endw
       BGT cond1
       B cond2
cond1  SUB R0,R1
       B gcd
cond2  SUB R1,R0
       B gcd
       B while
endw
stop   B stop
       END
~~~~

That worked for me, I built and debugged this in Keil uVision 4 for ARM7 Little Endian device.

## Version 2
##### More optimized algorithm and assembly code
I've seen a more optimized and fast great common division algorithm, in one of my books. I am also more experienced
in ARM Assembly, so that I could write shorter and better code for the algorithm.

##### GCD in ANSI-C
~~~~
int gcd(int a, int b)
{
  while(a != b)
  {
    if(a>b)
      a = a - b;
    else
      b = b - a;
  }
  return a; // or b because they are equals
}
~~~~

##### GCD in ARM Assembly
~~~~
gcd    CMP R1,R2
SUBGT  SUB R1,R1,R2
SUBLT  SUB R2,R2,R1
BNE    gcd
~~~~
It is even shorter than C code, thanks to instructions with condition.
