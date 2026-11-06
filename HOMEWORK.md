# Homework

Do this after [pre-requisites.md](pre-requisites.md). Git should already be installed, and you should already have a GitHub account.

Moving between folders is covered in [command-line.md](command-line.md). Keep that page open if `cd` and `pwd` are still new.

Plan on about 30 minutes. The git commands are short. Signing in is the part that takes the longest.

When you are done, all of this is true:

- [ ] You posted your GitHub username in the WhatsApp group, accepted the invite, and only then edited the repo.
- [ ] If you worked on your computer, a push or an SSH test succeeded. If you used the GitHub website, the commits show your username.
- [ ] Your line is in `guestbook.txt` on the `main` branch.
- [ ] GitHub shows a pull request with your new file on a branch.

Work in **robotics-git-demo** only. That is this project:

https://github.com/jzuhusky/robotics-git-demo

## For the coach

Students skip this section. Add each student as soon as their username shows up in the WhatsApp group, and before they edit anything. The pencil on github.com, a push from their laptop, and a new file all go wrong until they are a collaborator and have accepted. If they edit early, GitHub asks them to fork the repo into their own account. That fork is a private copy, not the class guestbook.

1. Open https://github.com/jzuhusky/robotics-git-demo
2. Click **Settings**.
3. In the left sidebar, under **Access**, click **Collaborators**.
4. Click **Add people**.
5. Type the username they posted in the WhatsApp group and click the matching account. An email works only when it is the email on that GitHub account.
6. Click **Add NAME to this repository**.

The Collaborators page then lists them as pending. After they accept, they show up as a collaborator. An invite expires after 7 days. From that same page you can see who is still pending.

On a personal repository, a collaborator can push, including a push straight to `main`. That is the guestbook step. Leave `main` unprotected for this assignment. Under **Settings**, check **Rules** and **Branches**. A rule that requires a pull request for `main` rejects the guestbook push even after they accept.

GitHub caps how many people you can invite to one repository in a day. If **Add people** starts refusing invites, wait until the next day.

## Before you start

Open Terminal on a Mac, or Git Bash on Windows.

```bash
git --version
```

A version number means git is installed. If the computer says `command not found`, finish [pre-requisites.md](pre-requisites.md) first.

Post your GitHub username in the WhatsApp group if you have not already. I invite that account to the repo. You will get an email from GitHub, and the same invite shows up under the bell icon on the website. Click **Accept invitation**.

Stop there until the invite is accepted. Do not edit `guestbook.txt`, do not click the pencil on github.com, and do not push. Part 1, telling git your name, can happen while you wait. Parts 2 and 3 cannot. If you click the pencil before you are a collaborator, GitHub offers to fork the project into your own account. That is a separate copy, and your name never lands in the class guestbook.

## 1. Tell git your name, and sign in to GitHub

### Put your name on your commits

Run these two commands. Use your real name, and the same email you used on GitHub.

```bash
git config --global user.name "Your Full Name"
git config --global user.email "you@example.com"
```

This is the name that shows up in `git log` and on the website. It is separate from your password.

### Pick a way to sign in

GitHub lets the Terminal prove who you are in two ways. Do **one** of them.

Way A is a special password called a personal access token. Way B is an SSH key. Way A has fewer steps. Way B is worth it if this is your own computer and you want git to stop asking for a password.

School wifi sometimes blocks SSH. If Way B hangs or says `Connection timed out`, switch to Way A. Both ways can push the same homework.

---

### Way A: a personal access token

GitHub will ask you for a password later. The password it accepts is a **personal access token** you create on the website. GitHub rejects the password you use to log in at github.com. Paste the token when Terminal asks for a password.

Create one:

1. Log in at https://github.com
2. Click your profile picture in the top right, then **Settings**.
3. Scroll the left sidebar to the bottom and click **Developer settings**.
4. Click **Personal access tokens**, then **Tokens (classic)**.
5. Click **Generate new token**, then **Generate new token (classic)**.
6. GitHub may ask for your password again.
7. Note: `robotics class`
8. Expiration: 90 days.
9. Check the single box named **repo**. Leave the other boxes unchecked. That one box is permission to read and write repos from the Terminal.
10. Scroll down and click **Generate token**.
11. Copy the token right then. A classic token starts with `ghp_`. GitHub shows it once. If you leave the page before copying it, you cannot get that same token back. Generate a new one, and delete the one you never copied.

