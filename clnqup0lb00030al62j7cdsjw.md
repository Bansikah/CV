---
title: "Bash Basics"
datePublished: Sun Oct 15 2023 02:31:55 GMT+0000 (Coordinated Universal Time)
cuid: clnqup0lb00030al62j7cdsjw
slug: bash-basics
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697614054300/0b36b115-dd8d-4bd7-92b8-4a559f014251.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1697614091814/4207c62c-3e5c-4ba7-9313-ecd3e0cf4da7.png
tags: bash, shell, linux-for-beginners, bash-shell-script

---

Bash (short for "Bourne Again SHell") is a command language interpreter that is widely used in Unix-like operating systems. It is the default shell for most Linux distributions and macOS. Bash allows users to interact with their computer by executing commands and scripts. It provides a set of built-in commands and utilities for tasks such as file manipulation, text processing, and system administration. Bash scripts can automate repetitive tasks and can be used for various purposes, including system administration, software development, and data processing.

In Bash code, `#!/bin/bash` is called a shebang or hashbang. It is a special comment that specifies the interpreter or shell to be used to execute the script.

The shebang `#!/bin/bash` specifically indicates that the script should be interpreted and executed by the Bash shell. By including this line at the beginning of a Bash script, you ensure that the script is executed with the correct interpreter, regardless of the default shell set on the system.

The `#!/bin/bash` shebang is commonly used in Linux and macOS systems where Bash is the default shell. It is necessary to include this shebang line for the script to be executed properly as a Bash script.

Including the shebang `#!/bin/bash` at the beginning of a Bash script ensures that the script is interpreted correctly and avoids any compatibility issues with different shell environments.

### Hello world!

```bash
#!/bin/bash
echo "Hello world"
```

### Variables in bash

**Variables in bash referenced and manipulated throughout a script. They are created by assigning a value to a name, and the convention is to use uppercase letters. Variables can store numbers, letters, and other characters. To access the value of a variable, you use the syntax** `$variable_name`**. For example:**

```bash
#!/bin/bash
NAME="John"
echo "My name is ${NAME}"
```

In this example, the variable **NAME** is assigned the value **"John",** and the value is then printed using the echo command.

### USER INPUT IN BASH

To capture user input in a Bash script, you can use the `read` command. Here's an example:

```bash
#!/bin/bash
read -p "Enter your name: " NAME
echo "Hello $NAME, nice to meet you!"
```

In this example, the `-p` option is used to display a prompt to the user. The user's input is then stored in the `NAME` variable, which can be used later in the script.#

### CONDITIONALS: SIMPLE IF STATEMENTS

```bash
#!/bin/bash
if [ "$NAME" == "Noel" ]
then
    echo "your name is Noel"
```

### IF-ELSE CONDITIONS

```bash
#!/bin/bash
if [ "$NAME" == "Noel" ]
then
    echo "your name is Noel"
else
    echo "your name is not Noel"
fi
```

### ELSE-IF CONDITIONS (elif)

```bash
#!/bin/bash
if [ "$NAME" == "Noel" ]
then
    echo "your name is Noel"
elif [ "$NAME" == "John" ]
then
    echo "Your name is John"
else
    echo "your name is not Noel"
fi
```

### COMPARISON

```bash
#!/bin/bash
NUM1=3
NUM2=5
if [ "$NUM1" -gt "$NUM2" ]
then
    echo " $NUM1 is greater than $NUM2"
else
    echo " $NUM1 is less than $NUM2"
fi
```

### COMPARISON VALUES

```plaintext
 value1 -eq value2 : return if value1 is equal to value2
 value1 -ne value2 : return if value1 is not equal to value2 
 value1 -gt value2 : return if value1 is greater than value2 
 value1 -ge value2 : return if value1 is greater than or equal to value2 
 value1 -lt value2 : return if value1 is less than value2
 value1 -le value2 : return if value1 is less than or equal to value2
```

### FILE CONDITIONS

```bash
#!/bin/bash
FILE="test.txt"
if [ -f "$FILE" ]; then
   echo "$FILE is a file"
else
   echo "$FILE is NOT a file"
fi
```

```plaintext
############
# -d file True if file is a directory
# -e file True if file exists( -f is generally used)
# -f file True if file provided string is a file
# -g file True if the group id is set on a file
# -r file True if the file is reachable
# -s file True if the file has none-zero size
# -u file True if the file user id is set on a file
# -w file True if the file is writable
# -x file Treu if the file is executable
############
```

### CASE STATEMENTS

