# suidscript
Here is a demo why suid-bits are unavailable for executable scripts.
There are a number of scripts in the repository to demonstrate the possible atack.

In OS suid-bits have no effect for executable scripts for security reason.
But what if there was an effect?

Let's imagine you are a hacker and you have found some suid-script (**script.sh**) with root owner.
Then you can write some malicious script using the same script language as the **script.sh**. Let it will be **hack.sh**.
To run **hack.sh** script with root privilege you can create **attack.sh** script where you create a symlink which follows to **script.sh** first (to get root privilege) and after running script via symlink you redirect the symlink to you **hack.sh** script.
If run **attack.sh** script several times you can catch a case when the symlink will be redirected before the interpreter (Bash our case) will start.
Then **hack.sh** script will run with root privilege. To catch this case you can run **attack.sh** in the loop and **repeat-attack.sh** script could help with this.

The output for the **repeat-attack.sh** will be something like following:
```
$ ./repeat-attack.sh 
hack
hack
hack
hack
hack
asd
hack
hack
hack
asd
hack
```

And it means we can run **hack.sh**. If the executing script were affected by suid-bits, the **hack.sh** script would be run as root.
