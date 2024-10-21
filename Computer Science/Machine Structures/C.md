C/C++ is a function-oriented, low level programming language.

### memory
C [[memory structure]] requires much more manual management by the program than a more high level language such as Python.
##### pointers
Pointers are variables that store a memory address.
```c
char str[7] = "String";
int var = 5;

int *ptr; //currently points to "nothing" but can point to a stored int 
char *ptr = str; //pointer storing the starting address of string str
int ptr = &var; //pointer to the memory address of var
```

To manage pointers, we have the following operators:
- The asterisk `*` we put in front of pointers is the **dereferencing operator.**
- The ampersand `&` is the *address* of operator.

So, for something like
```c
char *ptr = str;
```
the value of $\verb|ptr|$ is the _address of_ the first character in $\verb|str|$, whereas $\verb|*ptr|$ would give its actual first character.

### pass by value
C and Java are languages that pass parameters ********by value.******** This means that when a variable is passed to a function as a parameter, the function receives a copy of the variable, and any changes made within the functions do not modify the original variable.

However, if a **pointer** to a variable is passed into the function, then that variable can be modified.

```c
void addOne (int *ptr) {
	*p = *p + 1
}

int y = 3;
addOne(&y)

printf(y)
>>> 4
```