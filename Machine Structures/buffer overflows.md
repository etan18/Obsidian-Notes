Within computer [[memory structure]], a **buffer overflow** is one of the most common vulnerabilities. 

### background
These threats are seen most commonly in low-level languages like C/C++. A particular weakness of these languages is the absence of automatic bounds checking for array or pointer accesses. Without adequate safety checks implemented by the programmer, attackers can use out-of-bounds memory accesses to corrupt the program’s intended behavior.

```
char buf[8];
int authenticated = 0;
void vulnerable() {
    gets(buf);
}
```

In this sample code, note that `buf` and `authenticated` are both stored in static memory, right next to one another. A call to the function `vulnerable` writes standard user input to the character array `buf`. However, if the input contains more than 8 bytes of data, then `gets` will *overwrite* `authenticated`. Attackers can manipulate this behavior to set `authenticated` to 1 and gain access to the system.

## stack smashing
**Stack smashing** is a malicious attack that extends on the previous example. Let's say that we run some function `vulnerable`. When that function is called, a *stack frame* is pushed onto the stack, containing the `sfp` and `rip` of `vulnerable`. Now, using the same technique as the code snippet in the previous section, we can now overwrite the `sfp` and `rip` to insert our own malicious code. Here, the attacker could input

```
AAAAAAAAAAAA\xef\xbe\xad\xde
```

where `AAAAAAAAAAAA` are 8 bytes of garbage to fill the pre-defined buffer, as well as the `sfp`. The following characters consist of what will overwrite the `rip`.  This malicious code is often called **shellcode**, because the malicious code is often written to spawn an interactive shell that lets the attacker perform arbitrary actions.

#### mitigation
###### data execution prevention
One way to mitigate stack smashing attacks is to designate areas as *either executable OR writeable*. If a user can write to a page, it can't be executed, and if a program can execute a page, it can't be written to. This defense is known in practice as **W^X**—write XOR execute—or **Data Execution Prevention** (DEP). This can also be implemented using a *No Execute (NX)-bit*.
###### stack canaries
When we call a function, the [[compiler]] places a known dummy value, the _stack canary_, on the stack. When the function returns, the compiler checks that the canary value has not been changed.
- If it has been changed, this is evidence that something bad has happened
- Otherwise, continue

