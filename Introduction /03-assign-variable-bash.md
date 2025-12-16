# How to Assign Variable in Bash
A variable is a named storage location in a program's memory where a value can be stored, retrieved, and manipulated. Like any programming language, Variables are an essential component in the Bash scripts. They allow you to create dynamic scripts that can change based on the data that is passed to them.

In Bash, there are different ways to assign variables which will be covered in detail.
## Local vs Global variable assignment
Bash has two types of variables - local, and global based on the scope where they are defined in the script.

### Local variable
A local variable is a variable that is defined within a function or a block of code and can only be accessed within that function or block. Local variables are only accessible within the function or block in which they are defined and the value of the variable is lost once the function or the block ends.

### Global variable
A global variable, on the other hand, is a variable that is defined outside of any function or block and can be accessed from any part of the program. Global variables are accessible from anywhere in the program, including from within functions and blocks.

See the following script to understand the scope and lifetime of local vs global variables:

```
#!/bin/bash
 
num=2
function demo_local_var() {
       local num=1
       echo "This is the local variable: $num"
}
 
echo "Global num before function: $num"
demo_local_var
echo "Global num after function: $num"
```
In the script:

- num=2 initializes the global num variable.
- local num=1 declared inside the function demo_local_var block initializes the local num variable whose scope is within the function only
- Outside this function, echoing $num always prints the value of global num variable.
<img width="850" height="140" alt="image" src="https://github.com/user-attachments/assets/c84dcd12-d40b-492f-9e63-ccf04bc7f1eb" />

## Single variable assignment

In bash, a single variable can be assigned simply using the syntax

```
var_name=<value>
```
with no space before and after the `=` sign. You do not need to declare the data type in bash while assigning a variable.

## Integer assignment
To assign an integer to a variable, you can use the following syntax:
```
#!/bin/bash
 
num=1
echo $num
```

In the script, num=1 assigns a global integer variable value 1.
<img width="863" height="91" alt="image" src="https://github.com/user-attachments/assets/71435cff-712d-42aa-b712-fb30e06fd791" />

## String assignment

