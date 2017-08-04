



# Beginning Linux Programming, 4th Edition

Cover:

<img src=".\img\cover.jpg" style="height:520px">

## About the Authors

**Neil Matthew** 

**Rick Stones**



---

## Chapter 1: Getting Started



#### 1.2.3  The C Compiler



##### Try It Out:  "Your First Linux C Program"

In this example, you start developing for Linux using C by writing, compiling, and running your first Linux program. It might as well as be that most famous of all starting points, **Hello World**.

Here's the source code for the file `hello.c`:

~~~c
#include <stdio.h>
#include <stdlib.h>

int main() {
	printf("Hello world\n");
	exit(0);
}
~~~

Now compile, link, and run your program:

```mark
$ gcc -o hello hello.c
$./hello
```

It gives the following output:

```mark
Hello World
$
```
**How It Works**





## Chapter 2: Shell Programming

Having started this book on programming Linux using C, we now take a detour into writing shell programs. *Why?* Well, Linux isn't like systems where the command-line interface is an afterthought to the graphical interface.



## Chapter 7:  Data Management 

In earlier chapters, we touched on the subject of resource limits. In this chapter, we're going to look first at ways of managing your resource allocation, then at ways of dealing with files that are accessed by many users more or less simultaneously, and lastly at one tool provided in Linux systems for overcoming the limitations of flat files as a storage medium.

We can summarize these topics as three ways of managing data:

*   **Dynamic memory management**: what to do and what *Linux* won't let you do
*   **File locking**: cooperative locking, locking regions of shared files, and avoiding deadlocks
*   **The dbm database**: a basic, non-SQL-based database library featured in most Linux systems


### 7.1  Managing Memory





#### 7.1.1  Simple Memory Allocation

You allocate memory using the `malloc` call in the standard C library:

```c
#include <stdlib.h>
void *malloc(size_t size);
```



##### Try It Out:  "Simple Memory Allocation"

Type the following program, `memory1.c`:

```c
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>

#define A_MEGABYTE (1024 * 1024)

int main() {
	char *some_memory;
  	int megabyte = A_MEGABYTE;
  	int exit_code = EXIT_FAILURE;
  	
  	some_memory = (char *)malloc(megabyte);
  	if (some_memory != NULL) {
  		sprintf(some_memory, "Hello World\n");
  		printf("%s", some_memory);
  		exit_code = EXIT_SUCCESS;
  	}
  	exit(exit_code);
}
```
Now compile, link, and run your program:

```mark
$ gcc -o memory1 memory.c
$./memory1
```

It gives the following output:

```mark
Hello World
$
```

**How it Works**

>   This program asks the malloc library to give it a pointer to a megabyte of memory. You check to ensure that `malloc` was successful and then use some of the memory to show that it exists. When you run the program, you should see *Hello World* printed out, showing that `malloc` did indeed return the megabyte of useable memory. We don't check that all of the megabyte is present; we have to put some trust in the `malloc` code!



  

