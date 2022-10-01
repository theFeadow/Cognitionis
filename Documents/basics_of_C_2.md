---
id: D#a4tns7gj
date: 08/09/2022
type: article
aliases: [D#a4tns7gj]
tags:
  - C
---

..this document is part of a serial document set, see previous: [[basics_of_C_1|D#my5gb3ed]]

# Basics of the C Language and its Compiler - part 2


#### Compilers

Previously, the `make` command was introduced as a way to compile a C-program:

```bash
~$ make hello
```

However, `make` itself is not a compiler - it is a program that calls the actual compiler `clang`. The compiler `clang` provides various options for compilation and makes use of command-line arguments. By default, `clang` outputs a file called `a.out` that is the compiled version of the C-program. One can change the name of the output file by using command-line arguments. When using libraries (header files), one must be wary when compiling with `clang` as one needs to use the `-l` flag to link to the library files.

```bash
~$ clang -o hello hello.c -lcs50
```

It is thus easier to use `make` instead of `clang`, as `make` abstracts away much of the low-level details involved in the compilation process.



---



#### The Compilation Process

Compiling source code into machine code is actually made up of smaller steps, namely:

- preprocessing
- compiling
- assembling
- linking



##### Preprocessing

Preprocessing generally involves lines that start with a `#` like `#include`. Including a certain header file will tell `clang` to look for that header file, since it contains relevant code and functions that we want to include in our program. `clang` will replace the headers with prototypes of functions from the libraries that were included, so we can then use them in our code.

For example:

```C
#include <cs50.h>
#include <stdio.h>

int main(void)
{
    string name = get_string("What's your name? ");
    printf("hello, %s\n", name);
}
```

will be preprocessed into:

```C
...
string get_string(string prompt);
int printf(string format, ...);
...

int main(void)
{
    string name = get_string("Name: ");
    printf("hello, %s\n", name);
}
```



##### Compiling

Compiling translates **source code** into **assembly code**, which is lower-level and closer to the binary instructions that are ultimately executed directly by the computer's processor. Remember that the assembled code is **machine-dependent**, while the source code itself is not.



##### Assembling

Assembling involves translating the assembly code into binary instructions that are executed directly by the CPU of the machine.



##### Linking

Linking involves combining previously compiled versions of libraries that were included, like `stdio.h`, with the binaries of the actual program we wrote. The output is of the linking process is one binary file - `a.out` - that is the combined machine code for the source code as well as the linked libraries.



---



#### Arrays

In C, you don't get an `array index out of bound` error when you reference an index value larger than the array size, values from memory corresponding to bytes that come after those of the original array will be fetched instead.

Arrays in C are 0-indexed, of course.



One can immediately create a populated array of the suitable size via:

```C
int pi_array[] = {3, 1, 4, 1, 5, 9}
```

.. this will create an array of size 6 and populate it correspondingly. Note that:

```C
pi_array[8]
```

.. will NOT return an error, even though the largest index that really represents the array that was created is `[5]`.

---

Now Let's take a look at a program:

```C
#include <cs50.h>
#include <stdio.h>

const int TOTAL = 3;

int main(void)
{
    int scores[TOTAL];
    for (int i = 0; i < TOTAL; i++)
    {
      scores[i] = get_int("Score: "); // get_int function is in <cs50.h>
    }

    printf("Average: %f\n", average(TOTAL, scores));
}
```



..now we can add a function to calculate the average:

```C
float average(int length, int array[])
{
    int sum = 0;
    for (int i = 0; i < length; i++)
    {
        sum += array[i];
    }
    return sum / (float) length;
}
```



The `(float)` key-word is included to type-cast the variable `length` to float and thus the returned value for the average will be a float and not an int. This prevents values after the decimal point from being truncated.

Note that we need to keep track of the length of the array and pass it as a parameter to the averaging function as there's no inherent way to find the length of an array in C.

Wait.. but what about strings?



---



#### Strings

- There are NO variables of type `string` in C.

- In C, strings are represented as an array of type `char`.

- If a string is represented with an array `s`, the individual characters can be extracted using `s[0]`, `s[1]`, and so on..



However, one can quickly create an array of characters of the suitable size and populate it with the characters of a "string" via:

```C
char greetings[] = "Hello World!";
```

Note that you have to use double quotes.



And since strings in C are nothing but character arrays, we can do the following:

```C
char greetings[] = {'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '!', '\0'};
printf("%s", greetings);
```

Note the `'\0'` at the end.. we'll discuss it shortly.



Now to output a string, one can use the `printf()` function together with the format specifier `%s` to tell C that we are working with an array of characters that represent a string.

```C
char greetings[] = "Hello World!";
printf("%s", greetings);
```



##### The Null Terminating Character (`'\0'`)

Previously, we established that creating an array in C does not give it an "inherent size". We've also established that, by using character arrays, you can manipulate strings and print them out. But, how does the "printer" know when to stop? For example, when we say:

```C
char greetings[] = {'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '!', '\0'};
printf("%s", greetings);
```

..how does the `printf` function know where the string "ends"? At the end of the day, a string is an array and arrays in C have no size!..

This is where the ***"null terminating character"*** comes intro play. The character `'\0'` which has ASCII code "0" is used in C to define the end of a string. Functions that manipulate strings use this character to know where the end of the array is.

For example, the `strlen` function that exists in C's `string` library returns the size of a string. It is sane to believe that the implementation of `strlen` checks for the null character to identify where the string ends.



The code:

```C
#include <stdio.h>
#include <string.h>

int main(void)
{
    chat[] s = "Amygdallion"
    printf("Output: ");
    for (int i = 0; i < strlen(s); i++)
    {
        printf("%c\n", s[i]);
    }
    printf("\n");
}
```

..outputs:

```
A
m
y
g
d
a
l
l
i
o
n
```

---



#### Command-line Arguments

We can also pass "command-line arguments" when running a compiled program from the command-line.

To make the program accept command line arguments, we change the definition of `main`:

```C
int main(int argc, char *argv[])
```

The variable`argc` and the array `argv` will get automatically populated when we run our program from the command-line and include arguments.

- `argc` holds the *argument count* - the number of arguments passed in command-line
- `argc` holds the *argument vector* - the arguments themselves, obviously

I just told a white lie, `argc` doesn't actually hold the argument count, it holds the argument count PLUS ONE.. because it stores the name of the program itself in the first index.. so if only 1 argument is passed, `argc` will be equal to 2.



```C
#include <stdio.h>

int main( int argc, char *argv[] )  {

   if( argc == 2 ) {
      printf("The argument supplied is %s\n", argv[1]);
   }
   else if( argc > 2 ) {
      printf("Too many arguments supplied.\n");
   }
   else {
      printf("One argument expected.\n");
   }
}
```

```bash
$./a.out testing
The argument supplied is testing
```

```bash
$./a.out testing1 testing2
Too many arguments supplied.
```

```bash
$./a.out
One argument expected
```



> << You pass all the command line arguments separated by a space, but if argument itself has a space then you can pass such arguments by putting them inside double quotes "" or single quotes ''. >>



---

[^1]: 
[^2]: 

---

#### Bibliography

test?

[^prs]: [Harvard CS50 Lecture #2 Notes](https://cs50.harvard.edu/x/2021/notes/2/)
[^s1]: [w3schools.com article on C Strings](https://www.w3schools.com/c/c_strings.php)
[^s2]: [tutorialspoint.com article on command-line arguments](https://www.tutorialspoint.com/cprogramming/c_command_line_arguments.htm)