<h1>TryHackME - Eavesdropper</h1>
<img src="./img/logo.png" alt="logo" width="500">
<h4>
    There are two ways to solve this machine.
    <ol>
        <li>Intended Way</li>
        <li>Unintended Way</li>
    </ol>
</h4>
<h4>
    You can follow the steps below to solve it using the intended way or you can check out another writeup by
    <code>xyro</code> who found an unintended way to solve this machine which is something very few people would have
    found and his approach to solve this machine is also unique. Link to his write is here => <a
        href="http://xyro.codes/THM/eavesdropper/writeup.html">xyro's writeup</a>
</h4>

<h5>
    <strong>Intended way :</strong>
    <ul>
        <li>
            <strong>Step 1 :</strong><br>
            Log in to machine using the <code>idrsa.id-rsa</code> provided in task 1 with username <code> frank </code>.
        </li>
        <li>
            <strong>Step 2 :</strong><br>
            Transfer <code>pspy</code> onto the target machine and run it for a while. You will find an intresting
            command being executed. <code>sudo cat /etc/shadow</code>
        </li>
        <li>
            <strong>Step 3 :</strong><br>
            Time for <a href="https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-hijacking">sudo
                hijacking</a>.
            While creating our sudo executable, we have to be a little bit creative. Trying to get a reverse shell won't
            work and even if it did, the command is using <code> sudo </code> which is not required by the root user so
            the user executing that command does not have sudo privilege and you will get the same low privilege user
            shell and for the same reason, anything that requires sudo privilege wont work like reading or editing
            shadow file. So, what we can do here is to catch the password from the user after he runs the
            <code>sudo cat /etc/shadow</code> command. Follow these steps to capture the password.
            <ol>
                <li>
                    <code>touch /tmp/sudo</code> creating our own sudo executable.
                </li>
                <li>content of sudo file <br>
                    <code>#!/bin/bash</code> -- I don't think i need to explain this. <br>
                    <code>read -s password</code> -- after executes the command, this will read the password and store it in the password variable. <code>-s</code> is used so that the input is not displayed. Something i'm used to do.<br>
                    <code>echo $password > /home/frank/pass.txt</code> -- echoing the password from password variable to pass.txt so that we can read it. <br>
                </li>
            </ol>
        </li>
    </ul>
</h5>