```bash
#!/bin/bash
read -p "Are your 21 years old or not Y/N?: " ANSWER
case "$ANSWER" in
   [yY] | [yY][eE][sS])
    echo "You can take a beer :)"
    ;;
   [nN] | [nN][oO])
    echo "Sorry no drinking"
    ;;
   *)
   echo "Enter yes [yY] or No [nN]"
esac
```

### SIMPLE FOR LOOP

```bash
#!/bin/bash
NAMES="Noel Hans John James"
for NAME in $NAMES
  do
  echo "Hello, $NAME"
done
```

### FOR LOOP FOR RENAMING FILES

```bash
#!/bin/bash
FILES="ls *.txt"
NEW=new
for FILE in $FILES
  do
    echo "Renaming $FILE to new-$FILE"
    mv $FILE $NEW-$FILE
done
```

### WHILE LOOPS

```bash
#!/bin/bash
LINE=1
while read -r CURRENT_LINE
    do
      echo "$LINE: $CURRENT_LINE"
      ((LINE++))
done < "./new-1.txt"
```

### FUNCTIONS

In Bash, functions are blocks of reusable code that can be defined once and called multiple times within a script. They allow you to organize and modularize your code, making it easier to understand and maintain.

To define a function in Bash, you can use the `function` keyword followed by the function name and a set of parentheses, like this:

```bash
function sayHello() {
    echo "Hello, world!"
}
```

You can then call the function by simply using its name followed by parentheses:

```bash
sayHello
```

Functions can also accept parameters, which are variables that hold values passed to the function when it is called. You can define parameters inside the parentheses after the function name:

```bash
function greet() {
    echo "Hello, $1! You are $2 years old."
}
```

In this example, `$1` and `$2` refer to the first and second parameters passed to the function `greet`.

When calling a function with parameters, you can provide the values for the parameters inside the parentheses:

```bash
greet "Noel" 20
```

This will output: `Hello, Noel! You are 20 years old.`

Functions in Bash are useful for encapsulating a set of related commands, improving code reusability, and making scripts more modular and maintainable.

```bash
#!/bin/bash
function sayHello(){
    echo "Hello how are you doing"
}
sayHello
```

### FUNCTIONS WITH PARAMETERS

```bash
#!/bin/bash
function greet(){
    echo "Hello i am $1, and I am $2"
}
greet "Noel" 20
```

### CREATE FOLDER AND WRITE TO A FILE

```bash
#!/bin/bash
mkdir hello
touch "hello/world.txt"
echo "I am writing to this file" > "hello/world.txt"
echo "I create a file called world.txt"
```

### REGULAR EXPRESSIONS IN BASH

Regular expressions, often abbreviated as regex, are powerful patterns used for pattern matching and text manipulation in various programming languages, including Bash. In Bash, regular expressions are commonly used for tasks such as pattern matching, string validation, and text search and replace.

```bash
read -p "Enter Email:" email
if [[ "$email" =~ ^[A-Za-z0-9]+@[A-Za-z0-9]+\\.[A-Za-z] ]]
then
   echo "Email is ok"
else
    echo "Email is not ok"
fi
```

In this example, the regular expression pattern `^[A-Za-z0-9]+@[A-Za-z0-9]+\\\\.[A-Za-z]` is used to validate an email address. The `^` symbol denotes the start of the line, `[A-Za-z0-9]+` matches one or more alphanumeric characters, `@` matches the `@` symbol, `[A-Za-z0-9]+` matches one or more alphanumeric characters again, `\\\\.` matches the `.` symbol (escaped with `\\\\`), and `[A-Za-z]` matches a single alphabetic character. If the email entered by the user matches the regular expression pattern, the script outputs "Email is ok"; otherwise, it outputs "Email is not ok".

Regular expressions provide a powerful and flexible way to work with text patterns in Bash, allowing you to perform complex string matching and manipulation tasks.

### CONCLUSION

In conclusion, bash scripting is a powerful tool for automating tasks and streamlining workflows in a Linux environment. By learning the basics of bash scripting, you can harness the full potential of the command line and improve your productivity as a developer or system administrator.

Throughout this article, we covered essential concepts such as variables, conditionals, loops, and functions. We explored how to handle user input, manipulate strings, and perform file operations. Additionally, we discussed error handling and debugging techniques to ensure the robustness of your scripts.

Remember, practice is key to mastering bash scripting. Experiment with different scenarios and gradually build more complex scripts. Familiarize yourself with the vast array of available commands and utilities to expand your scripting capabilities.

By becoming proficient in bash scripting, you will have the ability to automate repetitive tasks, create custom tools, and enhance your overall efficiency in the command line environment. So, dive in, explore, and unleash the power of bash scripting in your daily workflow.