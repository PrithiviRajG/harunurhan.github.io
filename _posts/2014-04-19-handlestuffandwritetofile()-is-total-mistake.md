---
layout: post
title: handlestuffandwritetofile() is a total mistake, and more...
---
Everyone can write code which works and do what it is supposed to do.
Every programmer creates routines(functions or methods or procedures) to reduce complexity, improve
performance, readability and importantly to avoid duplicate code. Every programmer accepts
that this is is the greatest invention in computer science. However not all know how to design.

## Only one purpose

Routines should have only one purpose, If a routine does more than one thing then it is better split it into individual routines.

## Naming them

The most significant and main point is **routine's name must describe what it does clearly**.
-  Strong verbs should be used, AVOID names like `handleInput()`, `dealwithOutput()`, `performSalaryCalcuation()`
instead of these, use `getInput()`, `printfOutput()`, `calculateSalary()`
- Names can be as long as necessary, If long one is more clear, then do not hesitate to use it.
- Name to express return value/type: `isFull()`, `currentColor()`, `sine()`
- Combine strong verbs with an object: (if you aren't using an object oriented language); use `checkUserInfo()`, `openFile()` instead of `check()`, `open()`.
- Decide and use one way for common operations. `Class1.getId()`, `Class1.id()`, `Class1.Property.id()` all are OK, but you decide one of them and go with it in order retrieve id of any class that
you design because some time later, you may not remember how to retrieve id of an object.

## Parameters

- Use all of parameters (if you work with function pointers (in C,C++), it is OK not to use all of them.
- Don't use parameters as working variables,

~~~~
int sample(int inputValue)
{
    inputValue = inputValue * 2;
    inputValue = inputValue + anotherFunction(inputValue);
    return inputValue;
}
~~~~

By doing this, you change inputValue and you can never get its first value later. In addition imagine you pass params by reference, it would probably be a problem to change them. Also `return inputValue` doesn't look proper and legit.
Use below

~~~~
int sample(int inputValue)
{
    int localValue = inputValue;
    localValue = localValue * 2;
    localValue = localValue + anotherFunction(localValue);
    return localValue;
}
~~~~

- Consider using prefix (or suffix) keywords so as to distinguish between input,modify and out params.
`sample(in_param1, in_param2, param3, out_param4)`
in for input, out for output, none for modify. You can do it on your way.
- Use same param order, If some of your routines has same params.

I learned most of I wrote by reading Steve McConnell's Code Complete and I strongly recommend it.