Keep the token somewhere only you can open, such as a notes app with a lock, or a password manager. It is a password.

- Do not put it in this repo.
- Do not paste it in a group chat.
- Do not put it in a screenshot.

If a teammate sees it, delete that token on the same GitHub page and make a new one. Post in the WhatsApp group that you deleted it.

You will use this address when you clone in part 2:

```text
https://github.com/jzuhusky/robotics-git-demo.git
```

When git asks:

- **Username:** your GitHub username
- **Password:** paste the token

The token does not appear as you paste it. The cursor sits there. That is normal. Press Enter.

Sometimes a browser window opens instead of a password prompt. Sign in there in the browser. That counts as finishing Way A.

---

### Way B: an SSH key

SSH is a login method that uses a matched pair of files instead of a password you paste each time.

- The **private key** stays on your computer. This is the key. It never gets emailed, uploaded, or pasted into GitHub.
- The **public key** is the lock that matches it. You give the lock to GitHub. When you push, GitHub checks that your computer holds the matching key.

Anyone can see a public key. The private key stays on your machine.

**Make the key pair.** In Terminal or Git Bash, run:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

Use your GitHub email inside the quotes.

- `Enter file in which to save the key` — press Enter. That accepts the suggested folder.
- `Enter passphrase` — type a short passphrase you will remember, then type it again. This passphrase unlocks the key on your computer. You can press Enter twice to leave it empty. A passphrase is the better choice on a computer other people can log into.

**Copy the public key.** The file you want ends in `.pub`.

Mac:

```bash
pbcopy < ~/.ssh/id_ed25519.pub
```

Windows Git Bash:

```bash
clip < ~/.ssh/id_ed25519.pub
```

Check what you copied:

```bash
cat ~/.ssh/id_ed25519.pub
```

The line starts with `ssh-ed25519` and ends with your email. That is the public key.

If a file's contents include the words `OPENSSH PRIVATE KEY`, you opened the private key. Close it. Do not paste it anywhere. The public file is the one with `.pub` at the end of the name.

**Give the public key to GitHub.**

1. On GitHub, click your profile picture, then **Settings**.
2. In the left sidebar, click **SSH and GPG keys**.
3. Click **New SSH key**.
4. Title: `my laptop` (or whatever machine this is).
5. Key type: **Authentication Key**.
6. Paste into the Key box. Save.

**Test it.**

```bash
ssh -T git@github.com
```

The first time, the computer asks if you trust GitHub's address. Type `yes` and press Enter.

Success looks like this:

