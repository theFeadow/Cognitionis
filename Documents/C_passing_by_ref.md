---
id: D#g9okk2
date: 01/10/2022
type: node
status: digital
aliases: [D#g9okk2]
tags:
  - C
---
# Passing by Reference in C

C always passes 'by value'. However, it is possible to simulate passing 'by reference' by passing a pointer as an argument.

> << What is passed in is a copy of the pointer, but what it points to is still the same address in memory as the original pointer, so this allows the function to change the value outside the function. >> [^1]

We could use 'dereferenced pointers', which is essentially the same thing as working with the value itself. [^2]

```C
void swap(int *a, int *b)

{

	*a = *a + *b;
	*b = *a - *b;
	*a = *a - *b;
	
	return;

}
```

---

#### Bibliography

[^1]: from [prs]
[^2]: code idea from [prs]

[prs]: [dev.to](https://dev.to/mikkel250/passing-by-value-passing-by-reference-in-c-1acg)