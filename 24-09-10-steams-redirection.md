# Standard Streams

- **Program**: Something you can run (ex: python code)
- **Process:** Running instance of the program (ex: open vim file)
	- each process is given a *process ID (PID)*
	- Each process has to be started by another process, besides *PID 1* which is started by the Unix kernel itself
	- Programs that can act as PID 1 are called **init systems**.

- Each opened file is associated to a *numeric ID* called a **file descriptor**
- **Ex:** Suppose process A spawns process B
	- A is the parent and B is the child process
	- Process B inherits all the open file descriptors of its parent

By default, each process has 3 file descriptors: 
	1. FD 0 : **standard input**, `stdin`
	2. FD 1 : **standard output**, `stdout`
	3. FD 2 : **standard error**, `stderr`

These are not associated necessarily with files, for example, `stdin` = `input()` in Python and `stdout` = `print()` in Python.

# Redirection 

>**Recall**: Bash is to launch programs (create processes)

Here `stdin` comes from the terminal to the command, then if there's an error `sterr` will be sent back to the terminal, but if the process completed `stdout` will go to *output.txt*.

```bash
#redirect command stdout to a file
$ command > output.txt
#this is the same as
$ command 1> output.txt
```

To redirect `stderr`:
```bash
#redirect command stderr to a file
$ command 2> errors.txt
```

You can also stack redirections, and even to the same file.
```bash
$ command > output.txt 2> errors.txt
#this is the same as
$ command 2> errors.txt > output.txt
#to redirect both to the same file
$ command > errors.txt >&2
#this is the same as
$ command > errors.txt 1>&2
```

To redirect `stdin` from a file
```bash
$ command < input.txt
```
 And you can pipe 1 command to another

