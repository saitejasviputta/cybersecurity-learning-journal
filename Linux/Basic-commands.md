# Linux Basic Command Notes

Personal notes on Linux commands, terminal operations, file management, permissions, user management etc.

## 1. Introduction to Linux

- Linux is **case-sensitive**.
- `echo` works like the `print()` function in programming languages.

```bash
echo "Hello World"
```

Output:
```text
Hello World
```

### Basic Commands for User Information

| Command | Description |
|---|---|
| `whoami` | Displays the current username. |
| `id` | Displays user ID (UID), group ID (GID), and group information. |
| `id -un` | Displays only the username. |
| `id -u` | Displays the user ID (UID). |
| `id -g` | Displays the primary group ID (GID). |
| `groups` | Displays all groups the user belongs to. |

### Working with Directories

| Command | Description |
|---|---|
| `pwd` | Prints the current working directory. |
| `echo ~` | Displays the path to the home directory. |
| `ls` | Lists files in the current directory. |
| `ls ~` | Lists files in the home directory. |
| `history` | Displays the terminal command history. |
| `cd ..` | Moves one level up to the parent directory. |
| `cd ~` | Navigates to the home directory. |

## 2. File and Directory Management

### Creating Files and Directories

**Create an empty file:**

```bash
touch filename
```

Creates an empty file. If the file already exists, its timestamps are updated without changing its contents.

**Create a directory:**

```bash
mkdir directory_name
```

**Create or display text using echo:**

```bash
echo "Something" > filename
```

Redirects the output of `echo` into a file.

- `>` overwrites the existing contents.
- `>>` appends output to the existing contents.

### Hidden Files

In Linux, files and directories whose names begin with a dot (`.`) are considered hidden.

```bash
ls -a
```

Lists all files, including hidden files.

### Listing Files

| Command | Description |
|---|---|
| `ls` | Lists files in the current directory. |
| `ls -l` | Displays files in long-format listing. |
| `ls -a` | Lists all files, including hidden files. |
| `ls -R directory` | Lists directory contents recursively. |
| `ls -r` | Displays files in reverse sort order. |

### Copying Files and Directories

**Copy a file in the current directory:**

```bash
cp filename copy_name
```

Creates a copy of the file.

**Copy a file into another directory:**

```bash
cp filename directory/
```

**Copy a directory recursively:**

```bash
cp -r testdir test_copy
```

The `-r` option ensures that the directory and its contents are copied recursively.

### Moving and Renaming Files

**Rename a file:**

```bash
mv file.txt new.txt
```

**Move a file into another directory:**

```bash
mv file.txt directory/
```

**Move and rename a file:**

```bash
mv testdir/new.txt ./file.txt
```

Moves `new.txt` out of `testdir` and renames it to `file.txt` in the current directory.

### Removing Files and Directories

| Command | Description |
|---|---|
| `rm filename` | Removes a file. |
| `rm -i filename` | Asks for confirmation before deleting. |
| `rmdir directory` | Removes an empty directory. |
| `rm -r testdir` | Removes a directory and its contents recursively. |
| `rm -rf directory` | Removes directories recursively without prompting for confirmation. |


## 3. Important Linux Paths

| Path | Description |
|---|---|
| `~` | Represents the user's home directory. |


## 4. Viewing and Comparing Files

### cat

Displays the contents of a file.

```bash
cat filename
```

**Display contents with line numbers:**

```bash
cat -n filename
```

### head

Used to view the beginning of a file.

```bash
head filename
```

**Display only the first line:**

```bash
head -n 1 filename
```

**Display the first byte:**

```bash
head -c 1 filename
```

### tail

Similar to `head`, but displays the end of a file.

```bash
tail filename
```

### diff

Displays the differences between two files.

```bash
diff file1 file2
```

**Compare directories recursively:**

```bash
diff -r dir1 dir2
```

Recursively compares files and subdirectories.

## 5. File Ownership and Permissions

### File Permissions

When we execute:

```bash
ls -l filename
```

Linux displays file information, including its permissions.

Example:

```text
-rwxr-xr--
```

The first character indicates the file type:

| Symbol | Meaning |
|---|---|
| `-` | Regular file |
| `d` | Directory |
| `l` | Symbolic link |

The next nine characters represent permissions.

They are divided into three groups:

1. Owner permissions
2. Group permissions
3. Others (normal users) permissions

Each group has three permission types:

