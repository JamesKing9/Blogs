# Glossary

H~2~O

<u>decimal point</u>:  小数点

---



# Chapter 1:  A Tutorial Introduction



## 1.2  Variables and Arithmetic Expressions



Width and  precision may be omitted from a specification: `%6f` says that the number is to be at least six characters wide; `%.2f` specifies two characters after the decimal point,  but width is not constrained; and `%f` merely says to print the number as floating point.

| %d   | print as decimal integer                 |
| ---- | ---------------------------------------- |
| %6d  | print as decimal integer, at least 6 characters |
| %f   | print as floating point                  |
| %6f  | print as floating point, at least 6 characters wide |
|      |                                          |



## 1.3 The "for" statement

There are plenty of different ways to write a program for a particular task. Let's try a variation on the temperature converter.

```c
#include <stdio.h>

/* print Fahrenheit-Celsius table */
main() 
{
	int fahr;
	
	for (fahr = 0; fahr <= 300; fahr = fahr + 20)
		printf("%3d %6.1f\n", fahr, (5.0/9.0)*(fahr-32));
}
```



## 1.4  Symbolic Constants



## 1.5  Character Input and Output





### 1.5.1  File Copying

The simplest example is a program that copies its input to its output one character at a time:

```mark
read a character
	while (character is not end-of-file indicator)
		output the character just read
		read a character
```

Converting this into C gives:

```c
# include <stdio.h>

/* copy input to output; 1st version */
main() {
  int c;
  
  c = getchar();
  while (c != EOF) {
    putchar(c);
    c = getchar();
  }
}
```

The relational operator `!=` means  "not equal to".

The problem is distinguishing【区分】 the end of input from valid data. The solution is that `getchar` returns a distinctive【特殊的，可以区分的】 value when there is no more input, a value that cannot be confused with any real character.

`EOF`  is an integer defined in `<stdio.h>` , but the specific numeric value doesn't matter as long as it is not the same as any `char`  value. By using the symbolic constant, we are assured that nothing in the program depends on the specific numeric value.

### 1.5.2  Character Counting

The next program counts characters; it is similar to the copy program.

```c
# include <stdio.h>

/* count characters in input; 1st version */
main() {
  long nc;
  
  nc = 0;
  while (getchar() != EOF)	
    ++nc;
  printf("%ld\n", nc);
}
```

The statement

`++nc;`

presents a new operator, ++, which means *increment* by *one*. You could instead write `nc = nc + 1`  but `++nc`  is more concise and often more efficient. There is a corresponding operator `--` to decrement by 1. The operators `++` and `--`  can be either prefix operators (++nc) or postfix operators (nc++); these two forms have different values in expressions, as will be shown in 

It may be possible to cope with even bigger numbers by using a `double`(double precision `float`). We will also use a `for` statement instead of a `while`, to illustrate another way to write the loop.

```c
# include <stdio.h>

/* count characters in input; 2nd version */
main() {
  double nc;
  
  for (nc=0; getchar() != EOF; ++nc)
    ;
  printf("%.0f\n", nc);
}
```

`printf` uses `%f` for both `float` and `double`; `%.0f` suppresses the printing of the decimal point and the fraction part, which is zero.



## 1.6  Arrays



## 1.7  Functions



## 1.8  Arguments - Call by Value



## 1.9  Character Arrays



## 1.10  External Variables and Scope



---



# Chapter 4





## 4.7 Register Variables

A `register` declaration advises the compiler that the variable in question will be heavily used. The idea is that `register` variables are to be placed in machine registers, which may result in smaller and faster programs. But compilers are free to ignore the advice.

The `register` declaration looks like

```c
register int x;
register char c;
```







## 4.9 Initialization

Initialization has been mentioned in passing many times so far, but always peripherally to some other topic. This section summarizes some of the rules, now that we have discussed the various storage classes.



Scalar variables may be initialized when they are defined, by following the name with an equals sign and an expression:

```c
int x = 1;
char squota = '\'';
long day = 1000L * 60L * 60L * 24L; /* milliseconds/day */	
```

For external and static variables, the initializer must be a constant expression; the initialization is done once, conceptionally before the program begins execution. For automatic and register variables, the initializer is not restricted to being a constant: it may be any expression involving previously defined values, even function calls. For example, the initialization of the binary search program in <u>Section 3.3</u> could be written as 

```c
int binsearch(int x, int v[], int n) {
  int low = 0;
  int high = n - 1; /* "-" : minus */
  int mid;
  ...
}
```

instead of 

```c
int low, high, mid;

low = 0;
high = n - 1;
```

















# Chapter 7.  Input and Output

Input and output are not part of the C language itself, so we have not emphasized them in our presentation thus far. Nonetheless, programs interact with their environment in much more complicated ways than those we have shown before.

## 7.1  Standard Input and Output 

Many programs read only one input stream and write only one output stream; for such programs, input and output with `getchar`, `putchar`, and `printf` may be entirely adequate, and is certainly enough to get started. This is particularly true if redirection is used to connect the output of one program to the input of the next. For example, consider the program `lower`, which converts its input to lower case:

```c
# include <stdio.h>
# include <ctype.h>

/* lower: convert input to lower case */
main() {
  int c;
  
  while ((c=getchar()) != EOF)
    putchar(tolower(c));
  return 0;
}
```





## 7.2  Formatted output - Printf



## 7.3  Variable-length Argument Lists

The proper declaration for `printf` is 

```c
int printf(char *fmt, ...)
```

where the declaration ... means that the number and types of these arguments may vary. The declaration ... can only appear at the end of an argument list. Our `minprintf` is declared as 

```c
void minprintf(char *fmt, ...)
```

since we will not return the character count that `printf` does.

The tricky bit is how `minprintf` walks along the argument list when the list doesn't even have a name. The 



These properties form the basis of our simplified `printf`:

```c
# include <stdarg.h>

/* minprintf: minimal printf with variable argument list */
void minprintf(char *fmt, ...) {
  va_list ap;  /* points to each unnamed arg in turn */
  char *p, * sval;
  int ival;
  double dval;
  
  va_start(ap, fmt);  /* make ap point to 1st unnamed arg */
  for (p=fmt; *p; p++) {
    if (*p != '%') {
      putchar(*p);
      continue;
    }
    switch (*++p) {
      case 'd':
        ival = va_arg(ap, int);
        printf("%d", ival);
        break;
      case 'f':
        dval = va_arg(ap, double);
        printf("%f", dval);
        break;
        
    }
  }
}
```





## 7.4  Formatted Input - Scanf



## 7.5  File Access



## 7.6  Error Handling - Stderr and Exit





## 7.7 Line Input and Output

The standard library provides an input routine fgets that is similar to the getline function that we have used in earlier chapters:

```c
char * fgets(char *line, int maxline, FILE *fp)
```

fgets reads the next input line (including the newline) from file fp into the character array line; at most maxline - 1 characters will be read. The



7.8 Miscellaneous Functions



# Appendix B - Standard Library





## B.3 String Functions: <string.h>



### bcmp() : 比较字符串是否相等

函数原型：

```c
int bcmp(const void *s1, const void *s2, int n);
```



```c
# include <stdio.h>
# include <string.h>

void main() {
  char *s1 = "Golden Global View";
  char *s2 = "Golden global view";
  clrscr();
  if(!bcmp(s1, s2, 7))
    printf("s1 equal to s2 in first 7 bytes");
  else 
    printf("s1 not equal to s2 in first 7 bytes");
  if(!)
}
```
