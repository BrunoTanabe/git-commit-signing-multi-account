# SIGNING COMMITS IN GIT WITH MULTIPLE ACCOUNTS: THE COMPLETE GUIDE (WINDOWS, LINUX & MACOS)

![Banner](./images/banner.png)

- [View on Medium](https://medium.com/@tanabebruno/signing-commits-in-git-with-multiple-accounts-the-complete-guide-windows-linux-macos-2bd8125df03b)  
- [View in Brazilian Portuguese](README-PTBR.md)

If you’ve already tackled the challenge of setting up multiple SSH keys and now want to take your commit security and reliability to the next level, you’re in the right place! In this guide, we’ll pick up exactly where we left off in the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646), but this time focusing on GPG keys to sign your commits. That way, you get that “Verified” badge (way cooler than any Twitter checkmark) and ensure that everyone knows it was really you who made that commit! 🤩

You know those companies that require signed commits? Or those moments when you want to prove that the code is genuinely yours (no cloning or hacking involved)? That’s where GPG becomes your best ally, ensuring integrity and authenticity. And of course, we’ll keep things light and fun: yes, you can enjoy yourself while learning to configure two or more GPG keys without stress. 🚀

Ready to get everything running smoothly and securely signed? Let’s go! ✋

**IMPORTANT**: This tutorial is the second part of a series. If you haven’t read the first one yet, I recommend checking out the guide on [How to set up two or more SSH keys to use multiple Git accounts on the same computer (Windows, Linux & MacOS)](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646)before continuing here. I’ll be picking up right where that one left off, and you’ll need to have completed a few configurations explained there. Plus, it’ll help you better understand how everything connects and make it easier to follow along. 😉

---

## Table of Contents 📌

**Curious about what you’ll find in this guide?** 🔍

