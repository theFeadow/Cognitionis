---
id: D#my5gb3ed
date: 06/09/2022
type: article
aliases: [D#my5gb3ed]
tags:
  - C
---

# Basics of the C Language and its Compiler - part 1


#### A simple "Hello, world!" program

```c
#include <stdio.h>

int main(void){
    
    printf("Hello, world!\n");

}
```

> << **Header files** that end with `.h` refer to some other set of code, like a library, that we can then use in our program. We *include* them with lines like `#include <stdio.h>`, for example, for the *standard input/output* library, which contains the `printf` function. >> [^1]



------



#### The `printf` function

The `printf` function allows printing to output with formatting:

```c
#include <stdio.h>

int main(void){

	char[6] name = "Meadow";
	printf("Hello, %s\n", name);

}
```

..there are different placeholders for each type:

- `%c` for chars
- `%f` for floats, doubles
- `%i` for ints
- `%li` for longs
- `%s` for strings



------



#### The `make` command

To compile, one can use the `make` command, which abstracts away a lot of the details involved with compiling the C-code.

The shell command:

```shell
make hello
```

..will automatically look for a file named `hello.c` and will compile it to an executable file named `hello`, which can be executed with `./hello`.



------



#### Header Files

The line..

```C
#include <stdio.h>
```

is an example of using a header file.

> << **Header files** that end with `.h` refer to some other set of code, like a library, that we can then use in our program. We *include* them with lines like `#include <stdio.h>`, for example, for the *standard input/output* library, which contains the `printf` function. >>



---



#### Data Types

The types in C can be classified as follows:

- Basic/Primary Types (eg. `int`,`char`,`long`,`short`)
- Enumerated Types
- The Type `void`
- Derived Types (eg. Pointers, Arrays, Strings, Structures, Functions)

The array and structure types are referred to collectively as 'aggregate types'.



------



#### Basic Integer Types

Each basic integer type has a certain storage size (in bytes) **in memory**, allowing it to be assigned a certain range of values.

|      Type      |            Storage size            |                     Value range                      |
| :------------: | :--------------------------------: | :--------------------------------------------------: |
|      char      |               1 byte               |               -128 to 127 or 0 to 255                |
| unsigned char  |               1 byte               |                       0 to 255                       |
|  signed char   |               1 byte               |                     -128 to 127                      |
|      int       |            2 or 4 bytes            | -32,768 to 32,767 or -2,147,483,648 to 2,147,483,647 |
|  unsigned int  |            2 or 4 bytes            |          0 to 65,535 or 0 to 4,294,967,295           |
|     short      |              2 bytes               |                  -32,768 to 32,767                   |
| unsigned short |              2 bytes               |                     0 to 65,535                      |
|      long      | 8 bytes or (4 bytes for 32 bit OS) |     -9223372036854775808 to 9223372036854775807      |
| unsigned long  |              8 bytes               |              0 to 18446744073709551615               |

The storage size of a basic type may depend on the particular computer architecture used. To obtain the exact size of a type (or variable) on a particular system, one can use the `sizeof` operator.

```C
printf("Size of int data type: %d\n", sizeof(int));
printf("Size of variable x: %d\n", sizeof(x));
```



---



#### Basic Float Types

The same applies for basic float types, whose storage bytes store both a 'mantissa' and an 'exponent'.

|    Type     | Storage size |      Value range       |     Precision     |
| :---------: | :----------: | :--------------------: | :---------------: |
|    float    |    4 byte    |   1.2E-38 to 3.4E+38   | 6 decimal places  |
|   double    |    8 byte    |  2.3E-308 to 1.7E+308  | 15 decimal places |
| long double |   10 byte    | 3.4E-4932 to 1.1E+4932 | 19 decimal places |



---



#### Memory, Imprecision & Overflow

Due to the **finite amount of memory** allocated for each data type, approximation and overflow errors could possibly arise in C programs.



##### Imprecision

Dividing 1 by 10 and storing the output in a float then displaying the contents of the variable to a sufficient number of decimal places shows the presence of **floating-point imprecision**..

```c
#include <stdio.h>

int main(void)
{
    float x = 1
    float y = 10

    printf("%.50f\n", x / y);
}
```

yields:

```
0.10000000149011611938476562500000000000000000000000
```

> << With a finite number of bits for a `float`, we can’t represent all possible real numbers (of which there are an *infinite* number of), so the computer has to store the closest value it can. And this can lead to problems where even small differences in value add up, unless the programmer uses some other way to represent decimal values as accurately as needed. >> [^2]



##### Overflow

**Integer overflow** occurs when an integer's magnitude is too big that the variable holding it runs out of bits to represent it. The carry bit is discarded and therefore information is lost and/or corrupted.



---



#### Prototyping Functions

Here's a C program with a `meow` function that is called `main`. The `meow` function is defined before the `main` function.

```c
#include <stdio.h>

void meow(void) {
  printf("meow\n");
}

int main(void)
{
    for (int i = 0; i < 3; i++)
    {
        meow();
    }
}
```

If we move the definition of the `meow` function to be below the `main` function, there will be a compilation error.

To surpass this error while keeping the definition of `meow` below `main`, we need to add a declaration at the top of the script:

```C
#include <stdio.h>

// Declaring the meow function - a "prototype"
void meow(void);

int main(void)
{
    for (int i = 0; i < 3; i++)
    {
        meow();
    }
}

void meow(void)
{
    printf("meow\n");
}
```

Now the program compiles successfully.



---

[^1]: 
[^2]: 

------

#### Bibliography

[^prs]: [Harvard CS50 Lecture #1 Notes](https://cs50.harvard.edu/x/2021/notes/1/)
[^s1]: [Tutorialspoint.com article on C Data Types](https://www.tutorialspoint.com/cprogramming/c_data_types.htm)

