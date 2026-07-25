# Minishell

_lucinguy & ccauderl_  
_(piscine of september's 2025 - 42 PARIS)_ 

## Description

The **Minishell** project is about writing our own shell, based on bash posix. This was part of the 
 school curriculum.
### Instructions

It must contain the following features :
- Display of a prompt when waiting for a new command
- Have a working history
- Search and launch the right executable (based on the PATH or using a relative/absolute path)
- Indicate a received signal.
- Handle single and double quotes
- Handle the following redirections:
	- < to redirect input
	- \> to redirect output
	- << and >>
- pipes
- Handle environment variables
- Handle ctrl-C, ctrl-D and ctrl-\
- The following built-in :
	- echo (and its flag -n)
	- cd with only a relative or absolute path
	- pwd
	- export
	- unset
	- env (with no argument)
	- exit

### Parts

We divided the project into several sections :
- Signal : handle the received signals and execute the right behaviour
- Environment : manage the environment variables and recreate some if none are accessible
- Tokenizer : expand environment variables, divide the received prompt into tokens, assign to each token a type (ex: WORD, PIPE, REDIRECTION, ...)
- Execution : Execute the commands and the redirections
- Built-in : the built-in functions, which are accessible even if there is no environment variable.

## Instructions

***Usage***  
1) make all
2) ./minishell (no args)
3) execute commands in our minishell

***Examples***  
*in minishell :*
```bash
> ls -la | grep "." | wc
> < Makefile wc | cat > out
> << EOF cat
> echo "hi $USER, you're currently here : $PWD"
> export NEWVAR=blabla (then again export to see the result)
> unset NEWVAR
> cd srcs/
> echo -n hello >> out
> echo $?
> env
> pwd
```  

***Check leaks***  
valgrind --suppressions=readline.supp --leak-check=full --show-leak-kinds=all ./minishell

## Resources
Bash Reference Manual :
https://www.gnu.org/software/bash/manual/bash.html#What-is-Bash_003f

A tutorial to start the tokenizer :
https://mvsrgc.xyz/posts/Write-a-Shell-Tokenizer-in-C/

GNU Readline Library :
https://tiswww.cwru.edu/php/chet/readline/readline.html

A tutorial about signals :
https://www.geeksforgeeks.org/c/signals-c-language/

Another tutorial about enumerations:
https://www.w3schools.com/c/c_enums.php

A project subject about writing a shell from the Northeatern University:
https://course.ccs.neu.edu/cs3650sp23/p1.html

A site used to have the manual to the authorized functions:
https://man7.org/linux/man-pages/