There are multiple ways to assign strings:
- Single words can be assigned directly without any quotes.
- Multi-word strings can be defined using Single quotes (') and Double quotes (").
- However, there is a difference between how Bash interprets single quotes and double quotes.

When you use single quotes to define a string, it preserves the literal value of each character. On the other hand, if you use double quotes, it recognizes the special symbols ($, `, \) and expands the strings using the shell expansion rules.

```
#!/bin/bash
name=world
greeting2='Hello $name'
greeting3="Hello $name"
 
echo $name
echo $greeting2
echo $greeting3
```
In this example,

- greeting2 treats $name as a string and thus it gets expanded to Hello $name.
- While greeting3 expands $name to world, thus generating the string - Hello world.

<img width="820" height="136" alt="image" src="https://github.com/user-attachments/assets/92d41ca4-1cc4-42b7-bb89-2efbf3afa255" />

## Boolean assignment
To assign a boolean value to a variable, you can use the following syntax:
```
#!/bin/bash
 
true_val=true
false_val=false
 
if [[ "$true_val" == true ]]; then
       echo "true_val: true"
fi
 
if [[ "$false_val" == true ]]; then
       echo "false_val: true"
fi
```
In the script:

true_val=true and false_val=false initializes the boolean variables.
We can use these booleans in conditional statements to make decisions.

## Multi-variable assignments

Bash provides a straightforward syntax for assigning multiple variables in a single line as follows:

```
#!/bin/bash
 
a=1 b=2 c=3
echo "a: $a"
echo "b: $b"
echo "c: $c"
```
In the above script, a=1, b=2, c=3 initializes three integer variables using a single statement.

## Default value assignment

Bash has a built-in syntax for providing default values to the variables:-
```
newVar=${var:-defaultval}
```
If var is not defined, it assigns the defaultval to the newVar.
See the following script to see how default assignments work:

```
#!/bin/bash
 
var1=5
 
## first example
userOutput1="${var1:-var1 is not defined}"
echo $userOutput1
 
## second example
userOutput2="${var2:-var2 is not defined}"
echo $userOutput2
```

In script:
- in the first example, echo $userOutput1 prints 5 to the stdout since var1 is defined.
- In the second example, echo $userOutput2 prints var2 is not defined since var2 is not defined before.

<img width="867" height="146" alt="image" src="https://github.com/user-attachments/assets/c0373a92-fba8-496b-ba8a-9ec759e3ca1d" />

## Using let command for assignments

The let command is used to assign numeric values to the variables and perform arithmetic, bitwise, and logical operations.
Consider the following script:

```
#/bin/bash
 
## Numeric assignment
let "num1 = 1"
echo "num1: $num1"
 
## Addition
let "num1 = 1" "num2 = num1 + 2"
echo "$num1 + 2 = $num2"
 
## Subtraction
let "num1 = 3" "num2 = num1 - 2"
echo "$num1 - 2 = $num2"
 
## Multiplication
let "num1 = 2" "num2 = num1 * 2"
echo "$num1*2 = $num2"
 
## Division
let "num1 = 4" "num2 = num1 / 2"
echo "$num1 / 2 = $num2"
 
## Modulus
let "num1 = 4" "num2 = num1 % 2"
echo "$num1 % 2 = $num2"
 
## Exponentiation
let "num1 = 4" "num2 = num1 ** 2"
echo "$num1 ** 2 = $num2"
 
## Unary post increment
let "num1 = 4" "num2 = num1++"
echo "$num1 after unary post increment = $num2"
 
## Unary pre increment
let "num1 = 4" "num2 = ++num1"
echo "$num1 after unary pre increment = $num2"
 
## Left shift
let "num1 = 4" "num2 = num1 << 1"
echo "$num1 << 1 = $num2"
 
## Right shift
let "num1 = 4" "num2 = num1 >> 1"
echo "$num1 >> 1 = $num2"
 
## Bitwise Negation
let "num1 = 4" "num2 = ~num1"
echo "~$num1 = $num2"
 
## Bitwise AND
let "num1 = 6" "num2 = num1 & 2"
echo "$num1 & 2 = $num2"
 
## Bitwise OR
let "num1 = 4" "num2 = num1 | 1"
echo "$num1 | 2 = $num2"
 
## Bitwise XOR
let "num1 = 4" "num2 = num1 ^ 2"
echo "$num1 ^ 2 = $num2"
```
let command is an important utility which provides a simplistic syntax to perform a variety of arithmetic, logical and bitwise operations.

## Using Read command

Bash has a built-in read command that can read a line from the standard input (stdin) and split the line into multiple variables.

See the following script to understand how the read command works:

```
echo "Enter the animal name and its color"
read animal color
echo "animal: $animal, color: $color"
```

In the script read animal color accepts 2 inputs from the user and stores them in the variables animal and color.

Read command also comes with some useful options:
- Prompt: Prompt flag (-p) helps to provide a useful text to the user and accept inputs. This removes the additional need for echo statements simplifying the code.
- Silent: Silent flag (-s) helps the user to hide the input from display. This is useful when entering sensitive information such as passwords.
- Input to array: Array (-a) flag reads the input to an array instead of individual words

```
#!/bin/bash
 
read -p "Enter the username: " username
read -s -p "Enter the password: " password
echo
read -p "Enter your hobbies(space separated): " -a hobbies
 
echo "$username logged in"
echo "Your hobbies are:-  "
 
for hobby in ${hobbies[@]}; do
       echo $hobby
done
```
In the script:

- read -p “Enter the username: “  prints the text “Enter the username: “ and also accepts an input from the user.
- read -s -p “Enter the password: “  accepts an input from the user in silent mode, i.e. it is not displayed on the screen.
- read -p “Enter your hobbies(space separated): “ -a hobbies accepts an array input from the user into hobbies variable. The variable can then be iterated over using the array iteration syntax.

## Conclusion
- Bash supports both local and global variables. Using global variables, in general should be avoided since they increase the complexity of the code and may introduce hard to debug bugs.
- Bash provides built-in support for assigning integer, strings and boolean type variables. Data type is not required while assigning variables.
- Multiple variables can be assigned simply by defining multiple variables in a single line.
- Bash also supports initializing variables with default values. This is a good programming practice and helps to avoid bugs due to uninitialized variables.
- The let command is a useful built-in in bash for working with numerics and performing a variety of operations.
- The read command is another important built-in to read input from the command line and create interactive applications.



  
