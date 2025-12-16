# Bash Backticks vs Dollar Parentheses $()

There are two forms of command substitution which you can use in bash. One is with dollar-parentheses and the other is using backticks. The command enclosed by $() syntax will not work with the old bourne shell. The original Bourne shell only used to support backticks. However, all shells now support backticks as well as dollar-parentheses.

## Bash backticks
Backticks, also referred to as the back quote (`) character, allows you to store the output of a command in a variable. With backticks you can run the command in the system and assign the output to continue the logic. Backticks act as a bridge between two commands, which means that the second command’s action depends upon the first one.

Many feel that the backtick operators have been deprecated. However, this is not true. The backtick operator is available in bash, and many coders use it. It can get complicated if backticks are nested where the internal commands also make use of the backticks. 

Let’s look at the following example:

```
#!/bin/bash
list=`ls`
count=`ls -1 | wc -l` 
dateToday=`date`
echo [$dateToday] has $count entries and they are: $list
echo [`date`] also has `ls -1 | wc -l` entries and they are: `ls`
 
sum=`expr 5 + 2`
echo Sum is $sum
```
In this example, we are declaring variables and assigning the output of each of those commands to a variable. We can also use the results of the commands surrounded by backticks in other commands as shown above.

<img width="1226" height="648" alt="image" src="https://github.com/user-attachments/assets/1e3c7580-4948-4c3a-a083-91ca5fac2276" />

## Dollar Parentheses $()

The dollar-parentheses is a popular command substitution and applies to all POSIX-conformant shells. The command in the braces of $() is executed in a subshell and the output is then placed in the original command.

```
#!/bin/bash
list=$(ls)
count=$(ls -1 | wc -l)
dateToday=(date)
echo [$dateToday] has $count entries and they are: $list
echo [$(date)] also has $(ls -1 | wc -l) entries and they are: $(ls)
 
sum=$((5+2))
echo Sum is $sum
echo sum+count is $(($sum+$count))
```
As we can see above, variables are getting assigned the values on the basis of the output of the respective commands. These variables can be processed as per our needs. The result of $() can also be directly used in other commands 
<img width="1198" height="341" alt="image" src="https://github.com/user-attachments/assets/66594a0f-6a46-4eca-b93e-e81f534d38e3" />

## Backticks vs Dollar Parentheses $()
Backticks ( ` ) have a visual disadvantage as they can be easily confused by single quotes (‘). With newer shells, both backticks and dollar-parentheses are equivalent. Within backticks the backslash quotes are evaluated before other kinds of internal quotes are applied. $() operators are much more convenient to use when you need to nest multiple commands. The piece of code inside the $ parentheses operator is considered as a bash command. 

```
#!/bin/bash
path=/world/country/asia/japan/tokyo
 
echo "-----With dollar parentheses-----" 
echo $(basename $(dirname $(dirname $path)))
 
 
echo "-----With backticks-----" 
echo `basename \`dirname \\\`dirname $path \\\`\``
```
As you can see, both backticks and dollar parentheses operator display the same output. However, with the amount of escaping needed with backticks, it makes the task challenging and confusing. Nesting backtick operators inside other backtick operators require escaping and work if the nested back quotes are escaped. On the contrary, the dollar parentheses operator is readable as well as understandable.
<img width="461" height="138" alt="image" src="https://github.com/user-attachments/assets/bd4f9b45-cab4-4c70-823f-636473d5002a" />

## Conclusion
- Both backticks and dollar-parentheses operators are equivalent and referred to as command substitution operators.
- Dollar-parentheses operators are convenient to use.
- Nesting backtick operators inside other backtick operators require escaping, making it visually confusing.
