# Robotics Git Demo

This folder is the project we made together in class. In class it held two files, `file.txt` and `guestbook.txt`, plus the history of how they were written. Your homework is to add yourself to that history.

The Terminal felt fast in class. That is a normal first reaction. You can go one command at a time at home. Read what the computer prints before you type the next thing.

## The idea, in one picture

Imagine the team is writing the code that drives the robot.

You fix a bug. A teammate adds a new command. Someone else tries a change, and the robot starts spinning in circles. If the "real" code is whichever file got emailed last, the working version from Tuesday is gone.

Git is a save system that remembers every version, who saved it, and a sentence about what changed. You can read that history. You can go back to an older save when a new one is trouble.

Each save is called a **commit**.

That system is called version control. Git is the version control program we use.

## Git and GitHub

These are two separate things that work as a pair.

**Git** is the program on your computer. It keeps the history in a hidden folder named `.git` inside the project. Commits work with the wifi off.

**GitHub** is the website that stores a copy of that same history, so the whole team is building on one timeline. Ours is here:

https://github.com/jzuhusky/robotics-git-demo

A useful picture: Git is the notebook in your backpack. GitHub is the shelf in the classroom where the team keeps the shared notebook.

People mix the two words up. When you are typing commands, you are using git. When you are looking at the project in a browser, you are on GitHub.

## The loop to remember

Almost every task this season fits in four steps.

1. Change a file.
2. `git add` chooses which changes go into the next save.
3. `git commit` takes the save and attaches your message.
4. `git push` uploads that save to GitHub.

`git add` and `git commit` feel like two saves. They are one save, split in half, for a good reason. You might change three files and only want to save one of them. `git add` is you picking what belongs in this commit. `git commit` seals it and writes the label.

Any time you feel lost, run:

```bash
git status
```

Status is git answering the question "what is going on in this folder right now?" Run it often. It is the command we used the most in class.

## Words from class

**Repository (repo).** The project folder, plus the history git is keeping for it. This folder is a repo.

**Commit.** One save: the files at that moment, your name, the time, and the message you wrote.

**Commit message.** The sentence you put in quotes, like `"Joey signed the guest book"`. Write it so a teammate can tell what changed without opening the files. `"Change the stuff"` is a legal message, and it tells the team nothing.

**Stage.** What `git add` does. The chosen changes sit in a waiting area until you commit.

**Push.** Upload your new commits to GitHub.

**Pull.** Download commits that a teammate already uploaded.

**Clone.** Download the repo for the first time, history included, onto a computer that does not have it yet.

**Remote.** A nickname for the GitHub copy. Ours is named `origin`.

**main.** The official line of history. The version the team treats as current.

**Branch.** A side line of history for work that is not ready for `main`. Homework part 4 uses one. `main` is the competition robot. A branch is the practice robot. You try the new idea on the practice robot, and you move it over once it works.

## What we actually did

We used the Terminal, which is a text window for giving the computer instructions. You type a command, press Enter, and it answers.

### Making a file

```bash
mkdir robotics
cd robotics
pwd
echo "Hello there" > file.txt
echo "Hello there" >> file.txt
cat file.txt
```

`mkdir` makes a folder. `cd` moves into it. `pwd` prints where you are. `echo ... > file.txt` writes a file, replacing whatever was there. `>>` adds a line at the end. `cat` prints the file.

### Telling git to start remembering

```bash
git init
git status
git add file.txt
git commit -m "Intro to git in robotics"
git log
```

`git init` starts history for the folder you are standing in. `git add` picks `file.txt` for the first save. `git commit -m` takes the save. The words in quotes are the message. `git log` lists the saves, newest first.

Each commit has a long id, something like `3a0037fba6b8ff740ec08e50416673bc7c76b578`. You can look at one save with the first few characters:

```bash
git show 3a0037f
```

### Putting it on GitHub

```bash
git remote add origin git@github.com:jzuhusky/robotics-git-demo.git
git push --set-upstream origin main
```

The first line saves the GitHub address under the nickname `origin`. The second line uploads `main` and tells git to remember the connection. The next time, `git push` alone is enough.

That long command is just the four words we already know, plus an address. `origin` is GitHub. `main` is the branch. `--set-upstream` means "remember this pairing."

### Signing the guestbook

We opened `guestbook.txt`, added a line, then ran the loop:

```bash
git status
git add guestbook.txt
git commit -m "Joey signed the guest book"
git push
```

We did it again for a second line. The file looks like this:

```text
Joey Zuhusky, SHS Class of 2012
Scrooge McDuck, SHS Class of Never
```

Your homework adds the next line.

We edited the file with `vim`, an editor that lives inside the Terminal. It is powerful, and it is a bad first editor. If you ever land in it and cannot leave: press the Escape key, type `:q!`, and press Enter. That quits without saving. For homework, use the easier editor in [HOMEWORK.md](HOMEWORK.md).

### Getting a copy on another computer

```bash
git clone git@github.com:jzuhusky/robotics-git-demo.git
```

Clone makes a new folder with the files and the full history. We also opened the real 2026 kit bot code and walked around it with the same commands: `cd`, `ls`, `git status`, `git log`. The robot repo is bigger. The moves are the same.

Homework stays in **this** repo, `robotics-git-demo`. Leave the kit bot repo alone.

## A small cheat sheet

| Command | What it does |
| --- | --- |
| `pwd` | Where am I? |
| `ls` | What files are here? |
| `cd some-folder` | Move into a folder |
| `cd ..` | Move up one folder |
| `cat file.txt` | Print a file |
| `git status` | What has changed? What is waiting to be saved? |
| `git add file.txt` | Include this file in the next commit |
| `git commit -m "message"` | Save, with a label |
| `git log` | Show the list of commits |
| `git push` | Upload commits to GitHub |
| `git pull` | Download teammates' commits |
| `git clone ADDRESS` | Copy a repo onto this computer |

## When a command complains

Read the message. Git writes a lot, and the useful part is usually the last few lines.

We mistyped commands in class, including ones git does not have. The fix was to read the answer and try the right command. A typo is part of using a terminal, the same way a missed bolt is part of building a robot.

If you have been stuck for a few minutes, stop and send me two things: the command you typed, and the full message the computer printed. Leave the folder where it is. The history is the valuable part, and deleting the folder throws it away.

## Homework

The assignment is in [HOMEWORK.md](HOMEWORK.md). Do the four parts in order.
