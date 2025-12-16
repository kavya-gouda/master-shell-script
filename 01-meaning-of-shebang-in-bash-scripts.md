# Meaning of Shebang in Bash Scripts
When writing shell scripts, the first line we often encounter is a hash (#), followed by an exclamation mark (!) with some path. The hash and the exclamation mark together is known as the shebang. This is an important aspect during the development and execution of the script. 

## What is Shebang?
Shebang is a sequence of characters that passes instructions and informs the kernel about the interpreter that should be used to run the commands present in our script file. To execute our script in a specific shell, provided that shell is supported by our system, we must begin are scripts with a #!. This was created because the users wanted to run the script which were not compiled, and hence, technically non-executables. 

Example:
```
#!/bin/bash
```
This indicates that the interpreter must be a Bash shell.

## What happens if we don’t have Shebang?

We have plenty of shells available for Linux systems which differ slightly in their syntaxes and interpretation. However, they mostly have a similar syntax. Let us take an example and write a script without a shebang.

Example:

```
echo "Good day"
```
We will open a terminal, give this script execute permissions and run it with the "." operator.
<img width="857" height="293" alt="image" src="https://github.com/user-attachments/assets/9c90d2e0-7227-454e-94cf-e589ecb855fe" />

As we can see, the script is working without any shebang. This means this script uses the default shell to execute. We can check our default shell using the command:

```
echo $0.
```
<img width="679" height="189" alt="image" src="https://github.com/user-attachments/assets/37da36d9-96ae-4393-b81d-5a5b09ff4b34" />

Now we will take another example and write a script to check if the input is a number or not. Let’s save the below script named "isNumeric" and give it executable permissions.

```
#!/bin/bash
numericCheck()
{
        if ! [[ "$1" =~ ^[0-9]+(\.[0-9]+)?$ ]]
        then
         echo $1 is non numeric.
        fi
}
numericCheck 5
numericCheck A
```
Now we run the script as follows:
```
./isNumeric
```
<img width="863" height="691" alt="image" src="https://github.com/user-attachments/assets/a68936b7-6a71-4f97-a017-4dafbfcda927" />

The script is working as expected. Let us change the first line of the same script to #!/bin/ksh and rerun it.

<img width="882" height="549" alt="image" src="https://github.com/user-attachments/assets/c219dcca-5f10-47a9-be1c-e46a489846c9" />

We can notice that when there is a syntax error with an unexpected operator/operand '=~' as the KSH (Korn SHell) interpreter doesn’t recognize that. Hence, it is always suggested to mention the correct interpreter in the script. If not, some scripts may end up giving unexpected results when executed in different shells.

## How does Shebang work?

Shebang is simply the absolute path to the Bash interpreter. Almost every bash script will have #!/bin/bash as their first line. This ensures that Bash will be employed for the interpretation of the script, even if it is executed under a different shell.

When we run an executable file, the "execve" program gets called to replace the current process with a new one. Say we try to run a text file, the execve program will look for the first two characters to be present in the file to be "#!" followed by the absolute path of the interpreter.

If the text file has had its executable bit set, and the Shebang is followed by a valid command interpreter, Linux passes the script to the interpreter which will be reading the rest of the script and processing it accordingly.We can see the working of the shebang as using the trace command as follows:

```
strace bash -c './scriptname'
```
<img width="879" height="859" alt="image" src="https://github.com/user-attachments/assets/1274414c-0e1b-4782-9bc4-16629edb846f" />

Syntax
```
#!/path/to/interpreter [arguments]
```
## Bash shebang options
Let’s assume we have a script script1, beginning with #!/bin/bash and we run the script as follows:

```
script1 arg1 arg2 
```

This is equivalent to executing 
```
/bin/bash script1 arg1 arg2.
```

Similarly, if we have specified the shebang line with arguments say, #!/bin/bash -ex, this is equivalent to executing 

```
/bin/bash -ex script1 arg1 arg2.
```

Here, we have made use of the commonly used arguments e and x. This is just adding shell options to the shebang:

- -e tells us that if there is any command that is returning a non-zero status, the script will terminate immediately. This appears a good idea, but it acts inconsistently and has very complex rules to abort. 
- -x makes the shell display the execution trace. It prints the commands and their arguments as they get called for execution.
- -v displays the shell input lines as it reads the file.


It is not a good practice to set the shell options in the shebang as they will not be playing any role if the script is invoked directly with the command:

```
bash <scriptName>
```

## Types of Shebang

#!/bin/bash - It is the common shebang line present in every script. It informs the kernel to use the Bash interpreter present in the /bin directory. If no shebang line is provided, this is the default one.


#!/usr/bin/env bash - The shell might be present in different locations in different Linux distros. As we are using Ubuntu, we can see, in our examples, that bash is present in the /usr/bin/ directory. Some users also tend to customize their shells in different locations. The "env" command enables us to run our piece of code in any environment. It tries to find bash in the environment variable PATH. The moment there is a match, it stops the search and runs with that match. Here is an example of how we can use it:

Some commonly used interpreters are:

- #!/bin/sh - We can execute the file using the Bourne or any compatible shell with the help of this interpreter.
- #!/bin/bash - The presence of this Shebang line enables us to execute the file using the Bash shell.
- #!/usr/bin/pwsh - This ensures that our script executes the file using PowerShell.
- #!/usr/bin/env python3 - We look for the python interpreter in the path variable and then execute our script with it.
- #!/usr/bin/python3 - This ensures our files execute as python scripts.
- #!/bin/false - We get a non-zero exit status,indicating failure, when employing this interpreter. 
- #!/bin/perl - It executes our files as if they are perl scripts.
- #!/usr/bin/env perl - It executes our files as perl scripts using the env.

We can either specify the full path of the interpreter or use the env command in our shebang line. Shebang lines may include specific options that are passed to the interpreter. However, implementations vary in the parsing behavior of the options.

## Importance of Shebang

Since there are lots of shells available, we have seen what happens if we do not specify the shebang. Shebang makes shell scripts behave like actual executable files.It allows the other available interpreters to fit in seamlessly.

As a result, we don't need to mention anything. We just need to use the dot (.) operator with the filename and run it on the terminal. The shebang mentioned on the first line will be picked and it will make the script file executable

## When can we ignore Shebang?

If we do not specify an interpreter line, the default is usually the /bin/sh. But, it is always recommended that we set #!/bin/bash line for our scripts. Shebang can be overlooked if we explicitly specify the shell. Overriding the Shebang is also possible at the command line. 
Say, our script has the Shebang #!/bin/ksh. We can override to run as bash.

Example:

```
bash <script-name>
```
<img width="872" height="785" alt="image" src="https://github.com/user-attachments/assets/4f180913-d350-4099-a011-6cbe435eebce" />

As we have seen earlier, we should avoid the override of the shebang line. This ensures we get a highly consistent output.

# Conclusion
- Shebang should be our first line in the script.
- Shebang has the absolute path of the interpreter.
- It determines how a script executes.
- We can override the shebang line but it is not a good practice.