```text
Hi YOUR-USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

That second half is part of the success message. GitHub recognized your key, and this connection is only for git commands.

You will use this address when you clone in part 2:

```text
git@github.com:jzuhusky/robotics-git-demo.git
```

The files you download are the same ones Way A downloads. The address decides how you sign in.

## How to change a file

Accept the collaborator invite before you use any of these. The invite comes first, before TextEdit, before VS Code, before vim, and before the pencil on the website.

**TextEdit, on a Mac.** From inside the `robotics-git-demo` folder, run:

```bash
open -a TextEdit guestbook.txt
```

If you see font sizes and colors, choose **Format → Make Plain Text**, then save. Git stores plain text.

**Notepad, on Windows.** From inside the repo in Git Bash, run:

```bash
notepad guestbook.txt
```

Save, then close Notepad.

**A code editor, such as VS Code.** Open the `robotics-git-demo` folder in the editor, click the file, type, and save. In VS Code, save is Command+S on a Mac and Ctrl+S on Windows.

**vim,** if you want to learn the editor from class. Run `vim guestbook.txt`. Press `i`, then type. When you are finished, press Escape, type `:wq`, and press Enter. That saves and quits. To leave and throw away what you typed, press Escape, type `:q!`, and press Enter.

**The GitHub website.** Open the file in the browser and click the pencil. That edits the class repo directly, once you are a collaborator. If the page tells you to fork the repository, stop and accept the invite first. Parts 2 and 3 say which commit button to press. The guestbook goes straight onto `main`. The new file goes on a branch.

A website edit commits for you. You skip `git add`, `git commit`, and `git push`. An edit on your computer stays on your computer until you run those three commands, and the saved file has to be inside `robotics-git-demo`.

## 2. Sign the guestbook, on main

`main` is the official copy of the project. This part edits it directly, the way we did in class. Part 3 does the safer version, on a branch.

Add one new line at the bottom of `guestbook.txt`, matching the lines already there:

```text
Your Name, SHS Class of 20XX
```

Use your own name and class year. Do this in one place, the website or your computer.

### On the GitHub website

1. Open https://github.com/jzuhusky/robotics-git-demo/blob/main/guestbook.txt
2. Click the pencil. If GitHub talks about forking, stop. Accept the collaborator invite, then come back.
3. Add your line at the bottom.
4. Choose **Commit directly to the `main` branch**.
5. Commit message: `Your Name signed the guestbook`
6. Click **Commit changes**.

Reload the file. Your line is in the class guestbook, and part 2 is done. Skip the clone below and go to part 3.

### On your computer

Clone, using the address that matches the way you signed in.

Token (Way A):

```bash
cd
git clone https://github.com/jzuhusky/robotics-git-demo.git
cd robotics-git-demo
```

SSH (Way B):

```bash
cd
git clone git@github.com:jzuhusky/robotics-git-demo.git
cd robotics-git-demo
```

`cd` by itself takes you to your home folder. `git clone` creates `robotics-git-demo` there. The second `cd` steps into it.

Check that you are in the right place:

```bash
pwd
ls
```

`pwd` should end in `robotics-git-demo`. `ls` should show `file.txt`, `guestbook.txt`, `README.md`, `HOMEWORK.md`, `pre-requisites.md`, and `command-line.md`. If `pwd` ends in your name, or in your home folder, you are one level too high. Run `cd robotics-git-demo` and check again. [command-line.md](command-line.md) is the page for this kind of "where am I?" problem.

Download any lines classmates have already added:

```bash
git pull
```

Open `guestbook.txt` with TextEdit, Notepad, VS Code, or vim, using [How to change a file](#how-to-change-a-file). Add your line, and save.

Back at the prompt, run the loop from class:

```bash
git status
git add guestbook.txt
git commit -m "Your Name signed the guestbook"
git push
```

Use your own name inside the quotes.

`git status` before the add should mention `guestbook.txt`. After the commit, status should say the working tree is clean. `git push` uploads it.

The first push is often the moment git asks you to sign in. Way A asks for your username and token. Way B may ask for the key passphrase.

Then refresh the repo page on GitHub. Your line is in `guestbook.txt`, and your commit is at the top of the list.

### If push is rejected

**You don't have permission.** The message mentions permission, or `403`, or access denied. Your commit is safe on your computer. Open GitHub, click the bell icon, and accept the repository invite if it is sitting there. Then run `git push` again. If there is no invite, post your GitHub username in the WhatsApp group. I still need to add you.

**Someone else signed the book while you were working.** The message says the remote contains work you do not have, or tells you to pull first. Run:

```bash
git pull
git push
```

**Git says CONFLICT.** Stop. Do not commit again. Open `guestbook.txt` only to look. Lines made of `<<<<<<<` and `>>>>>>>` are git marking the two versions it could not combine. Leave them there and post a screenshot of the Terminal in the WhatsApp group. We will clean it up together.

## 3. Add a new file, on a branch

Part 2 changed `main` directly because the guestbook is one shared list. Robot code goes on a branch first, so a half-finished change stays off the copy everyone else is using.

A branch is a second timeline, starting from `main` at the moment you create it. Your commits land on that timeline. `main` stays as it was until we merge your branch in. A **pull request** is you asking to merge it.

```text
main      *---*---*---*-----------*      official copy
                    \           /
                     *---*---*           students/yourname.txt
                     yourname-intro
