# Module: Program Interaction

This module tests your existing knowledge of interacting with programs!

## Lectures

Here is the introductory lecture:

- [Program Interaction: Linux Command Line](https://www.youtube.com/watch?v=w7nQFk6bi_k) (slides [here](https://docs.google.com/presentation/d/1aiHdtSm8xoT0u2XcTo3qYGes5GY__-PK-FlVyNBQAfY/edit#slide=id.g88f71ddc4c_0_0))

The following videos have been upgraded from Fundamentals to a core part of this module!

- [Program Interaction: Binary Files](https://www.youtube.com/watch?v=nKqFeYJ483U) (slides [here](https://docs.google.com/presentation/d/1wrX8tvwaxIEk5hx4OtQmPqps-MScIaDO-9bTKQqr8vI/edit?usp=sharing))
- [Program Interaction: Linux Process Loading](https://www.youtube.com/watch?v=kUMCAzSOY-o) (slides [here](https://docs.google.com/presentation/d/1TwM5WLWnTqrNkpXjGKkaXYbKZEpatEQYA7ckBVXAOhs/edit?usp=sharing))
- [Program Interaction: Linux Process Execution](https://www.youtube.com/watch?v=Vtb5wIlthRg) (slides [here](https://docs.google.com/presentation/d/1ezY9Q8I0tzDD-7ZDXMbQM5RQ7z1dvB9-U_nDEhc6qdE/edit#slide=id.g8a9f5b81a5_0_0))

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
