# Before class

Do this on the computer you will use for homework, before we meet. Two things have to exist before git commands will work.

```text
   YOUR COMPUTER                         THE WEBSITE
+--------------------------+           +--------------------------+
| git                      |           | a GitHub account         |
| installed, so Terminal   |           | free, with a username    |
| understands git          |           | you send to me           |
+--------------------------+           +--------------------------+
```

Git is the program. GitHub is the website. You need both.

When you are done:

- [ ] `git --version` prints a version number.
- [ ] You can log in at https://github.com
- [ ] You have posted your GitHub username in the WhatsApp group.

The commands for moving between folders are in [command-line.md](command-line.md). Skim that once git is installed. You do not have to memorize it.

Homework comes after this, in [HOMEWORK.md](HOMEWORK.md).

## If your computer is a Chromebook

Stop here and post in the WhatsApp group. A school Chromebook usually cannot install git. We will set you up another way.

## 1. Install git

### Mac

1. Press Command and the space bar together.
2. Type `Terminal` and press Enter.
3. In the window that opens, type this and press Enter:

```bash
git --version
```

A version number means git is already installed. Skip to creating your GitHub account.

If git is missing, a window asks to install command line developer tools. Click **Install**. It can take several minutes and needs wifi. The Mac may ask for the password you use to log into the computer. When it finishes, close Terminal, open it again, and run `git --version` once more.

If no install window appeared and the command still fails, run:

```bash
xcode-select --install
```

Click Install on the window that opens, wait, then try `git --version` again.

If the computer asks for an administrator password you do not have, stop and post in the WhatsApp group. Some school laptops block this install.

### Windows

1. Go to https://git-scm.com/download/win
2. The installer should download. Open it.
3. Click **Next** through the screens. Leave the choices as they are. On the screen about your PATH, the selected line should be **Git from the command line and also from 3rd-party software**. That is the default. Keep it.
4. Finish the install. Open the Start menu, type `Git Bash`, and press Enter.
5. In that window, run:

```bash
git --version
```

A version number means you are ready. Use **Git Bash** for this class, the same way a Mac uses Terminal. Command Prompt and PowerShell are different apps. [command-line.md](command-line.md) shows their commands too, in case one of those opens instead.

### Linux

Open a terminal. On Ubuntu, Ctrl+Alt+T often does it. Then run:

```bash
git --version
```

A version number means you are done with this step. If the command is missing and the computer is Ubuntu or Debian, run:

```bash
sudo apt install git
```

It asks for the password you use to log into the computer. Nothing shows as you type the password. Press Enter. If that command fails, post the message in the WhatsApp group and stop.

### The check, on every computer

```bash
git --version
```

Something like `git version 2.39.2` is success. `command not found` means the install did not finish.

## 2. Create a GitHub account

1. Go to https://github.com/signup
2. Use an email you can check. GitHub sends a code. Look in spam if it is not in your inbox.
3. Choose a password for the **website**. GitHub wants at least 15 characters, or at least 8 characters with a number and a lowercase letter. Save it somewhere only you can open. Homework later creates a second secret for the Terminal. The website password stays the website password.
4. Pick a username the team will see. Letters, numbers, and single hyphens only. No spaces. It cannot start or end with a hyphen. Your name is a good username.
5. Enter your country and finish the form. Solve the puzzle if one appears.
6. Type the code from the email when GitHub asks.

You can choose **Continue with Google** or **Continue with Apple** instead of typing an email and password. You still pick a username.

If GitHub asks extra questions about your interests, or offers a paid plan, stay on the free account and skip anything optional.

When you are in, click your profile picture. Your username is there. Post that username in the WhatsApp group. I add each person to the class repo by hand. You can look at the project on the website while you wait. Do not click the pencil, edit a file, or push until you have accepted the collaborator invite. Before that, GitHub treats your edit as a request to copy the whole project into your own account.

GitHub may also offer two-factor authentication, a second check when you log in. You can skip it for now. If you turn it on, save the recovery codes somewhere you can find them. Those codes are how you get back in if you lose your phone.

## You are done when

1. `git --version` prints a number.
2. You can open https://github.com and see your username.
3. The WhatsApp group has your username.

Next, glance at [command-line.md](command-line.md), then do [HOMEWORK.md](HOMEWORK.md).
