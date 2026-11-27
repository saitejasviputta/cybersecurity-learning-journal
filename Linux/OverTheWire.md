## OverTheWire - Bandit

This consists detailed steps to navigate through Bandit Wargames by OverTheWire. It does not consists direct answers but rather simple personal steps to cross each level.

# Introduction

To start these level, we need to use the following command to enter any required level.

```bash
ssh banditX@bandit.labs.overthewire.org -p 2220
```

Here the 'X' before @ needs to be replaced by neccesary level number.

ssh - to connect using secure shell
-p 2220 - Port number

# Level 0

enter using the following code.

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

Now, the password for this level is given by the official page. 

after finishing a level by finding required password, use 

```bash
exit
```

to exit the current level before entering the next one.

# Level 0 -> Level 1

To find required password for next level, it is stored in "readme" in the home directory.

Use
```bash
ls ~
```
To get the list of files in the home directory. The to read the required file, use

```bash
cat readme
```

Store the password somewhere before exiting the current level.

# Level 1 -> Level 2

To find required password for next level, it is stored in "-" in the home directory.

Use
```bash
ls ~
```
To get the list of files in the home directory. The to read the required file, use
```bash
cat < -
```

"<" is input redirection. 
Why '<' is necessary?
Because if we don't use this, it will expect a command after the '-'. (like -p or -r)

# Level 2 -> Level 3

To find required password for next level, it is stored in "--spaces in filename--" in the home directory.

Use
```bash
ls ~
```
To get the list of files in the home directory. The to read the required file, use
```bash
cat -- "--spaces in filename--"
```

Here '--' is called deliminator. It tells to consider the following '-'s as filename.
