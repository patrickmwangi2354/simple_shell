Writing a fully functional UNIX command line interpreter, also known as a shell, is a complex task that requires a deep understanding of system programming concepts, including process management, file descriptors, input/output redirection, and signal handling. However, I can provide a basic implementation of a shell that supports some common features

Usage: simple_shell
Your Shell should:

Display a prompt and wait for the user to type a command. A command line always ends with a new line.
The prompt is displayed again each time a command has been executed.
The command lines are simple, no semicolons, no pipes, no redirections or any other advanced features.
The command lines are made only of one word. No arguments will be passed to programs.
If an executable cannot be found, print an error message and display the prompt again.
Handle errors.
You have to handle the “end of file” condition (Ctrl+D)
You don’t have to:

use the PATH
implement built-ins
handle special characters : ", ', `, \, *, &, #
be able to move the cursor
handle commands with arguments


NB:



This simple shell uses fgets() to read a line of input from the user, then forks a child process to execute the command using execlp(). If execlp() returns, it means the command was not found, so the shell prints an error message and waits for the user to enter another command.

Note that this shell does not handle any special characters, such as quotes or backslashes, and it does not support arguments or built-in commands. It also does not use the PATH environment variable to search for executables, so the user must specify the full path to the executable..
