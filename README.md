# simple_shell

main.c

This is the main function of a shell program. It takes in the argument count and argument vector as parameters. It initializes an info_t struct array with the macro INFO_INIT, and sets the file descriptor for standard error output to 2.

If the argument count is 2, it attempts to open the file specified by the second argument in read-only mode. If the file cannot be opened, it exits with a status code of 126 if the error is due to permission issues or 127 if the file does not exist. If the file is successfully opened, it sets the readfd field of the info_t struct to the file descriptor of the opened file.

The function then calls populate_env_list to populate the environment variables in the info_t struct, followed by read_history to read the history file if it exists. Finally, it calls the hsh function, passing in the info_t struct and argument vector.

The function returns 0 on success and 1 on error.

shell.c
header file of a simple shell 

This is the header file for a simple shell implementation in C. The file defines several constants, structs, and function prototypes that are used in the implementation of the shell.

The file defines several constants such as READ_BUF_SIZE, WRITE_BUF_SIZE, CMD_NORM, CMD_OR, and CMD_AND, which are used in different parts of the code. It also defines the HIST_FILE and HIST_MAX constants, which are used for storing and managing command history.

The file also defines two structs, list_t and info_t. The list_t struct is a singly linked list that contains a number field and a string field. The info_t struct contains pseudo-arguments to pass into a function, allowing for a uniform prototype for function pointer struct.

The file defines several function prototypes, such as hsh(), find_builtin(), find_cmd(), fork_cmd(), and others, which are used in the implementation of the shell. These functions handle different parts of the shell's functionality, such as parsing input, executing commands, and managing history.

The file also includes several standard library headers such as stdio.h, stdlib.h, unistd.h, string.h, sys/types.h, sys/wait.h, sys/stat.h, limits.h, fcntl.h, and errno.h.





atoi.c

This code/file contains several utility functions that are commonly used in shell programming:

interactive() function checks if the shell is in interactive mode, which means that the shell is reading input from the user directly through a terminal.

is_delim() function checks if a given character is a delimiter character. Delimiters are commonly used in shell programming to separate arguments and commands.

_isalpha() function checks if a given character is an alphabetic character.

_atoi() function converts a string of characters to an integer value.

These utility functions are used by the shell program to perform various tasks, such as parsing user input, checking for special characters, and converting strings to numerical values.

builtin.c
The role of the code is to define built-in shell commands for the custom shell program. The built-in commands include _myexit, _mycd, and _myhelp.

_myexit exits the shell program with a given exit status if the argument passed to it is "exit". If an exit argument is provided, it checks if it is a valid integer and exits with that value if it is. If it is not a valid integer, it prints an error message and sets the exit status to 2.

_mycd changes the current working directory of the shell program. If no argument is provided, it changes to the home directory. If "-" is provided as the argument, it changes to the previous directory. If an argument is provided, it changes to that directory. If the directory change is successful, it updates the PWD and OLDPWD environment variables.

_myhelp is not yet implemented but is defined to print a message stating that it has not been implemented yet



buitin1.c

This file contains the implementation of several built-in functions for a shell program.

The _myhistory function displays the command history, which is stored in a linked list. It calls the print_list function to print the list.

The unset_alias function removes an alias from the alias list. It searches for an equal sign in the input string to determine the end of the alias name and the beginning of its value. It then calls the delete_node_at_index function to remove the node containing the alias.

The set_alias function sets an alias to a string. It first searches for an equal sign in the input string to determine the end of the alias name and the beginning of its value. If no equal sign is found, it calls unset_alias to remove the alias. If an equal sign is found, it calls unset_alias to remove any existing alias with the same name, then calls add_node_end to add the new alias to the alias list.

The print_alias function prints an alias in the format "alias='value'\n". It first searches for an equal sign to determine the end of the alias name and the beginning of its value. It then prints the alias name, the string "='", the alias value, and the string "'\n".

The _myalias function implements the alias built-in command. If called with no arguments, it prints all the aliases in the alias list. If called with arguments, it sets or prints aliases as appropriate using set_alias and print_alias.

environ.c

This file contains the implementation of several built-in functions related to environment variables: _myenv, _getenv, _mysetenv, _myunsetenv, and populate_env_list.

The _myenv function prints the current environment by calling the print_list_str function, which prints a linked list of strings.

The _getenv function gets the value of an environment variable by searching the linked list of environment variables for a node that starts with the given name. If found, it returns the string after the name, which is the value of the environment variable.

The _mysetenv function sets a new environment variable or modifies an existing one. It checks that the correct number of arguments has been passed and then calls the _setenv function, which adds or modifies a node in the linked list of environment variables.

The _myunsetenv function removes an environment variable. It checks that at least one argument has been passed and then calls the _unsetenv function, which removes the node in the linked list of environment variables that matches the given name.

