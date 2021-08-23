# Module: Misusing Programs

This module explores the impact of program misuse (specifically, of SUID programs) on the security of a system.

## Lectures

The video for the lecture is this:

- [Privilege Escalation](https://youtu.be/ZWxYWdiXqD8) (slides [here](https://docs.google.com/presentation/d/1EB7dL5gx3pQlPDqZSEqTtlDiJRZmHGbqRnwxgm4feuw/edit#slide=id.g8a9f5b81a5_0_0))
- [Mitigations](https://youtu.be/kzbyvr_PJ9k) (slides [here](https://docs.google.com/presentation/d/1pvWd6n4UN3lZ1BdRySWDl80iEYGRJj9VC5exbYlGdAg/edit#slide=id.g8a9f5b81a5_0_0))

Additionally, the following lectures may be useful for this module:

- [Program Interaction: Binary Files](https://www.youtube.com/watch?v=nKqFeYJ483U) (slides [here](https://docs.google.com/presentation/d/1wrX8tvwaxIEk5hx4OtQmPqps-MScIaDO-9bTKQqr8vI/edit?usp=sharing))
- [Program Interaction: Linux Process Loading](https://www.youtube.com/watch?v=kUMCAzSOY-o) (slides [here](https://docs.google.com/presentation/d/1TwM5WLWnTqrNkpXjGKkaXYbKZEpatEQYA7ckBVXAOhs/edit?usp=sharing))
- [Program Interaction: Linux Process Execution](https://www.youtube.com/watch?v=Vtb5wIlthRg) (slides [here](https:
//docs.google.com/presentation/d/1ezY9Q8I0tzDD-7ZDXMbQM5RQ7z1dvB9-U_nDEhc6qdE/edit#slide=id.g8a9f5b81a5_0_0))

## Practice

Practice problems for this module will go live on [the dojo](https://dojo.pwn.college) on **August 24, 2021**.

## Freebies!

Here are several freebies to help you get started.
Feel free to use these solutions!
Later programs will be more tricky.

`cat` is a program that concatenates files and prints them out to standard out.
Thus, after launching an instance with `/bin/cat` as the chosen file, retrieving the flag with it is quite simple:

```
cse466@b38bdd753b5b:~$ cat /flag
pwn_college{747985b99bd25b8805ced639297720ae71e87a7acef580dc6b514143e5152133}
cse466@b38bdd753b5b:~$ exit
```

As you can see, this gives you the flag associated with `cat`.
Let's choose another program: say, `tail` (you may use this for another solution!).
`tail` is a program that prints out the last few lines of a file.
Since the `/flag` file only has one line (the flag), this is perfect for us!
Specifying `/usr/bin/tail`, you will receive another flag:

```
cse466@b38bdd753b5b:~$ tail /flag
pwn_college{7ca9d3c2fcbaa0c0cde22777bfefff2a5f5ac707f5194f91cd24226dbae0b74b}
cse466@b38bdd753b5b:~$ exit
```

Now, you have two flags: one for `cat` and one for `tail`.
Note that, while `cat` and `tail` is easy, other programs are not so simple to read flags with.

For a slightly more complex example, let's look at `/usr/bin/chmod`.
`chmod` is a program that can change permissions of files.
There are _many_ ways to read the `/flag` file with `chmod`.
We'll cover a few here (feel free to use this for one of your solutions!).

First, we can simply change the permissions of the `/flag` file to allow us to read it:

```
cse466@5d1f52fff4e8:~$ chmod 644 /flag
cse466@5d1f52fff4e8:~$ cat /flag
pwn_college{36ef1e24753a8e3119eeac953e44f47f48aa388f9a72e2cb2d54fc9a622c5ef8}
cse466@5d1f52fff4e8:~$ exit
```

Second, we can make the `/bin/cat` binary SUID, so that _it_ runs as root and lets us read the flag.

```
cse466@5d1f52fff4e8:~$ chmod 4755 /bin/cat
cse466@5d1f52fff4e8:~$ cat /flag
pwn_college{36ef1e24753a8e3119eeac953e44f47f48aa388f9a72e2cb2d54fc9a622c5ef8}
cse466@5d1f52fff4e8:~$ exit
```

And we can do the same with other binaries, such as `/usr/bin/tail`:

```
cse466@5d1f52fff4e8:~$ chmod 4755 /usr/bin/tail
cse466@5d1f52fff4e8:~$ cat /flag
pwn_college{36ef1e24753a8e3119eeac953e44f47f48aa388f9a72e2cb2d54fc9a622c5ef8}
cse466@5d1f52fff4e8:~$ exit
```

Note that all three ways of getting the flag after specifying `chmod` _get the same flag_.
One challenge, one flag, and `chmod` is one challenge.
`chmod` is great, and it'll let you run _any_ binary with SUID, but it'll only get you one flag.

Now you have _three_ freebies.
Go get the rest!

## HINT: Reading program documentation

To get a flag using a given program, you need to understand how the program works.
For `cat` and `tail` it's easy.
Can you get the flag using `whiptail`, a program that is used to create TUIs (Text User Interfaces)?
Hint: yes, but you need to know how to use whiptail!

So, how do you learn?
There are two main ways: the program help and the program manual.
The program help is generally accessed by using the `-h`, `--help`, or `--usage` options (i.e., `whiptail --usage`).
The program manual is generally accessible using the `man` or `info` commands (`man whiptail` or `info whiptail`).

To save disk space, the manuals aren't installed on our system, but you can also find manuals on google.
For example, googling `man whiptail` will bring up the `whiptail` manual.

Remember!
This is a _hacking_ challenge. You will have to *abuse* these programs.
They might not be originally intended to read out files, but you can often misuse their functionality to do so.
Their documentation is your friend.

## HINT: Dealing with errors

In the course of trying to abuse programs into giving you the flag, they might fail in weird ways.
They might also fail in weird ways because of the way the container is run.
As a rule of thumb, you should google all the errors that you get.
Sometimes, the solution is quite simple!

`/bin/whiptail` is a great example of this: depending on exactly how you interact with the dojo, some it might not work at all right out of the box, but the error that it gives you (`TERM environment variable needs set.`), and the [first result on google](https://stackoverflow.com/questions/16242025/term-environment-variable-not-set) shows you how to fix that.
There are other good examples of this (such as `/bin/nano`).

## Other hints

Also keep in mind a few hints:

1. The flag is stable across connections and program executions, for the same SUID binary. That means that you don't necessarily have to read the entire flag, cleanly, in one swoop. Some programs might mangle it (but in a way that you can unmangle), and some programs might only be able to leak a small amount of it in a single execution, but can leak the whole flag when executed multiple times. If you find the flag changing for a single program, that probably means that the program itself is mangling it.
1. Think very carefully about how programs present information to you when they don't think that information is something critical. Debug info when debug flags are enabled. Error messages containing data that isn't sensitive when it's data you have access to anyways, but could be sensitive when the program has access to data that you don't have access to. These situations expose methods that you can abuse certain programs to get flags.
1. Sometimes, lazy programmers call out to other utilities instead of writing the functionality themselves. What happens if those other utilities are SUID root? What happens if you can influence where those other utilities are launched from (i.e., check out the PATH variable). This relies on lazy programming of the utilities that you are attacking, so you might want to pick up other targets before going down this path.

## Further Reading

Some other useful resources:

- A primer on Linux file permissions: [https://wiki.archlinux.org/index.php/File_permissions_and_attributes](https://wiki.archlinux.org/index.php/File_permissions_and_attributes)
- A primer on privilege escalation attacks against Linux hosts. The SUID abuse section has obvious implications for this assignment: [https://payatu.com/guide-linux-privilege-escalation/](https://payatu.com/guide-linux-privilege-escalation/)
- Some thoughts on abusing dangers in SUID executables: [https://www.pentestpartners.com/security-blog/exploiting-suid-executables/](https://www.pentestpartners.com/security-blog/exploiting-suid-executables/)
- Another SUID attack tutorial: [https://null-byte.wonderhowto.com/how-to/use-misconfigured-suid-bit-escalate-privileges-get-root-0173929/](https://null-byte.wonderhowto.com/how-to/use-misconfigured-suid-bit-escalate-privileges-get-root-0173929/)
- Another SUID tutorial. It is focused on shell scripts, but there are insights that can be used: [http://www.drdobbs.com/dangers-of-suid-shell-scripts/199101190](http://www.drdobbs.com/dangers-of-suid-shell-scripts/199101190)
