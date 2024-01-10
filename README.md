![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/ea9009f5-736b-404b-ad10-f870455b4346)# Task_-Level1-Linux-Module

Section A
1.	I want a manual page of command so that I can see the full documentation of the command.

Man page for the command

man internctl
Code:-
![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/16bc056b-044c-4056-9c9c-4022d82a3029)

 
















Output: -

 ![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/a6176c97-4def-442b-a3ce-013f1d23c92e)

 

2.	Each linux command has an option --help which helps the end user to understand the use cases via examples. Similarly if I execute internsctl --help it should provide me the necessary help.


3.	I want to see version of my command by executing

internsctl –version

File internsctl --version code
echo "v0.1.0"

Output:

![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/355e8ee1-4750-4994-896f-2331456134fe)

 



 
Section B

Part1:

1.	I want to get cpu information of my server through the following command: Internsctl cpu getinfo:
![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/8bd841e9-8947-4652-aa08-0848349311cf)

 
 
2. I want to get memory information of my server through the following command: 

$Internsctl memory getinfo:
 File internsctl memory getinfo: 
Code:
 ![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/0bf3ff0a-c6fe-422f-82dd-91b717137a6c)

 


Part2
1.	I want to create a new user on my server through the following command:

$ internsctl user create <username>

File internsctl user create

 

Code
![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/436d3113-d275-4145-97b1-f5895460e3f0)

#! /bin/bash

if id "$1" &>/dev/null; then
echo "User $1 already exists."
echo "please chose another username." exit

 
else
 

read -p "password " pswd
useradd -p "$pswd" -d /home/"$1" -m -g users -s /bin/bash "$1" echo "$1 added"
fi
 






1.	I want to list all the regular users present on my server through the following command:

$ internsctl user list

#! /bin/bash cat /etc/passwd

  ![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/c7cc8883-61c4-47aa-96be-9e3e33dfd56a)




2.	If want to list all the users with sudo permissions on my server through the following command:

$ internsctl user list --sudo-only

 ![image](https://github.com/Gulchetan/Task_-Level1-Linux-Module/assets/91937485/b949b9ae-a98a-43ea-be23-96b6bfac3e45)


File internsctl user list --sudo-only Code
#!/bin/sh

getent group sudo
 
Part3
By executing below command I want to get some information about a file

$ internsctl file getinfo <file-name>

Expected Output
xenonstack@xsd-034:~$ internsctl file getinfo hello.txt File:	hellot.txt
Access:	-rw-r--r--
Size(B):	5448
Owner:	xenonstack
Modify:	2020-10-07 20:34:44.616123431 +0530.


Code:
#! /bin/bash
if [[ "$#" -eq 1 ]]; then
ls -l $1
elif [[ "$#" -eq 2 ]]; then
if [ "$1" == "-s" ] || [ "$1" == "--size" ] then
wc -c $2
elif [ "$1" == "-p" ] || [ "$1" == "--permissions" ] then
ls -ld $2 |awk '{ print $1; }'
elif [ "$1" == "o" ] || [ "$1" == "--owner" ] then
stat -c '%U' $2
elif [ "$1" == "m" ] || [ "$1" == "--last-modified" ] then
stat -c ‘%y’ $2
fi
fi


