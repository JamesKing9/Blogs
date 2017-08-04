# About the Authors

**Neil Matthew** 

**Rick Stones**

---



# Chapter 2: Shell Programming

Having started this book on programming Linux using C, we now take a detour into writing shell programs. *Why?* Well, Linux isn't like systems where the command-line interface is an afterthought to the graphical interface.



# Chapter 7:  Data Management

In earlier chapters, we touched on the subject of resource limits. In this chapter, we're going to look first at ways of managing your resource allocation, then at ways of dealing with files that are accessed by many users more or less simultaneously, and lastly at one tool provided in Linux systems for overcoming the limitations of flat files as a storage medium.

We can summarize these topics as three ways of managing data:

*   **Dynamic memory management**: what to do and what *Linux* won't let you do
*   **File locking**: cooperative locking, locking regions of shared files, and avoiding deadlocks
*   **The dbm database**: a basic, non-SQL-based database library featured in most Linux systems



## 7.1  Managing Memory





### 7.1.1  Simple Memory Allocation

You allocate memory using the `malloc` call in the standard C library:

```c
#include <stdlib.h>
void *malloc(size_t size);
```



#### Try It Out:  "Simple Memory Allocation"

Type the following program, `memory1.c`:

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

#define A_MEGABYTE (1024 * 1024)

int main() {
	char *some_memory;
}
```

  

