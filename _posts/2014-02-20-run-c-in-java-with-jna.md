---
layout: post
title: Running C in Java with JNA
---
It is very easy to run your native library in Java by using JNA(Java Native Access). Some terminal commands then it is done.

I will show you how to print `pointer` which java doesn't have.
Do all these, in the same folder.

## Source
First we need to write c code that prints pointer of given integer.
Create a file named `CSource.c`

~~~~
#include <stdio.h>
void printPointOf(int n) {
    printf("%p\n"&n);
}
~~~~

`gcc -o libcsourc.dylib -shared cSource.c` (if your os is Windows change .dylib to .dll)

## Java

Before do anything, download jna library from [github](https://github.com/twall/jna), copy **src/com** folder to your workdir (folder that contains library and files you just created). Also copy **dist/jna.jar** to your workdir.

Then create a file named `Example.java`

~~~~
import com.sun.jna.Library;
import com.sun.jna.Native;

public class Example {
    public interface CSource extends Library {
        public void printPointOf(int n);
    }
    static public void main(String argv[]) {
        CSource cSrc = (CSource) Native.loadLibrary("csource", CSource.class);
        int n = 1;
        cSrc.printPointOf(n);
    }
}
~~~~

## Compile and Run

to compline your java file

`javac -classpath jna.jar Example.java` this produces .class file.

to run your class file

`java -classpath jna.jar:. Example`
