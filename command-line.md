# Finding your way in the Terminal

The Terminal is a text window for talking to your computer. You are always standing in one folder. Commands act on that folder until you move.

```text
  (the folder above)              cd ..
         |
         +-- robotics-git-demo/   <-- pwd says you are here
               |
               +-- file.txt
               +-- guestbook.txt
               +-- students/      <-- cd students
                     |
                     +-- alex.txt
```

`cd students` steps down into `students`. `cd ..` steps up to the folder above. Two dots means "the folder that contains this one."

Mac, Linux, and **Git Bash** on Windows share the commands in the first column. **Command Prompt** on Windows uses the second column. For this class, Mac users open Terminal, and Windows users open Git Bash, so everyone types the first column.

How to open the window, and how to install git, is in [pre-requisites.md](pre-requisites.md).

## The prompt

The line you type on ends in `$` or `%`. You do not type that symbol. Type the command, then press Enter.

A window whose first line starts with `PS` is PowerShell. `cd`, `ls`, `pwd`, and `mkdir` still work there. If a command from this page fails, close that window and open Git Bash.

## Commands

| What you want | Mac, Linux, Git Bash | Windows Command Prompt |
| --- | --- | --- |
| Where am I? | `pwd` | `cd` |
| What files are here? | `ls` | `dir` |
| Go into a folder | `cd students` | `cd students` |
| Go up one folder | `cd ..` | `cd ..` |
| Go to your home folder | `cd` | `cd %USERPROFILE%` |
| Make a folder | `mkdir students` | `mkdir students` |
| Print a file | `cat note.txt` | `type note.txt` |
| Clear the screen | `clear` | `cls` |
| Copy a file | `cp note.txt copy.txt` | `copy note.txt copy.txt` |
| Rename a file | `mv note.txt letter.txt` | `move note.txt letter.txt` |
| Delete a file | `rm note.txt` | `del note.txt` |

`pwd` means print working directory. The working directory is the folder you are standing in.

`cd` with nothing after it, on Mac, Linux, and Git Bash, takes you home. Home is your user's folder, the one named after you.

`rm` and `del` skip the trash. The file is gone. Delete a file only when you typed its exact name and `ls` or `dir` shows it in this folder. Leave any folder named `.git` alone. That folder is the project history.

A name with a space needs quotes:

```bash
cd "My Folder"
```

## Slashes

Mac and Linux paths look like this:

```text
/Users/alex/robotics-git-demo
```

Git Bash on Windows looks like this:

```text
/c/Users/alex/robotics-git-demo
```

Command Prompt looks like this:

```text
C:\Users\alex\robotics-git-demo
```

In Terminal and Git Bash, type forward slashes: `cd students/alex`.

## Habits that save time

**Up arrow** repeats the last command. Press it again for the one before that.

**Tab** finishes a name. Type `cd rob` and press Tab. If `robotics-git-demo` is the only match, the computer fills it in. If nothing happens, the letters you typed do not match a file here. Run `ls` and look.

**Control+C** cancels the command that is running. It does not copy text.

Copy and paste:

- Mac Terminal: Command+C copies, Command+V pastes.
- Git Bash: highlight the text and right-click to copy. Right-click to paste.
- Linux: Ctrl+Shift+C copies, Ctrl+Shift+V pastes.

When git asks you to paste a secret, the characters stay hidden. The cursor sits still. That is normal. Press Enter.

## Try it

Do this in your home folder, away from any project. The lines starting with `#` are notes. Do not type them.

```bash
cd
pwd
mkdir terminal-practice
cd terminal-practice
pwd
echo "Hello there" > note.txt
ls
cat note.txt
cd ..
pwd
```

`echo "Hello there" > note.txt` writes a file. One `>` creates the file. Two arrows, `>>`, add a line at the end of a file that already exists.

After `cd ..`, you are back in your home folder, and `terminal-practice` is still there. You can leave it. To throw it away, delete `terminal-practice` from Finder or File Explorer. That uses the trash, which `rm` does not.

## Where this shows up in class

The lesson is [README.md](README.md). The assignment is [HOMEWORK.md](HOMEWORK.md). Both assume you can `cd` into a folder and read what `pwd` and `ls` say. When a git command complains that this is not a git repository, you are almost always standing in the wrong folder. Run `pwd`, then `ls`, and move until `pwd` ends in `robotics-git-demo`.