```

Each `*` is a commit. Your file rides on the side branch until the pull request merges it into `main`.

Do this in one place, the website or your computer. Use your first name in lowercase, with no spaces. Alex's file is `students/alex.txt` and Alex's branch is `alex-intro`.

### On the GitHub website

1. Open https://github.com/jzuhusky/robotics-git-demo
2. Click **Add file**, then **Create new file**. If GitHub talks about forking, stop and accept the collaborator invite first.
3. Name the file `students/yourname.txt`. Use your first name, lowercase. The slash creates the `students` folder. Alex types `students/alex.txt`.
4. Write a few lines: your name and grade, one thing you want to learn on this team, and anything else you want the team to know.
5. Choose **Create a new branch for this commit and start a pull request**. Name the branch `yourname-intro`.
6. Click **Propose changes**, then **Create pull request**.

That pull request is the homework. I merge it onto `main` after I read it. Skip the terminal steps below.

### On your computer

If you signed the guestbook on the website, you do not have the folder yet. Do the clone steps in part 2, then come back here.

Start from an up-to-date `main`, inside the `robotics-git-demo` folder:

```bash
git checkout main
git pull
git checkout -b yourname-intro
```

`git checkout main` stands on the official branch. `git checkout -b` makes a new branch and stands on that one instead. Alex would run `git checkout -b alex-intro`.

Make a folder for the file, then open it in the same editor you used for the guestbook:

```bash
mkdir -p students
```

Save the file as `students/yourname.txt` inside `robotics-git-demo`. In vim, that is `vim students/yourname.txt`.

Write a few lines:

- Your name and grade
- One thing you want to learn on this team
- Anything else you want the team to know

Save the file. Then:

```bash
git status
git add students/yourname.txt
git commit -m "Add yourname intro"
git push --set-upstream origin yourname-intro
```

Match the branch name from the checkout command. `--set-upstream origin yourname-intro` is the same idea as the first push in class: upload this branch, and remember that it belongs to GitHub. Later pushes of this branch can be `git push`.

Git prints a link that starts with `https://github.com/jzuhusky/robotics-git-demo/pull/new/`. Open it.

If you do not see a link, open the repo on GitHub. A banner near the top offers **Compare & pull request**. Click it.

On the pull request page:

1. Title: `Add yourname intro`
2. In the comment box, one sentence about what the file is.
3. Click **Create pull request**.

That pull request is the homework. I merge it onto `main` after I read it. Your file joins the official copy when it is merged, and your branch is how it got there.

## You are done when

1. Your GitHub username is in the WhatsApp group, you accepted the invite, and you edited only after that.
2. If you worked on your computer, a push or an SSH test succeeded. If you used the website, the commits show your GitHub username.
3. Your guestbook line is visible on GitHub in `guestbook.txt`.
4. An open pull request contains `students/yourname.txt`.

## If you get stuck

Post in the WhatsApp group: the command you typed, and the full text the computer printed.

A few messages and what they usually mean:

| What you see | What it usually means |
| --- | --- |
| `command not found: git` | Git is not installed. Finish [pre-requisites.md](pre-requisites.md). |
| `not a git repository` | The Terminal is in the wrong folder. Run `pwd` and `ls`. You want to be inside `robotics-git-demo`. See [command-line.md](command-line.md). |
| `nothing to commit, working tree clean` | The editor did not save, or the file was saved outside `robotics-git-demo`. Save again, run `pwd`, and check that `ls` shows the file. |
| `Authentication failed` | Way A used the website password, or the token was incomplete. Make a new classic token, check **repo**, and paste that when asked for a password. |
| `Permission denied (publickey)` | Way B: GitHub does not have your public key yet, or the clone used the `git@github.com` address before the key was added. Repeat the `.pub` copy steps and the `ssh -T` test. |
| `Connection timed out` on `ssh` | This network is blocking SSH. Use Way A and the `https://` address. |

Stuck inside `vim`: press Escape, type `:q!`, press Enter. That quits and leaves the file as it was.