Finally, the populate_env_list function populates the linked list of environment variables by iterating over the global char** environ variable and adding each string to a new node in the linked list.


  errors.c

These are implementation files for functions related to printing and manipulating the environment in a shell program.

The environ.c file defines four functions:

_myenv: Prints the current environment by calling the print_list_str function with the env member of the info_t structure.
_getenv: Gets the value of an environment variable given its name by iterating over the linked list of environment variables and comparing the name of each variable to the target name. Returns a pointer to the value of the variable if found, or NULL if not found.
_mysetenv: Sets a new environment variable or modifies an existing one. If the number of arguments is not exactly 3, an error message is printed and the function returns 1. Otherwise, the _setenv function is called with the name and value of the variable, and the function returns 0 if successful or 1 if not.
_myunsetenv: Removes one or more environment variables. If the number of arguments is 1, an error message is printed and the function returns 1. Otherwise, the _unsetenv function is called with each argument, and the function returns 0.
The utils.c file defines several utility functions:

_eputs: Prints a string to standard error using _eputchar to print each character.
_eputchar: Writes a character to standard error, using a static buffer to accumulate characters before writing them to the file descriptor. If the character is BUF_FLUSH or the buffer is full, the buffer is written to standard error and the buffer is reset.
_putfd: Writes a character to a given file descriptor, using the same static buffer as _eputchar. If the character is BUF_FLUSH or the buffer is full, the buffer is written to the file descriptor and the buffer is reset.
_putsfd: Prints a string to a given file descriptor by calling _putfd on each character and returning the total number of characters printed.

      errors1.c

This is a C file that contains several functions related to shell functionality. Here's a brief description of each function:

_erratoi - This function converts a string to an integer. If the string contains non-digit characters or the resulting integer is greater than INT_MAX, the function returns -1. Otherwise, it returns the converted integer.
print_error - This function prints an error message to stderr in a specified format. It takes an info_t struct pointer and a string containing the error message type as parameters.
print_d - This function prints an integer to a file descriptor. It takes the integer and file descriptor as parameters and returns the number of characters printed.
convert_number - This function converts a number to a string in the specified base (decimal, hexadecimal, etc.). It takes the number, base, and flags as parameters and returns a pointer to the resulting string.
remove_comments - This function removes the first instance of a # character in a string, replacing it with a null character

      exits.c

These are implementation functions for string manipulation in the shell program.
 _strncpy copies n characters from src to dest. If src is shorter than n, the remaining bytes are filled with null bytes.
 _strncat concatenates n bytes of src to the end of dest. If src is shorter than n, the remaining bytes are filled with null bytes.
 _strchr searches for the first occurrence of c in the string s and returns a pointer to the location of the character if found.
 If c is not found, it returns NULL.

 These functions are commonly used in C programs for string manipulation.

shell_loop.c


This is a C program that implements a shell, a command-line interface used to interact with an operating system. The program is composed of several functions that work together to execute user commands.

The hsh function is the main loop of the shell. It reads input from the user, processes it, and executes commands. The find_builtin function checks if the user command is a built-in shell command, and if it is, it executes the corresponding function. The find_cmd function searches for the user command in the system's PATH environment variable and, if found, executes it by forking a child process. Finally, the fork_cmd function forks a child process to execute the user command using the execve system call.

The program uses several other functions, such as clear_info, get_input, set_info, free_info, and write_history, which are used to manage the shell's state, read input from the user, and free memory.

The program also defines a builtin_table struct that associates built-in shell commands with their corresponding functions. The builtin_table struct is used by the find_builtin function to locate the correct function to execute.

Overall, this program is a simple implementation of a shell that can execute basic commands and built-in shell commands.


      parser.c
This file contains three functions used for parsing commands in the shell: is_cmd(), dup_chars(), and find_path().

The is_cmd() function takes an info_t struct and a string path as arguments. It uses the stat() function to check if path points to a regular file. If so, it returns 1, indicating that the file is an executable command. Otherwise, it returns 0.

The dup_chars() function takes a string pathstr and two integers start and stop as arguments. It creates a new static buffer and copies the characters of pathstr from index start to index stop, excluding any colons. The buffer is terminated with a null byte and a pointer to the buffer is returned.

The find_path() function takes an info_t struct, a string pathstr, and a string cmd as arguments. It checks if cmd starts with "./", indicating that it is a relative path, and if so, it checks if the file exists and is a regular file using is_cmd(). If it is, it returns the path to the file.

Otherwise, it loops through the pathstr string, using dup_chars() to extract each path from the PATH environment variable. It then concatenates the path with the cmd argument to form a potential path to the command. If the resulting path points to a regular file, it is returned. If none of the paths lead to a regular file, NULL is returned.