- [SIGNING COMMITS IN GIT WITH MULTIPLE ACCOUNTS: THE COMPLETE GUIDE (WINDOWS, LINUX \& MACOS)](#signing-commits-in-git-with-multiple-accounts-the-complete-guide-windows-linux--macos)
  - [Table of Contents 📌](#table-of-contents-)
  - [1. What are GPG keys? 🤔](#1-what-are-gpg-keys-)
  - [2. Why set up more than one GPG key? 🔒](#2-why-set-up-more-than-one-gpg-key-)
  - [3. Prerequisites: Making Sure GPG Is Installed 🔧](#3-prerequisites-making-sure-gpg-is-installed-)
    - [Windows](#windows)
    - [Linux](#linux)
    - [MacOS](#macos)
  - [4. Generating New GPG Keys 🔑](#4-generating-new-gpg-keys-)
    - [Windows, Linux and MacOS](#windows-linux-and-macos)
    - [IMPORTANT](#important)
  - [5. Configuring Git to Use the Correct GPG Keys 🔧](#5-configuring-git-to-use-the-correct-gpg-keys-)
    - [Windows, Linux, and macOS (common part)](#windows-linux-and-macos-common-part)
    - [Windows](#windows-1)
    - [Linux and macOS](#linux-and-macos)
  - [6. Copying Your GPG Keys to Add Them to Services ☁️](#6-copying-your-gpg-keys-to-add-them-to-services-️)
    - [Windows, Linux and MacOS](#windows-linux-and-macos-1)
  - [7. Adding GPG Keys to Services (GitHub, GitLab, Bitbucket, etc.) ☁️](#7-adding-gpg-keys-to-services-github-gitlab-bitbucket-etc-️)
    - [GitHub](#github)
    - [GitLab](#gitlab)
    - [BitBucket](#bitbucket)
  - [8. How to Sign Your Commits ✍️](#8-how-to-sign-your-commits-️)
    - [Signing Commits Automatically](#signing-commits-automatically)
    - [Signing Commits Manually](#signing-commits-manually)
  - [9. Conclusion 🎉](#9-conclusion-)
  - [Who is Bruno Tanabe?](#who-is-bruno-tanabe)

---

## 1. What are GPG keys? 🤔

Think of **GPG (GNU Privacy Guard)** as a cryptographic superhero that not only protects the identity of the person making the commit but also guarantees the integrity of what’s being submitted. Instead of just proving “who” you are, it proves it was **exactly** you who signed that commit — no room for fraud or hacker interference. 🕵️‍♂️

When you sign a commit with GPG, you get that shiny **authenticity badge** (the “Verified” label) that instantly makes things look more professional. It’s like putting a **powerful lock** on your commits, showing the world they’re legit and came from you.

And why is that so cool? Because besides increasing trust in the project’s history, you avoid the chaos of someone pretending to be you — plus, you can separate work from personal stuff just by **switching keys**! Imagine a setup like “Clark Kent” (your work login) and “Superman” (your personal account), each with their own signature. ⚡️

In short: GPG adds that extra touch of security and credibility. Want your commits to scream “this is serious and totally mine”? Then let’s get those GPG keys flying in your Git world and start signing safely! ✨

---

## 2. Why set up more than one GPG key? 🔒

If you’ve ever dealt with multiple Git accounts (for personal projects, work, or clients), you probably already know that **organization** is key to staying sane. Now, when we talk about **GPG keys**, things go up a level: you don’t just want to prove it’s you making the commits, but also **which** account each commit came from, right?

Picture this scenario:

- 💼 Your **work account** needs that verified signature, showing the commits came “officially” from your team or company.  
- 🏠 Your **personal account**, meanwhile, signs every commit with its own key, adding more security and authenticity to your side projects.

Having multiple distinct GPG keys for each of these accounts is the most practical way to **separate** (and sign) what’s personal from what’s professional. And the best part? No Git confusion, no need to constantly change configs, and yes, you still get that “Verified” badge that makes everything look super pro.

Instead of “messing around” copying and pasting keys, you configure each one properly and boom: when it’s time to sign, Git knows exactly which to use. That way, your work repo clearly shows your “official” commits, and your personal projects are signed by a different “you” (but still you — just organizing the chaos).

And let’s be honest, when it comes to **security**, you can never be too cautious. Isolating each “environment” is just smart. So if you like the idea of making sure no one can impersonate you (even just to mess around in your repo), let’s dive into setting up these GPG keys and keep everything flowing smoothly… and **signed**! ✍️✨

---

## 3. Prerequisites: Making Sure GPG Is Installed 🔧

Before you start creating your keys and giving those top-notch signatures to your commits, we need to make sure **GPG** is already installed on your machine, ready to jump into action. After all, without this tool from our cryptography superhero, the show of verified signatures can’t go on. 🎉

The good news? The installation process is super chill:

### Windows

[Go to the official **Gpg4win** download page](https://gpg4win.org/get-gpg4win.html).

Once downloaded, click the `.exe` file and run it as **Administrator**.

That classic installer with all the “Next” buttons will show up. Just keep clicking **Next, Next, Next** and accept everything — the default settings work just fine.

When it’s done, open your terminal (**Command Prompt or PowerShell**) and type:

```bash
   gpg --version
```

If the GPG version number shows up — success! You’re all set to fly around signing commits with your cape on. 🚀

### Linux

Open your terminal and try:

```bash
   gpg --version
```

If the GPG version shows up, awesome — you're good to go. If not, just install it:

```bash
   sudo apt-get install gnupg
```

(Or use your distro's package manager, like `yum`, `dnf`, etc.) Give it five minutes and... done. 🔧

### MacOS

Open the Terminal and type:

```bash
   gpg --version
```

If you see the version info, great. If not, you can install it using [Homebrew](https://brew.sh/):

```bash
   brew install gnupg
```

In just a few moments, everything will be ready. 🍏

Done! With GPG **officially** set to boost your security, the verified commit party can go on. Now it’s time to move on and actually start setting up your GPG keys. Ready? ✨

---

## 4. Generating New GPG Keys 🔑

Now that GPG is installed and ready for action, it’s time to create the GPG keys that will add that special touch to your commits. Don’t worry — the process is smooth and quick! Let’s do it? 🚀

As you saw in the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646) on **SSH** keys, I like to keep things tidy by isolating the keys in a specific folder in the root of my user directory. That helps keep everything organized and makes it easier to find the keys you need. So, let’s create a folder called `gpg` inside the `.ssh` directory we made earlier. If you didn’t make it yet, no worries — but I strongly recommend it! 😉

### Windows, Linux and MacOS

Here’s the step-by-step. It works the same way on Windows, Linux, and MacOS, so no system-specific steps here:

Open your terminal and make sure you’re in your user’s root directory. You can do that with this command:

```bash
    cd ~
```

Now, let’s create the `.gpg` folder in your root directory:

```bash
    mkdir .gpg
```

**Folder created!** Now let’s go into it:

```bash
    cd .gpg
```

Now comes the important part: **generating the GPG keys**. Just like in the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646), I’m going to create two GPG keys — one for each of my accounts: one ‘personal’ and one for ‘work’. If you have more than two accounts, just repeat the process for each one — it’s exactly the same.

```bash
    gpg --full-generate-key
```

At this point, GPG will ask you a series of questions. Just choose the options that make the most sense for you. Here are the options I chose:

- **Key type**: (9) ECC (sign and encrypt) *default*
- **Elliptic curve**: (1) Curve 25519 *default*
- **Expiration**: (0) Never expires *default* (If you pick an expiration date, you’ll need to generate a new key once it expires.)

### IMPORTANT

The last three questions are the most important, so pay close attention:

- **Name**: This is the name that will appear on your commits. I recommend using the same name as on your GitHub, GitLab, Bitbucket (or whichever platform you use) account. This helps identify your commits easily.
- **Email**: Here you **MUST** use the email tied to your GitHub, GitLab, Bitbucket (or whichever platform) account. If you don’t enter the correct email, GPG won’t be able to verify your commits and you won’t get that shiny “Verified” badge. So, focus on this part! 😉
- **Comment**: This field is optional and not super important — it’s only marked as important to maintain the flow of the tutorial. You can leave it blank or put in something meaningful to you.

Now I’m going to repeat the process for my second key, which will be for my work account. The process is the same, but this time use the **name** and **email** from your other account.

```bash
    gpg --full-generate-key
```

As for the options, you can stick with the same ones as before — just remember to use your work account’s name and email.

*Repeat the process as many times as needed to generate all the keys you need.*

---

## 5. Configuring Git to Use the Correct GPG Keys 🔧

You’ve got your GPG keys ready to roll, and now it’s time to make Git recognize these beauties. And don’t worry—it’s a super simple process! Let’s go? 🚀

Remember how we created a `.gitconfig` file for each account in the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646)? Well, now we’re going to add the GPG keys to those files. The process is the same, except now we’re adding the GPG key instead of the SSH key.

Here’s the step-by-step:

### Windows, Linux, and macOS (common part)

First, you need to find the ID of the GPG key you just created. To do that, just run the following command:

```bash
    gpg --list-secret-keys --keyid-format LONG
```

This command will list all the GPG keys you have on your machine. You’ll see something like this:

```bash
   sec   ed25519/8AEDA33EA0CA3AF6 2024-10-24 [SC] [expires: 2025-10-24]
         8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6
   uid                 [ultimate] Bruno Tanabe (My Personal Key) <brunotanabe@personal.com>
   ssb   cv25519/458RRDCC83ER4528 2024-10-24 [E] [expires: 2025-10-24]

   sec  ed25519/5A3F4B2D7E8C9A88 2024-10-24 [SC] [expires: 2025-10-24]
        A8AYTC1E26AFE7E2585A3F4B2D7E8C9ADADFC9A
   uid                 [ultimate] Bruno Tanabe (My Work Key) brunotanabe@work.com>
   ssb   cv25519/87A3F4B283ER49A 2024-10-24 [E] [expires: 2025-10-24]
```

You’ll have one key for each account. What you need to do now is copy the ID of each key. The key ID is the part between the slash `/` and the space—so in the example above, the personal key ID is `8AEDA33EA0CA3AF6`, and the work key ID is `5A3F4B2D7E8C9A88`.

Remember the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646)  where we created a `.gitconfig` file for each account? Now we’re going to add the GPG key to that file. Same process, just with the GPG key instead of the SSH key.

In the terminal, navigate to the `.gitconfig` file of the account you want to add the GPG key to. In my case, the `.gitconfig` files for each account are in the `.git` folder in my home directory (as we set up in the [previous tutorial](https://medium.com/@tanabebruno/how-to-set-up-two-or-more-ssh-keys-to-manage-multiple-git-accounts-on-the-same-computer-ca2767753646)). So the next step is to access the `.gitconfig` files for each account. To do that, run:

```bash
    cd ~/.git
```

Now we’ll edit the `.gitconfig` file for the account you want to add the GPG key to. This part varies depending on your operating system. Let’s go:

### Windows

Open the file with **Notepad** (or any editor you prefer):

```bash
   notepad .gitconfig-personal
```

Inside the file, add the line `signingkey = 8AEDA33EA0CA3AF6`, replacing it with the actual key ID for that account. The file will look like this:

```ini
   [user]
      name = Bruno Tanabe Personal
      email = brunotanabe@personal.com
      signingkey = 8AEDA33EA0CA3AF6
   [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**But Tanabe, how do I know which ID belongs to which account?**  
Easy! When you created the key, you set the name and email of the account you wanted. So just look at the key ID and see which name and email you assigned to it. That way, you’ll know which ID belongs to each account. And if both accounts have the same name and email? In that case, it doesn’t really matter—you can use the same ID for both or pick either key. What matters is that you know which ID belongs to which account.

Perfect! Now let’s do the same thing for the work account. The process is the same, but now you’ll add the work account’s GPG key. So open the `.gitconfig` file for the work account:

```bash
   notepad .gitconfig-work
```

The file will look like this:

```ini
   [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
      signingkey = 5A3F4B2D7E8C9A88
   [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
```

Just repeat the process for every account you have. And that’s it! Now your GPG keys are set up and ready to add that special signature touch to your commits. 🚀

### Linux and macOS

Open the file with **nano** (or any editor you prefer):

```bash
   nano .gitconfig-personal
```

Inside the file, add the line `signingkey = 8AEDA33EA0CA3AF6`, replacing it with the actual key ID for that account. The file will look like this:

```ini
   [user]
      name = Bruno Tanabe Personal
      email = brunotanabe@personal.com
      signingkey = 8AEDA33EA0CA3AF6
   [core]
      sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**But Tanabe, how do I know which ID belongs to which account?**  
Easy! When you created the key, you set the name and email of the account you wanted. So just look at the key ID and see which name and email you assigned to it. That way, you’ll know which ID belongs to each account. And if both accounts have the same name and email? In that case, it doesn’t really matter—you can use the same ID for both or pick either key. What matters is that you know which ID belongs to which account.

Perfect! Now let’s do the same thing for the work account. The process is the same, but now you’ll add the work account’s GPG key. So open the `.gitconfig` file for the work account:

```bash
   nano .gitconfig-work
```

The file will look like this:

```ini
   [user]
      name = Bruno Tanabe Work
      email = brunotanabe@work.com
      signingkey = 5A3F4B2D7E8C9A88
   [core]
      sshCommand = "ssh -i ~/.ssh/work_ssh_key"
```

Just repeat the process for every account you have. And that’s it! Now your GPG keys are set up and ready to add that special signature touch to your commits. 🚀

---

## 6. Copying Your GPG Keys to Add Them to Services ☁️

Now that your GPG keys are all set up, it’s time to copy them and paste them into the services you use (GitHub, GitLab, Bitbucket, etc.). It’s super simple: these services only need your **public key** to verify your commits. So just copy this part of your GPG key and paste it into your platform of choice—and boom, you’ve got that “Verified” badge! 🚀

### Windows, Linux and MacOS

Remember the key ID you used to configure Git? Now it’s time to use it to copy the public key. The command is the same for all operating systems—just plug in the key ID you want to export. For example, if your key ID is `8AEDA33EA0CA3AF6`, the command will look like this:

```bash
   gpg --armor --export 8AEDA33EA0CA3AF6
```

This command will generate a public key that you can copy and paste into your chosen platform. The output will look something like this:

```bash
   -----BEGIN PGP PUBLIC KEY BLOCK-----
   Version: GnuPG v2

   mQENBFh3+XABCAC1v4
   8AEDA33EA0CA3AF6B4E5D7E5
   8F2F8C1E26E0069BC7FE7E258AEDA33EA0CA3AF6
   =3A1D
   -----END PGP PUBLIC KEY BLOCK-----
```

You should copy everything from `-----BEGIN PGP PUBLIC KEY BLOCK-----` to `-----END PGP PUBLIC KEY BLOCK-----`. And that’s it! Now just paste it into the platform you want and lock in that “Verified” badge for your commits. 🚀

If you have more than one key, just repeat the process for each one. Don’t worry—it’s the same process, you just change the key ID. So if I wanted to run the command for my work key, it would look like this:

```bash
   gpg --armor --export 5A3F4B2D7E8C9A88
```

I recommend copying and pasting each key into its corresponding service as you go, so feel free to bounce between steps 7 and 8. 🔄

---

## 7. Adding GPG Keys to Services (GitHub, GitLab, Bitbucket, etc.) ☁️

Good news: everything on your computer is all set! Now there's just one final step to make everything run smoothly — letting the version control services (GitHub, GitLab, Bitbucket, or any other) know that you have a GPG key and that they can sign your commits with it. This is super simple and quick — all you need to do is paste the public key you copied in the previous step. 🖥️✨

Now that you’ve copied your keys, let’s paste them into your favorite service:

Here’s how to add your keys to the main version control services, but if you use a different one, just look for a similar section and add the keys.

### GitHub

1. Go to: [https://github.com/settings/keys](https://github.com/settings/keys)  
2. Click on **New GPG key**.  
3. Give the key a name (e.g., **Personal** or **Work**).  
4. Paste the content of your public key into the **Key** field.  
5. Click **Add GPG key**. Done! ✅  

### GitLab

1. Go to: [https://gitlab.com/-/profile/gpg_keys](https://gitlab.com/-/profile/gpg_keys)  
2. In the **Key** field, paste your public key.  
3. Give it a title for identification (e.g., **Personal** or **Work**).  
4. Click **Add key**. 🔑  

### BitBucket

1. Go to: [https://bitbucket.org/account/settings/gpg-keys/](https://bitbucket.org/account/settings/gpg-keys/)  
2. Click **Add key**.  
3. In the **Label** field, name your key.  
4. In the **Key** field, paste your public key.  
5. Save. 💾  

And that’s it! Now you’ve got your GPG keys added to the services and you’re ready to start signing your commits with them. 🚀  

---

## 8. How to Sign Your Commits ✍️

Now that your GPG keys are configured and added to the services, it’s time to learn how to sign your commits. Don’t worry — the process is super simple! Let’s do this! 🚀

You can sign your commits in two ways: **automatically** or **manually**. I’ll show you both so you can choose whichever works best for you. 😉

### Signing Commits Automatically

To sign all your commits automatically, just run the following command in the terminal:

```bash
   git config --global commit.gpgSign true
```

This command basically adds the following line to your `.gitconfig` file:

```ini
   [commit]
      gpgSign = true
```

This way, every commit you make will automatically be signed with the GPG key you configured. And the best part: you don’t have to change a thing about how you normally work! Just commit as usual, and that’s it. 🚀

### Signing Commits Manually

If you don’t want to sign every single commit, you can sign them manually (I can’t really think of a reason why you wouldn’t want to sign them all, but hey, some developers are weird). To do that, just add the `-S` flag to the commit command:

```bash
   git commit -S -m "Your commit message"
```

This command will sign the commit with the GPG key you configured. And again, the best part: you can use this command in any repository, no need to change your usual workflow! Just commit and go. 🚀

---

## 9. Conclusion 🎉

Look how far you’ve come! You now know how to generate keys, configure Git to use them, and paste them correctly into the services you use. Not bad, huh? 🚀  

With GPG keys, every commit becomes **your business card** (complete with that “Verified” badge), showing that you take security seriously in your workflow. Plus, having different keys for each account (personal, work, freelance...) keeps everything tidy and avoids mix-ups when you’re in the middle of a commit sprint.  

Now it’s time to celebrate: enjoy the feeling of having your commits signed and properly “verified” on any repo out there. And if you ever want to create new keys for other projects or accounts, you already know the drill. So go ahead and keep exploring the endless possibilities of Git and GPG — your commit history will thank you! ✨

---

## Who is Bruno Tanabe?

If you’ve made it this far and haven’t yet asked yourself “who the heck is this guy who made me set all this up?”, congrats on your patience! But if you’re curious, let me introduce myself real quick. 👋

I’m **Bruno Tanabe**, a developer focused on backend and artificial intelligence, always working on scalable and innovative solutions (or at least trying to). If you enjoyed the tutorial and want to connect, here’s how to reach me:

Find me here:

- [LinkedIn](https://www.linkedin.com/in/tanabebruno/)  
- [GitHub](https://github.com/BrunoTanabe)  
- [Email](mailto:tanabebruno@gmail.com)  
- [Medium](https://medium.com/@tanabebruno)  

Now we’re done for real! 🎯

---
