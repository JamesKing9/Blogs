





# Chapter 7.  Input and Output



7.1  Standard Input and Output 



7.2  Formatted output - Printf



7.3  Variable-length Argument Lists



7.4  Formatted Input - Scanf



7.5  File Access



7.6  Error Handling - Stderr and Exit





## 7.7 Line Input and Output

The standard library provides an input routine fgets that is similar to the getline function that we have used in earlier chapters:

```c
char * fgets(char *line, int maxline, FILE *fp)
```

fgets reads the next input line (including the newline) from file fp into the character array line; at most maxline - 1 characters will be read. The



7.8 Miscellaneous Functions