| Symbol | Permission | Meaning |
|---|---|---|
| `r` | Read | Permission to read the file. |
| `w` | Write | Permission to modify the file. |
| `x` | Execute | Permission to execute the file. |
| `-` | No permission | Permission is not granted. |

### chmod – Change Mode

The `chmod` command is used to change file permissions.

#### Numeric Notation

| Permission | Value |
|---|---:|
| Read (`r`) | 4 |
| Write (`w`) | 2 |
| Execute (`x`) | 1 |
| No permission | 0 |

Permissions are specified separately for the owner, group, and others.

Example:

```bash
chmod 754 filename
```

Here:
- Owner: 7 = Read + Write + Execute
- Group: 5 = Read + Execute
- Others: 4 = Read

#### Symbolic Notation

| Symbol | Represents |
|---|---|
| `u` | Owner (user) |
| `g` | Group |
| `o` | Others |
| `a` | All |

Operators:

- `+` adds permissions.
- `-` removes permissions.
- `=` sets permissions explicitly.

Example:

```bash
chmod u+x filename
```

Adds execute permission to the owner.

### chown – Change Ownership

Changes the ownership of a file or directory.

```bash
sudo chown owner:group filename
```

Changes the file's owner and group.

## 6. Shell and Bash

### What is a Shell?

A shell is a program that interprets and executes the commands you type in the terminal.

### What is Bash?

Bash stands for **Bourne Again Shell**.

Benefits of Bash:

- More intuitive command-line interface.
- Enhanced scripting capabilities.
- Better customization options for the user's environment.

### Shebang

```bash
#!/bin/bash
```

This line is called the **shebang**.

It tells Linux to execute the script using the Bash interpreter.

### Changing the Default Shell

```bash
sudo usermod -s /bin/bash username
```

Changes the default shell of the specified user to Bash.

## 7. User Management

### sudo

`sudo` is a command that allows a permitted user to execute commands with elevated privileges.

It is commonly used when performing administrative tasks that require higher-level permissions.

### Creating a User

```bash
sudo useradd username
```

Creates a new user.

**Create a user with a home directory:**

```bash
sudo useradd -m username
```

The `-m` option creates a home directory for the new user.

### Setting a Password

```bash
sudo passwd username
```

Sets or changes the password for the specified user.

### User Account Files

```text
/etc/passwd
```

This file contains information about user accounts. Each line represents a user account.

### Modifying User Accounts

**Change the home directory:**

```bash
sudo usermod -d /home/new_directory username
```

Changes the user's home directory setting.

**Change the default shell:**

```bash
sudo usermod -s /bin/bash username
```

**Add a user to the sudo group:**

```bash
sudo usermod -aG sudo username
```

- `-a` appends the user to existing supplementary groups.
- `-G` specifies the supplementary group.

### Why Add a User to the sudo Group?

- System administration
- Software installation
- Configuration changes
- User management

### Why Use the sudo Group Instead of Sharing the Root Password?

- Convenience: No need to share the root password.
- Granular control over administrative access.
- Accountability: Commands can be associated with individual users.
- Improved security.

### Switching Users

```bash
su username
```

Switches to another user account.

### Locking and Unlocking User Accounts

**Lock a user's password:**

```bash
sudo passwd -l username
```

**Unlock a user's password:**

```bash
sudo passwd -u username
```

### Deleting a User

```bash
sudo userdel -r username
```

Deletes the user and removes their home directory and mail spool.

## 8. Command History Shortcuts

| Command | Description |
|---|---|
| `!!` | Executes the most recently executed command. |
| `!-n` | Executes the command located `n` positions back in history. |

Example:

```bash
!!
```

Runs the previous command again.

## 9. Environment Variables

Environment variables store information that can be accessed by processes running in the shell environment.

### HISTSIZE

```bash
HISTSIZE
```

Defines how many previous commands are stored in the shell's command history.

Its value can be modified using an assignment expression.

### env

```bash
env
```

Displays a list of environment variables.

**Search for a particular variable:**

```bash
env | grep variable_name
```

### export

```bash
export var_name
```

Exports a shell variable so that it is available to child processes.

### unset

```bash
unset var_name
```

Removes the specified shell variable.

## 10. Locating Files and Directories

### locate

```bash
locate filename
```

Helps find the location of files and directories.

### locate -c

```bash
locate -c filename
```

Displays the number of matching results.

---
