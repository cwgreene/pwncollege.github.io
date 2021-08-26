# Module: Program Interaction

This module tests your existing knowledge of interacting with programs!

## Lectures

Here is the introductory lecture:

- [Program Interaction: Linux Command Line](https://www.youtube.com/watch?v=w7nQFk6bi_k) (slides [here](https://docs.google.com/presentation/d/1aiHdtSm8xoT0u2XcTo3qYGes5GY__-PK-FlVyNBQAfY/edit#slide=id.g88f71ddc4c_0_0))

The following videos have been upgraded from Fundamentals to a core part of this module!

- [Program Interaction: Binary Files](https://www.youtube.com/watch?v=nKqFeYJ483U) (slides [here](https://docs.google.com/presentation/d/1wrX8tvwaxIEk5hx4OtQmPqps-MScIaDO-9bTKQqr8vI/edit?usp=sharing))
- [Program Interaction: Linux Process Loading](https://www.youtube.com/watch?v=kUMCAzSOY-o) (slides [here](https://docs.google.com/presentation/d/1TwM5WLWnTqrNkpXjGKkaXYbKZEpatEQYA7ckBVXAOhs/edit?usp=sharing))
- [Program Interaction: Linux Process Execution](https://www.youtube.com/watch?v=Vtb5wIlthRg) (slides [here](https://docs.google.com/presentation/d/1ezY9Q8I0tzDD-7ZDXMbQM5RQ7z1dvB9-U_nDEhc6qdE/edit#slide=id.g8a9f5b81a5_0_0))

The following live Q&As were done for this module:

- [8/24/21](https://youtu.be/HroVArg5s5A)

## Practice Problems

Practice problems for this module are live at [the dojo](https://dojo.pwn.college/challenges/interaction)!

## Helpful stuff

- For launching programs from Python, we recommend using [pwntools](https://docs.pwntools.com/en/stable/intro.html), but [subprocess](https://docs.python.org/3/library/subprocess.html) should work as well. If you are not using one of these two, you will suffer heavily when you get to input redirection (for that, check out the `stdin` and `stdout` arguments to `pwn.process` or `subprocess.Popen`).
- For reading and writing directly to file descriptors in bash, check out the `read` and `echo` builtins.
- You will find the `env` command useful, and the `exec` bash builtin.
- Quick refreshers on `fork()` versus `exec*()` [here](https://www.geeksforgeeks.org/difference-fork-exec/) and [here](https://linuxhint.com/linux-exec-system-call/) and [here](https://iximiuz.com/en/posts/how-to-on-processes/).
- Remember to `wait()` on your children! If you use `subprocess.Popen`, `pwn.process`, or good old `fork()`, your parent will keep executing and, unless it waits for the child in some way, will just terminate! This is almost never what you want.
- Some [documentation](https://www.binarytides.com/socket-programming-c-linux-tutorial/) on networking in C.
- Useful resource for [pipes in C](https://jameshfisher.com/2017/02/17/how-do-i-call-a-program-in-c-with-pipes/).
- Useful resource for [FIFOs in C](https://www.geeksforgeeks.org/named-pipe-fifo-example-c-program/).
- A treatise on I/O redirection in Linux shells, which has applications in this assignment: [https://bencane.com/2012/04/16/unix-shell-the-art-of-io-redirection/](https://bencane.com/2012/04/16/unix-shell-the-art-of-io-redirection/)
- A guide on Linux symbolic links. [https://www.nixtutor.com/freebsd/understanding-symbolic-links/](https://www.nixtutor.com/freebsd/understanding-symbolic-links/)

## Programs accessing arguments and environment variables

Some of the challenges will take input from an [environment variable](https://wiki.archlinux.org/index.php/environment_variables) or commandline arguments.
The linked material for it above is useful --- read it.

This subsection is a quick example of how to reverse-engineer a program that accesses commandline variables and environment variables.
As discussed in class, in C, this data is provided as arguments to the `main` function, like this:

```
int main(int argc, char **argv, char **envp)
{
	printf("The number of arguments is: %d\n", argc);
	printf("The program name is: %s\n", argv[0]);
	printf("The first argument is: %s\n", argv[1]);
	printf("The first environment variable is: %s\n", envp[0]);
	printf("The second environment variable is: %s\n", envp[1]);
}
```

`argc` is the number of arguments.
`argv` is a pointer to an array of pointers that each point to an argument, where each argument is a string.
More information is available [here](http://pages.cs.wisc.edu/~smoler/cs354/onyourown/C.argv.html), with more discussion (and some nit-picking) [here](https://stackoverflow.com/questions/17254853/argv-pointer-to-an-array-of-pointers).
`envp` is the same structure as `argv` (a pointer to an array of pointers), but each entry is an environment variable string in the format `NAME=value`.

Let's run it and see what happens!

```
$ gcc -o test test.c
$ ./test testing
The number of arguments is: 2
The program name is: ./test
The first argument is: testing
The first environment variable is: PWD=/home/yans
The second environment variable is: SHLVL=1
```

A few things to unpack here.
First, why is `number of arguments` 2?
That's because the name of the program (`./test`) comes across as the first entry in `argv` (`argv[0]`), and the actual first argument is the second (`argv[1]`).
If there were more arguments, they would be pointed to by `argv[2]`, `argv[3]`, and so on.
What if there are no arguments?

```
$ ./test
The number of arguments is: 1
The program name is: ./test
The first argument is: (null)
The first environment variable is: PWD=/home/yans
The second environment variable is: SHLVL=1
```

Interestingly, it prints `(null)` for the second argument.
`printf` does this when the argument passed to `%s` is a NULL pointer.
The last element of the `argv` and `envp` arrays is always a NULL pointer, so that you know when to stop if you are looping through them (you can also use `argc` to tell when to stop for `argv`, but there's no equivalent to `argc` for `envp`).

Now, what about the environment variables?
They're stored similarly to environment variables, with the difference that each variable value is prepended by its variable name in a `NAME=value` pair.
The order is arbitrary; they just happen to be in some order (probably chronologically in the order that they were set).
In the shell above, the first environment variable is `PWD` (the process working directory), with a value of `/home/yans`, and the second is `SHLVL`, with a value of 1.
There are a _lot_ of environment variables in a normal shell.
Here is a program that counts the number:

```
int main(int argc, char **argv, char **envp)
{
	int num_vars = 0;
	while (*envp)
	{
		envp++;
		num_vars++;
	}
	printf("There are %d environment variables.\n", num_vars);
}
```

This program increments the `envp` environment (using [pointer arithmetic](https://www.tutorialspoint.com/cprogramming/c_pointer_arithmetic.htm), which you should know) until it points to the NULL value that terminates the `envp` array, at which point dereferencing the `envp` pointer (`*envp`) will result in NULL, and the `while` loop will terminate.
The number of times it had to increment it (`num_vars`) is the number of environment variables we have.
If I run it in my shell, I get:

```
$ gcc countenv.c -o countenv
$ ./countenv
There are 59 environment variables.
```

Quite a few.
`env` runs a command with a modified environment.
For example, `env -i` will run it with an empty environment.

```
$ env -i ./countenv
There are 0 environment variables.
```

I can also use `env` to set environment variables.

```
$ env -i NAME=Yan JOB=Professor ./countenv
There are 2 environment variables.
```

And we can view them:

```
$ env -i NAME=Yan JOB=Professor ./test
The number of arguments is: 1
The program name is: ./test
The first argument is: (null)
The first environment variable is: NAME=Yan
The second environment variable is: JOB=Professor
```

Amazing.

## COMPLICATION: The binaries demand to read or write files that I don't have permission to!

You'll notice that the directory where all of the challenges reside is not writable by non-root users.
This is a problem because some of the challenges will attempt to create or open files in this directory, which will fail.

All of the challenges open files using a _relative path_ (i.e., `open("blah", 0);`).
Relative paths are relative to the _current working directory_ of the process.
You should watch lecture 1 of this module or google this concept to understand what to do to make these challenges work.
