---
title: "Introducing the Shell"
teaching: 5
exercises: 0
questions:
- "What is a command shell and why would I use one?"
objectives:
- "Explain how the shell relates to the keyboard, the screen, the operating system, and users' programs."
- "Explain when and why command-line interfaces should be used instead of graphical interfaces."
keypoints:
- "Explain the steps in the shell's read-run-print cycle."
- "Most commands take options (flags) which begin with a `-`."
- "Identify the actual command, options, and filenames in a command-line call."
- "Explain the steps in the shell's read-run-print cycle."
- "Demonstrate the use of tab completion and explain its advantages."
keypoints:
- "A shell is a program whose primary purpose is to read commands and run other programs."
- "The shell's main advantages are its high action-to-keystroke ratio, its support for
automating repetitive tasks, and its capacity to access networked machines."
- "The shell's main disadvantages are its primarily textual nature and how
cryptic its commands and operation can be."
---
### Background
-   At a high level, computers do four things:

    -   run programs
    -   store data
    -   communicate with each other, and
    -   interact with us
-   Computers can interact with us in many different ways:
    -   keyboard and mouse
    -   touch screen
    -   speech recognition
-   Traditional screen, mouse/touchpad, and keyboards are still dominant.
-   Within that mode, the **graphical user interface** (GUI) is the most widely used way to 
    interact with personal computers. 
    -   We give instructions (to run a program, to copy a file, to create a new folder/directory) with 
        the convenience of a few mouse clicks. 
    -   intuitive and easy to learn
    -   scales very poorly for a large stream of systematic instructions. Ex: copy the third line
        from each of 1000 text files into a single file; this will take hours.
-   The shell - a **command-line interface** makes such repetitive tasks automatic and fast. 
    -   Take a single instruction and repeat it as is or with some modification as many times as we want. 
    -   The task in the example above can be accomplished in a few minutes at most.
-   The heart of a command-line interface is a **read-evaluate-print loop** (REPL). 
    It is called so because when you type a command and press <kbd>Return</kbd> (also known as
    <kbd>Enter</kbd>) the shell:
    1.  <kbd>R</kbd>eads your command,
    2.  <kbd>E</kbd>valuates (or 'executes') it,
    3.  <kbd>P</kbd>rints the output of your command,
    4.  <kbd>L</kbd>oops back and waits for you to enter another command.


### The Shell

-   A Shell is a program which runs other programs rather than doing calculations itself.
-   It is just a "shell", in the sense of a snail, itself lifeless, but serving as a container
    for the real meat of the animal.
-   Those programs can be as complicated as climate modeling software and as simple as a
    program that creates a new directory.
-   The simple programs which are used to perform stand alone tasks are usually refered
    to as commands.
-   The most popular Unix shell is Bash
    -   The Bourne Again SHell --- so-called because it's derived from a 
        shell written by Stephen Bourne.
-   Bash is the default shell on most versions of Unix and in most packages
    that provide Unix-like tools for Windows.

-   When the shell is first opened, you are presented with a **prompt**,
    indicating that the shell is waiting for input.

~~~
$
~~~
{: .language-bash}

-   The shell typically uses `$ ` as the prompt, but may use a different symbol.
    We'll always show the prompt as `$ `.
-   <kbd>Importantly</kbd>: when typing commands, *do NOT type the prompt*, only the commands that follow it.

So let's try our first command, which will list the contents of the current directory:

~~~
$ ls
~~~
{: .language-bash}

~~~
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
~~~
{: .output}

> ## Command not found
> If the shell can't find a program whose name is the command you typed, it
> will print an error message such as:
>
> ~~~
> $ ks
> ~~~
> {: .language-bash}
> ~~~
> ks: command not found
> ~~~
> {: .output}
>
> Usually this means that you have mis-typed the command.
{: .callout}

### Is it difficult?

-   It is a different model of interacting than a GUI; it will take time and effort to learn.
-   A GUI presents you with choices and you select one. 
-   With a **command line interface** (CLI) the choices are combinations of commands and parameters
    -    more like words in a language than buttons on a screen. 
-   The optins are not simply presented to you so you must learn a bit
    -   like learning some vocabulary in a new language. 
-   A small number of commands gets you a long way
-   We'll cover those essential few today.

### Flexibility and automation

-   The grammar of a shell allows you to combine existing tools into powerful
    pipelines and handle large workloads automatically
-   Sequences of commands can be written into a *script*
    -   improving reproducibility,
    -   and repeatability

-   The command line is often the easiest way to interact with remote machines:
    -   supercomputers
    -   cloud computing
-   The shell is near essential to run many specialized tools:
    -   high-performance computational models.
    -   customizable data pipelines
-   As clusters and cloud computing systems are becoming common, so the shell 
    is becoming a necessary skill.
-   We can build on the command-line skills covered here to tackle a wide range of scientific
    questions and computational challenges.

## Nelle's Pipeline: A Typical Problem

Nelle Nemo, a marine biologist,
has just returned from a six-month survey of the
[North Pacific Gyre](http://en.wikipedia.org/wiki/North_Pacific_Gyre),
where she has been sampling gelatinous marine life in the
[Great Pacific Garbage Patch](http://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch).
She has 1520 samples in all and now needs to:

1.  Run each sample through an assay machine
    that will measure the relative abundance of 300 different proteins.
    The machine's output for a single sample is
    a file with one line for each protein.
2.  Calculate statistics for each of the proteins separately
    using a program her supervisor wrote called `goostats`.
3.  Write up results.
    Her supervisor would really like her to do this by the end of the month
    so that her paper can appear in an upcoming special issue of *Aquatic Goo Letters*.

It takes her about two weeks to run her samples by the assay machine.
Now she has the daunting task of analysing her results by running 'goostats'.
The bad news is that if she has to run `goostats` by hand using a GUI,
she'll have to select a file using an open file dialog 1520 times.
At 30 seconds per sample,
the whole process will take more than 12 hours
(and that's assuming the best-case scenario where she is ready to select the next file
as soon as the previous sample analysis has finished).
This zero-breaks always-ready scenario is only achievable by a machine so it would
likely take much longer than 12 hours, not to mention that
the chances of her selecting all of those files correctly are practically zero.
Missing that paper deadline is looking increasingly likely.

The next few lessons will explore what she should do instead.
More specifically, they explain how she can use a command shell to run the `goostats` 
program, using loops to automate the repetitive steps e.g. entering file names,
so that her computer can work 24 hours a day while she writes her paper.

As a bonus,
once she has put a processing pipeline together,
she will be able to use it again whenever she collects more data.

