# How to Make Bash Script Executable Using Chmod

In this tutorial, I am going through the steps to create a bash script and make the script executable using the chmod command. After that, you will be able to run it without using the sh or bash commands.

## Step 1: Creating a Bash File

The first step is to create a new text file with .sh extension using the following command.
```
touch hello_script.sh
```
## Step 2: Writing a Sample Script
Open the newly created file using any of your favorite editors to add the following bash script to the file.
```
$ vim hello_script.sh

#!/bin/bash
echo "Hello World"
```
Save and close the file using ESC +:wq!
## Step 3: Executing the Bash Script

There are two ways to run the bash file. The first one is by using the bash command and the other is by setting the execute permission to bash file.

Let’s run the following command to execute the bash script using bash or sh command.
```
bash hello_script.sh
or 
sh hello_script.sh
```
<img width="873" height="134" alt="image" src="https://github.com/user-attachments/assets/14cbecd8-d2f3-4edb-acec-fbb4a29863f1" />

## Step 4: Set Executable Permissions to Script

The second way to execute a bash script is by setting up the executable permissions.

To make a script executable for the owner of the file, use u+x filename.

```
chmod u+x hello_script.sh
```

To make the file executable for all users use +x filename or a+x filename.

```
chmod +x hello_script.sh
```
## Step 5: Running Executable Script
After you have assigned the executable permissions to the script, you can run the script without bash command as shown.
```
./hello_script.sh
```

<img width="868" height="244" alt="image" src="https://github.com/user-attachments/assets/8243de48-e5d0-4bc3-97bd-6352cb6c9064" />

### Another Example

In the following example, I am going to write and execute a bash script to take a backup from source to destination.

```
$ vim backup_script.sh

#!/bin/bash
TIME=`date +%b-%d-%y`
DESTINATION=/home/ubuntu/backup-$BACKUPTIME.tar.gz
SOURCE=/data_folder
tar -cpzf $DESTINATION $SOURCE
```

Save and close the file using :wq! and give it the executable permissions for all users using the following command:
```
chmod +x backup_script.sh
```
Now run the script:
```
./backup_script
```
<img width="866" height="249" alt="image" src="https://github.com/user-attachments/assets/9a3df0f7-546a-4d58-8d16-ef0f2151e9d9" />

## Conclusion

At the end of this tutorial, you should be familiar with how to set a script executable in Linux.

I hope you enjoyed reading it, please leave your suggestion in the below command section.

