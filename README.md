## 0x19. C - Stacks, Queues - LIFO, FIFO

# Monty Interpreter

A language interpreter made in the C programming language to manage stacks and queues (LIFO and FIFO). The aim is to interpret Monty bytecodes files. [Monty](http://montyscoconut.github.io/) is a language that aims to close the gap between scripting and programming languages.

# Compilation & Output

```
$ gcc -Wall -Werror -Wextra -pedantic -std=c89 *.c -o monty
```

# Option Codes

## Push opcode

The opcode `push` pushes an element to the stack.

**Usage:** `push <int>`, where *int* is an integer.

## Pall opcode

The opcode `pall` prints all the values on the stack, starting from the top of the stack.

**Usage:** `pall`. If the stack is empty, `pall` don’t print anything.
```
julien@ubuntu:~/monty$ cat -e bytecodes/00.m
push 1$
push 2$
push 3$
pall$
julien@ubuntu:~/monty$ ./monty bytecodes/00.m
3
2
1
julien@ubuntu:~/monty$
```
## Pint opcode

The opcode `pint` prints the value at the top of the stack, followed by a new line.

**Usage:** `pint`. If the stack is empty, `pint` print an error message.
```
julien@ubuntu:~/monty$ cat bytecodes/06.m 
push 1
pint
push 2
pint
push 3
pint
julien@ubuntu:~/monty$ ./monty bytecodes/06.m 
1
2
3
julien@ubuntu:~/monty$

```
## Pop opcode

The opcode `pop` removes the top element of the stack.

**Usage:** `pop`. If the stack is empty, `pop` print an error message.

```
julien@ubuntu:~/monty$ cat bytecodes/07.m 
push 1
push 2
push 3
pall
pop
pall
pop
pall
pop
pall
julien@ubuntu:~/monty$ ./monty bytecodes/07.m 
3
2
1
2
1
1
julien@ubuntu:~/monty$
```
## Swap opcode

The opcode `swap` swaps the top two elements of the stack.

**Usage:** `swap`. If the stack contains less than two elements, `swap` print an error message.

```
julien@ubuntu:~/monty$ cat bytecodes/09.m 
push 1
push 2
push 3
pall
swap
pall
julien@ubuntu:~/monty$ ./monty bytecodes/09.m 
3
2
1
2
3
1
julien@ubuntu:~/monty$
```
## Add opcode

The opcode `add` adds the top two elements of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `add`. If the stack contains less than two elements, `add` print an error message.

```
julien@ubuntu:~/monty$ cat bytecodes/12.m 
push 1
push 2
push 3
pall
add
pall

julien@ubuntu:~/monty$ ./monty bytecodes/12.m 
3
2
1
5
1
julien@ubuntu:~/monty$
```
## Nop opcode

The opcode `nop` doesn’t do anything.

**Usage:** `nop`.

## Sub opcode

The opcode `sub` subtracts the top element of the stack from the second top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `sub`. If the stack contains less than two elements, `sub` print an error message.

```
julien@ubuntu:~/monty$ cat bytecodes/19.m 
push 1
push 2
push 10
push 3
sub
pall
julien@ubuntu:~/monty$ ./monty bytecodes/19.m 
7
2
1
julien@ubuntu:~/monty$
```
## Div opcode

The opcode `div` divides the second top element of the stack by the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `div`. If the stack contains less than two elements, `div` print an error message.

## Mul opcode

The opcode `mul` multiplies the second top element of the stack with the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `mul`. If the stack contains less than two elements, `mul` print an error message.
## Mod opcode

The opcode `mod` computes the rest of the division of the second top element of the stack by the top element of the stack. The result is stored in the second top element of the stack, and the top element is removed, so that at the end:

* The top element of the stack contains the result
* The stack is one element shorter

**Usage:** `mod`. If the stack contains less than two elements, `mod` print an error message.

## Comments

Every good language comes with the capability of commenting. When the first non-space character of a line is `#`, treat this line as a comment (don’t do anything).

## Pchar opcode

The opcode `pchar` prints the char at the top of the stack, followed by a new line. The integer stored at the top of the stack is treated as the ascii value of the character to be printed.

**Usage:** `pchar`

* If the value is not in the ascii table (`man ascii`), `pchar` print an error message.
* If the stack is empty, `pchar` print an error message.

```
julien@ubuntu:~/monty$ cat bytecodes/28.m 
push 72
pchar
julien@ubuntu:~/monty$ ./monty bytecodes/28.m 
H
julien@ubuntu:~/monty$
```
## Pstr opcode

The opcode `pstr` prints the string starting at the top of the stack, followed by a new line. The integer stored in each element of the stack is treated as the ascii value of the character to be printed.

**Usage:** `pstr`. If the stack is empty, `pstr` print only a new line

```
julien@ubuntu:~/monty$ cat bytecodes/31.m 
push 1
push 2
push 3
push 4
push 0
push 110
push 0
push 108
push 111
push 111
push 104
push 99
push 83
pstr
julien@ubuntu:~/monty$ ./monty bytecodes/31.m 
School
julien@ubuntu:~/monty$
```
## Rotl opcode

The opcode `rotl` rotates the stack to the top. The top element of the stack becomes the last one, and the second top element of the stack becomes the first one.

**Usage:** `rotl`

```
julien@ubuntu:~/monty$ cat bytecodes/35.m 
push 1
push 2
push 3
push 4
push 5
push 6
push 7
push 8
push 9
push 0
pall
rotl
pall
julien@ubuntu:~/monty$ ./monty bytecodes/35.m 
0
9
8
7
6
5
4
3
2
1
9
8
7
6
5
4
3
2
1
0
julien@ubuntu:~/monty$
```
## Rotr opcode

The opcode `rotr` rotates the stack to the bottom. The last element of the stack becomes the top element of the stack.

**Usage:** `rotr`

## Stack opcode

The opcode `stack` sets the format of the data to a stack (LIFO). This is the default behavior of the program.

**Usage:** `stack`
## Queue opcode

The opcode `queue` sets the format of the data to a queue (FIFO).

**Usage:** `queue`

```
julien@ubuntu:~/monty$ cat bytecodes/47.m
queue
push 1
push 2
push 3
pall
stack
push 4
push 5
push 6
pall
add
pall
queue
push 11111
add
pall
julien@ubuntu:~/monty$ ./monty bytecodes/47.m
1
2
3
6
5
4
1
2
3
11
4
1
2
3
15
1
2
3
11111
julien@ubuntu:~/monty$
```
## Some Brainfuck Tasks

[Brainfuck](https://en.wikipedia.org/wiki/Brainfuck) is an esoteric programming language created in 1993 by Urban Müller. Here are some testing scripts.

```
julien@ubuntu:~/monty/bf$ bf 1000-school.bf 
School
julien@ubuntu:~/monty/bf$
```
## Add two digits

Add two digits given by the user.

* Read the two digits from stdin, add them, and print the result
* The total of the two digits with be one digit-long (<10)

```
julien@ubuntu:~/monty/bf$ bf ./1001-add.bf
81
9julien@ubuntu:~/monty/bf$
```
## Multiplication
Multiply two digits given by the user.

* Read the two digits from stdin, multiply them, and print the result
* The result of the multiplication will be one digit-long (<10)
```
julien@ubuntu:~/monty/bf$ bf 1002-mul.bf
24
8julien@ubuntu:~/monty/bf$
```


## Multiplication level up

Multiply two digits given by the user.

* Read the two digits from stdin, multiply them, and print the result, followed by a new line
```
julien@ubuntu:~/monty/bf$ bf 1003-mul.bf 
77
49
julien@ubuntu:~/monty/bf$
```
