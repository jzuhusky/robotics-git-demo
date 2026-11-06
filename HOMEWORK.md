# Homework

Do these four things before our next meeting, in this order. Each part needs the one before it.

Plan on about 45 minutes. Most of that time is making an account and signing in. The git commands at the end are short.

When you are done, all of this is true:

- [ ] You have a GitHub account, and you have sent me the username.
- [ ] A push or an SSH test has succeeded, so GitHub recognizes your computer.
- [ ] Your line is in `guestbook.txt` on the `main` branch.
- [ ] GitHub shows a pull request with your new file on a branch.

Work in **robotics-git-demo** only. That is this project:

https://github.com/jzuhusky/robotics-git-demo

## 0. Open a Terminal, and check that git is installed

You need a computer where you can install programs. A school Chromebook usually cannot do these steps. If that is the machine you have, tell me and we will set you up another way.

**Mac**

1. Press Command and the space bar together. A search box opens.
2. Type `Terminal` and press Enter.
3. A window appears with a blinking cursor. That window is the Terminal.

**Windows**

1. Download Git from https://git-scm.com/download/win and install it. The default choices are fine. Click through them.
2. Open the Start menu, type `Git Bash`, and press Enter.
3. Use that window for every command below. The regular Command Prompt is a different program.

The line you type on ends in `$` or `%`. You do not type that symbol. You type the command, then press Enter.

Check git:

```bash
git --version
```

A version number means you are ready. On a Mac, the computer may ask to install developer tools. Click Install, wait for it to finish, and run `git --version` again.

If the computer says `command not found`, stop and message me. The rest of the homework needs git.

Paste in the Terminal is Command+V on a Mac. In Git Bash, right-click the window and choose Paste.

## 1. Create a GitHub account

1. Go to https://github.com/signup
2. Use an email you can actually check. GitHub sends a code.
3. Pick a username you are willing to have on a team. Your name is a good username. The team will learn it.
4. Finish the signup and open the confirmation email.

Send me the username. I add each person to the repo by hand. Until I add you, the push in part 3 is rejected. That message means "you are not on the list yet," and the fix is me adding you.

## 2. Tell git your name, and sign in to GitHub

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

If a teammate sees it, delete that token on the same GitHub page and make a new one. Tell me.

You will use this address when you clone in part 3:

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

You will use this address when you clone in part 3:

```text
git@github.com:jzuhusky/robotics-git-demo.git
```

The files you download are the same ones Way A downloads. The address decides how you sign in.

## 3. Sign the guestbook, on main

`main` is the official copy of the project. This part edits it directly, the way we did in class. Part 4 does the safer version, on a branch.

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

`pwd` should end in `robotics-git-demo`. `ls` should show `file.txt`, `guestbook.txt`, `README.md`, and `HOMEWORK.md`.

Download any lines classmates have already added:

```bash
git pull
```

Open the guestbook in a simple editor:

```bash
nano guestbook.txt
```

`nano` is a text editor inside the Terminal. The controls are printed along the bottom. The `^` symbol means the Control key.

1. Move to the end of the file with the arrow keys.
2. Add one new line, matching the lines that are already there:

```text
Your Name, SHS Class of 20XX
```

3. Press Control+O, then Enter, to save. The letter is O, as in "output."
4. Press Control+X to exit.

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

**You don't have permission.** The message mentions permission, or `403`, or access denied. Send me your GitHub username. I still need to add you. Your commit is safe on your computer. Push again after I reply.

**Someone else signed the book while you were working.** The message says the remote contains work you do not have, or tells you to pull first. Run:

```bash
git pull
git push
```

**Git says CONFLICT.** Stop. Do not commit again. Open `guestbook.txt` only to look. Lines made of `<<<<<<<` and `>>>>>>>` are git marking the two versions it could not combine. Leave them there and message me with a screenshot of the Terminal. We will clean it up together.

## 4. Add a new file, on a branch

Part 3 changed `main` directly because the guestbook is one shared list. Robot code goes on a branch first, so a half-finished change stays off the copy everyone else is using.

A branch is a second timeline, starting from `main` at the moment you create it. Your commits land on that timeline. `main` stays as it was until we merge your branch in. A **pull request** is you asking to merge it.

Start from an up-to-date `main`, inside the `robotics-git-demo` folder:

```bash
git checkout main
git pull
git checkout -b yourname-intro
```

Replace `yourname` with your first name in lowercase, with no spaces. Alex would run:

```bash
git checkout -b alex-intro
```

`git checkout main` stands on the official branch. `git checkout -b` makes a new branch and stands on that one instead.

Make a folder for student files, then open a new file:

```bash
mkdir -p students
nano students/yourname.txt
```

Use your first name, lowercase, in the file name too: `students/alex.txt`.

Write a few lines:

- Your name and grade
- One thing you want to learn on this team
- Anything else you want the team to know

Save with Control+O, Enter. Leave with Control+X.

Then:

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

1. I have your GitHub username.
2. Way A has pushed successfully, or `ssh -T git@github.com` greeted you by username.
3. Your guestbook line is visible on GitHub in `guestbook.txt`.
4. An open pull request contains `students/yourname.txt`.

## If you get stuck

Send me the command you typed and the full text the computer printed.

A few messages and what they usually mean:

| What you see | What it usually means |
| --- | --- |
| `command not found: git` | Git is not installed. Go back to part 0. |
| `not a git repository` | The Terminal is in the wrong folder. Run `pwd` and `ls`. You want to be inside `robotics-git-demo`. |
| `nothing to commit, working tree clean` | Git sees no saved edit. In `nano`, Control+O writes the file. Also check that you edited the file inside this folder. |
| `Authentication failed` | Way A used the website password, or the token was incomplete. Make a new classic token, check **repo**, and paste that when asked for a password. |
| `Permission denied (publickey)` | Way B: GitHub does not have your public key yet, or the clone used the `git@github.com` address before the key was added. Repeat the `.pub` copy steps and the `ssh -T` test. |
| `Connection timed out` on `ssh` | This network is blocking SSH. Use Way A and the `https://` address. |

Stuck inside `vim` from class: press Escape, type `:q!`, press Enter.

Stuck inside `nano`: Control+X. If it asks to save, press N to leave without saving, or Y and then Enter to keep the edit.
