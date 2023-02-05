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
            Time for <a href="https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-hijacking">sudo hijacking</a>.
        </li>
    </ul>
</h5>