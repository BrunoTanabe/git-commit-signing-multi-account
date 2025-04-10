# SIGNING COMMITS IN GIT WITH MULTIPLE ACCOUNTS: THE COMPLETE GUIDE (WINDOWS, LINUX, AND MACOS)

![Banner](./images/banner.png)

- [View on Medium](https://tanabebruno.medium.com/signing-commits-in-git-with-multiple-accounts-the-complete-guide-windows-linux-and-macos-026735f45f85)
- [View in Portuguese](README-PTBR.md)

If you’ve already tackled the challenge of setting up multiple SSH keys and now want to take a step further in securing and validating your commits, you’re in the right place! In this guide, we’ll pick up exactly where we left off in the [previous tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13), but now we’re diving into GPG keys for signing your commits. This way, you get that stylish “Verified” badge (way cooler than any Twitter checkmark) and make sure everyone knows it was really you who made the commit! 🤩

You know those companies that require signed commits, or that moment when you want to prove the code is genuinely yours (no cloning or hacking involved)? That’s where GPG becomes your best friend, ensuring integrity and authenticity. And of course, we’ll keep things light and fun: yes, it’s totally possible to enjoy learning how to configure two or more GPG keys without the headache. 🚀

Ready to get everything running smoothly and signed? Let’s go! ✋

![Verified Commit Example](./images/verified-commit.png)

**IMPORTANT**: This tutorial is part two of a series. If you haven’t read the first one yet, I recommend checking out [How to set up two or more SSH keys to use multiple Git accounts on the same computer? (Windows, Linux, and MacOS)](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) before continuing, because we’ll pick up where that one left off and you need to have done some of the configurations explained there. Plus, you’ll understand better how everything connects and it’ll be easier to follow. 😉

---

## Table of Contents 📌

**Let’s take a peek at what you’ll learn in this guide?** 🔍

- [SIGNING COMMITS IN GIT WITH MULTIPLE ACCOUNTS: THE COMPLETE GUIDE (WINDOWS, LINUX, AND MACOS)](#signing-commits-in-git-with-multiple-accounts-the-complete-guide-windows-linux-and-macos)
  - [Table of Contents 📌](#table-of-contents-)
  - [1. What are GPG keys? 🤔](#1-what-are-gpg-keys-)
  - [2. Why set up more than one GPG key? 🔒](#2-why-set-up-more-than-one-gpg-key-)
  - [3. Prerequisites: ensuring GPG is installed 🔧](#3-prerequisites-ensuring-gpg-is-installed-)
    - [Windows](#windows)
    - [Linux](#linux)
    - [MacOS](#macos)
  - [4. Generating new GPG keys 🔑](#4-generating-new-gpg-keys-)
    - [Windows, Linux, and MacOS](#windows-linux-and-macos)
    - [IMPORTANT](#important)
  - [5. Setting Up Git to Use the Correct GPG Keys 🔧](#5-setting-up-git-to-use-the-correct-gpg-keys-)
    - [Windows, Linux, and macOS (common steps)](#windows-linux-and-macos-common-steps)
    - [Windows](#windows-1)
    - [Linux and macOS](#linux-and-macos)
  - [6. Copying Your GPG Keys to Add Them to Services ☁️](#6-copying-your-gpg-keys-to-add-them-to-services-️)
    - [Windows, Linux, and MacOS](#windows-linux-and-macos-1)
    - [OPTIONAL](#optional)
  - [7. Adding GPG Keys to Services (GitHub, GitLab, Bitbucket, etc) ☁️](#7-adding-gpg-keys-to-services-github-gitlab-bitbucket-etc-️)
    - [GitHub](#github)
    - [GitLab](#gitlab)
    - [BitBucket](#bitbucket)
  - [8. How to Sign Commits ✍️](#8-how-to-sign-commits-️)
    - [Signing Commits Automatically](#signing-commits-automatically)
    - [Signing Commits Manually](#signing-commits-manually)
  - [9. Additional Settings and Troubleshooting 🛠️](#9-additional-settings-and-troubleshooting-️)
  - [10. Conclusion 🎉](#10-conclusion-)
  - [11. References 📚](#11-references-)
  - [Who is Bruno Tanabe?](#who-is-bruno-tanabe)

---

## 1. What are GPG keys? 🤔

Think of **GPG (GNU Privacy Guard)** as a cryptographic superhero that not only protects your identity when committing but also guarantees the integrity of what’s being sent. Instead of just proving “who you are,” it shows that it was **exactly** you who signed that commit — no chance of fraud or sneaky hackers. 🕵️‍♂️

When you sign a commit with GPG, you get that **authenticity badge** (the “Verified”) that makes everything look way more professional. It’s like putting a **strong lock** on your commits, showing everyone they’re legit and truly yours.

And why is this so cool? Because besides boosting trust in the project’s history, you avoid the mess of someone pretending to be you — and you can also separate personal from work just by **switching keys**! Picture it like a “Clark Kent” (your work login) and “Superman” (your personal account) kind of deal, each with its own signature. ⚡️

In short: GPG gives your commits that extra touch of security and credibility. Want your commits to scream “this is serious and it’s really mine”? Then let’s add GPG keys to your Git setup and soar off in pursuit of safer commits! ✨

---

## 2. Why set up more than one GPG key? 🔒

If you’ve ever had to deal with multiple Git accounts (for personal projects, work, or clients), you probably already know that **organization** is key to keeping your sanity. Now, when it comes to **GPG keys**, we’re leveling up: you don’t just want to prove it’s *you* in the commits, but also prove which *account* each commit is coming from, right?

Imagine the scenario:

- 💼 Your **work account** needs that verified signature, showing commits officially came from your team or company.  
- 🏠 Your **personal account** signs each commit with its own key, adding more security and authenticity to your projects.  

Having different GPG keys for each of these accounts is the most practical way to **separate** (and sign) what’s work and what’s personal. And the best part? No Git confusion, no needing to constantly tweak settings, and of course, with that “Verified” badge that gives everything a pro look.

Instead of messing around copying/pasting keys, you set each one up properly and that’s it: when it’s time to sign, Git knows exactly which one to use. That way, in your work repo, your commits are clearly “official,” and in your personal projects, the signature comes from another “you” (but still you — just keeping things tidy).

And let’s be honest — when it comes to **security**, isolating each “environment” is never a bad idea. So if you liked the idea of making sure no one can impersonate you (even just for a joke in your repo), let’s get started with setting up those GPG keys and get everything flowing… and **signed**! ✍️✨

---

## 3. Prerequisites: ensuring GPG is installed 🔧

Before creating your keys and giving your commits that top-tier signature, we need to make sure **GPG** is installed on your machine and ready for action. After all, without our cryptographic superhero’s tool, there’s no show. 🎉

The good news is, installation is super simple:

### Windows

[Go to the official **Gpg4win** download page](https://gpg4win.org/get-gpg4win.html).

After downloading, click the `.exe` file and run it as **Administrator**.

You’ll get the classic installer full of “Next” buttons. When you get to the screen asking which components to install, pick only GnuPG. That’s the one that does the magic — Kleopatra and GpgOL are nice extras but not needed for signing commits. Uncheck them and move on. 🚀

Once done, open your terminal (**Command Prompt or PowerShell**) and type:

```bash
   gpg --version
```

If a GPG version number shows up, success! You’re ready to go signing commits with a cape on. 🚀

### Linux

Open your terminal and try:

```bash
   gpg --version
```

If you get a version, great — you’re all set. If not, just install it:

```bash
   sudo apt-get install gnupg
```

(Or use your distro’s package manager, like `yum`, `dnf`, etc.) Five minutes tops and you’re good. 🔧

### MacOS

Open Terminal and type:

```bash
   gpg --version
```

If it returns a version number, great. If not, you can install it using [Homebrew](https://brew.sh/):

```bash
   brew install gnupg
```

In just a moment, you’ll be ready. 🍏

Done! With GPG **officially** good to go and ready to secure your work, the verified commits party can go on. Now let’s move on to actually configuring your GPG keys. Let’s do it! ✨

---

## 4. Generating new GPG keys 🔑

Now that we’ve got GPG installed and ready to roll, it’s time to create the GPG keys that’ll give your commits that special touch. Don’t worry — the process is smooth and quick! Let’s go? 🚀

As you saw in the [previous tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) about **SSH** keys, I like to organize keys in a specific folder at the root of my user directory. That helps keep everything neat and makes it easier to find your keys. But for GPG keys, they don’t create files in your current folder — instead, they’re stored in the `~/.gnupg` folder. So don’t worry about that. GPG will create the folder automatically when you generate the key. Even better: no need to place keys in specific folders — GPG handles that for you. So relax, and let’s go! 😉

### Windows, Linux, and MacOS

Let’s go step-by-step. This works the same on Windows, Linux, and MacOS — no system-specific tweaks here:

This step is simple — just **generate the GPG keys**. Like in the [previous tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13), I’ll create two GPG keys, one for each of my accounts: a ‘personal’ one and a ‘work’ one. If you have more than two accounts, just create one key for each — the process is identical.

```bash
    gpg --full-generate-key
```

At this point, GPG will ask you a series of questions. Just pick the options that make the most sense for you. Here’s what I chose:

- **Key type**: (1) RSA and RSA *Not the default — the `(9) ECC (sign and encrypt)` doesn’t work well on Windows*
- **Key size**: 4096
- **Expiration**: (0) Never expires *default* (If you pick an expiration date, you’ll need to generate a new key once it expires.)

### IMPORTANT

The last three options are the most important — pay attention:

- **Name**: This is the name that’ll show up in your commits. I recommend using the same name as on your GitHub, GitLab, Bitbucket, or whatever service you’re using. That’ll make it easier to identify your commits.
- **Email**: You **MUST** use the email linked to your GitHub, GitLab, Bitbucket, or whatever account you’re using. If you don’t use the correct email, GPG won’t be able to verify your commits and you’ll miss out on the “Verified” badge. So be careful here! 😉
- **Comment**: This field is optional and not that important — it’s only marked important to keep the tutorial’s structure. You can leave it blank or put something meaningful to you.

Now I’ll repeat the process for the second key, which will be for my work account. The process is the same, just use your other account’s **name** and **email**.

```bash
    gpg --full-generate-key
```

You can choose the same options as before, just remember to use your work account’s name and email.

*Repeat the process as many times as needed to create all the keys you need.*

---

## 5. Setting Up Git to Use the Correct GPG Keys 🔧

You already have your GPG keys ready to go, and now it’s time to make Git recognize these beauties. Don’t worry, the process is super simple! Ready? Let’s go! 🚀

Remember in the last [tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) we created a `.gitconfig` file for each account? Now we’re going to add the GPG keys to that file. The process is the same, but this time we’re adding the GPG key instead of the SSH key.

Here’s the step-by-step:

### Windows, Linux, and macOS (common steps)

First, you need to find out the ID of the GPG key you just created. To do that, just run the following command:

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

You’ll have one key for each of your accounts. What you need to do now is copy the ID of each key. The key ID is the part between the slash `/` and the space. In the example above, the personal key ID is `8AEDA33EA0CA3AF6`, and the work key ID is `5A3F4B2D7E8C9A88`.

Remember that [tutorial](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13) where we created a `.gitconfig` file for each account? Now we’re going to add the GPG key to that file. Same process, just swapping SSH for GPG.

In the terminal, access the `.gitconfig` file for the account you want to add the GPG key to. In my case, each account’s `.gitconfig` file is in the `.git` folder in my home directory (as we set up in the last tutorial). So the next step is to go into that folder with:

```bash
    cd ~/.git
```

Now let’s edit the `.gitconfig` file for the account you want to add the GPG key to. This part of the tutorial will vary depending on your operating system. Let’s go:

### Windows

Open the file with **Notepad** (or whichever editor you prefer):

```bash
notepad .gitconfig-personal
```

Inside the file, you’ll add the line `signingkey = 8AEDA33EA0CA3AF6`, replacing it with that account’s key ID. The file will look like this:

```ini
[user]
   name = Bruno Tanabe Personal
   email = brunotanabe@personal.com
   signingkey = 8AEDA33EA0CA3AF6
[core]
   sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**But Tanabe, how will I know which ID belongs to which account?**  
Simple! When you created the key, you included the name and email of the account you wanted. So just check the key ID and see what name and email are attached to it. That’s how you’ll know which key ID belongs to which account. But what if the accounts have the same name and email? In that case, it doesn’t matter—you can use the same ID for both accounts or choose either of the two keys. What matters is knowing which ID belongs to which account.

Perfect! Now do the same for your work account. The process is exactly the same, but now you’ll add the GPG key for the work account. So, open the work account’s `.gitconfig` file:

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

Just repeat the process for each of your accounts. Done! Now your GPG keys are all set up and ready to give your commits that special signature. 🚀

### Linux and macOS

Open the file with **nano** (or whichever editor you prefer):

```bash
nano .gitconfig-personal
```

Inside the file, you’ll add the line `signingkey = 8AEDA33EA0CA3AF6`, replacing it with that account’s key ID. The file will look like this:

```ini
[user]
   name = Bruno Tanabe Personal
   email = brunotanabe@personal.com
   signingkey = 8AEDA33EA0CA3AF6
[core]
   sshCommand = "ssh -i ~/.ssh/personal_ssh_key"
```

**But Tanabe, how will I know which ID belongs to which account?**  
Simple! When you created the key, you included the name and email of the account you wanted. So just check the key ID and see what name and email are attached to it. That’s how you’ll know which key ID belongs to which account. But what if the accounts have the same name and email? In that case, it doesn’t matter—you can use the same ID for both accounts or choose either of the two keys. What matters is knowing which ID belongs to which account.

Perfect! Now do the same for your work account. The process is exactly the same, but now you’ll add the GPG key for the work account. So, open the work account’s `.gitconfig` file:

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

Just repeat the process for each of your accounts. And that’s it! Your GPG keys are now set up and ready to give your commits that special touch. 🚀

---

## 6. Copying Your GPG Keys to Add Them to Services ☁️

Now that you have your GPG keys set up, it’s time to copy them and paste them into the services you use (GitHub, GitLab, Bitbucket, etc.). It’s super easy: these services only need the **public key** to verify your commits. So just copy that part of the GPG key and paste it into your platform of choice — and boom, you’ll have that “Verified” badge in no time! 🚀

### Windows, Linux, and MacOS

Remember the key ID you used to set up Git? Now it’s time to use it to copy the public key. The command is the same across all operating systems—just plug in the key ID you want to copy. For example, if the key ID is `8AEDA33EA0CA3AF6`, the command will be:

```bash
gpg --armor --export 8AEDA33EA0CA3AF6
```

This command will generate a public key that you can copy and paste into the platform of your choice. The output will look something like this:

```bash
   -----BEGIN PGP PUBLIC KEY BLOCK-----

   4bOkOJy0eUJydW5vIFRhbmFiZSAoRmVpdG8gY29tIGFtb3I/IE7ilJzDum8sIGZl
   d2p8u1j/Arg4BGfrUlcSCisGAQQBl1UBBQEBB0BYYWYdzHtrGMIPo/Dk1cgc0JPo
   b3IuIGNvbSBkZWRpY2HilJzCuuKUnMO6by4gUG9yIEJydW5vIFRhbmFiZSEpIDxi
   ruSgH33JThIPRlDurrzjPSIIeSHAP47x6f29Lrm7w0ksdYfxVQ1fo/e/+V2mtNPb
   QJn61JXAhsMAAoJEOXVOzy94AH7VjIBALW9dBGGjjM1GWRMcCEECvHV57IJgoBuG
   brVfpcaPCs/1IAMBCAeIeAQYFgoAIBYhBC8CfJ+0aWPB5M2J2uXVOzy94AH7BQJn
   94AH7BQJn61JXAhsDBQsJCAcCAiICBhUKCQgLAgQWAgMBAh4HAheAAAoJEOXVOzy9
   W9dBGGjjM1GWRMcCEECvHV57IJgoBuGGbT942xT4SbAP441tlp5bLy7EobHSOHmk
   Z+tSVxYJKwYBBAHaRw8BAQdARcc22jcKOHSJjLYQCga9nG0nnLqWvDhaPfWz
   nLqWvDhaPfWzZ+tSVxYJKwYBBAHaRw8BAQdARcc22jcKOHSJjLYQCga9nG0
   CF8xYhBC8CfJ+0aWPB5M2J2uXVOzy94AH7BQJn61JXAhsMAAoJEOXVOzy94AH7Vj
   McCEECvHV57IJgoBuGGbT942xT4SbAP441tlp5bLy7EobHSOHmkeqiiDbfRhnlJl
   Tf0bkK+GAw==W9dBGGjjM1GWRMc
   -----END PGP PUBLIC KEY BLOCK-----
```

You should copy everything from `-----BEGIN PGP PUBLIC KEY BLOCK-----` to `-----END PGP PUBLIC KEY BLOCK-----`. And done! Just paste that into the platform of your choice and get that sweet “Verified” badge on your commits. 🚀

If you have more than one key, just repeat the process for each one. Don’t worry, the process is the same—the only thing that changes is the key ID. So if you have two keys, just run the command twice, once for each key. If I were to run the command for my work key, it would look like this:

```bash
gpg --armor --export E6BF4F45C3ADD6950420C1D4F94F3E72C3DD5962
```

I recommend copying each key and adding it to the respective service right away—so alternate between steps 7 and 8. 🔄

### OPTIONAL

If you don’t remember your key ID, use the following command to list info for all your GPG keys:

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
uid                 [ultimate] Bruno Tanabe (My Work Key) <brunotanabe@work.com>
ssb   cv25519/87A3F4B283ER49A 2024-10-24 [E] [expires: 2025-10-24]
```

You’ll have one key for each of your accounts. What you need to do now is copy the ID of each key. The key ID is the part between the slash `/` and the space. In the example above, the personal key ID is `8AEDA33EA0CA3AF6`, and the work key ID is `5A3F4B2D7E8C9A88`.

Once you’ve noted the key, just follow the steps in `Copying Your GPG Keys to Add Them to Services` again, but now using the correct ID. And you’re all set!

---

## 7. Adding GPG Keys to Services (GitHub, GitLab, Bitbucket, etc) ☁️

Good news: everything is already set up on your computer! Now there's just one final step to make everything work smoothly — letting your version control services (GitHub, GitLab, Bitbucket, or any other) know that you have a GPG key and that they can use it to sign your commits. This is super simple and quick; you just need to paste the public key you copied in the previous step. 🖥️✨

Now that you've copied your keys, let’s paste them into your favorite service:

Below, you’ll see how to add the keys to the main code versioning services, but if you use a different one, just find a similar section and add your keys there.

### GitHub

1. Go to: [https://github.com/settings/keys](https://github.com/settings/keys)  
2. Click **New GPG key**.  
3. Name your key (e.g., **Personal** or **Work**).  
4. Paste the contents of your public key into the **Key** field.  
5. Click **Add GPG key**. All done! ✅

### GitLab

1. Go to: [https://gitlab.com/-/profile/gpg_keys](https://gitlab.com/-/profile/gpg_keys)  
2. In the **Key** field, paste your public key.  
3. Give it a title to identify it (e.g., **Personal** or **Work**).  
4. Click **Add key**. 🔑

### BitBucket

1. Go to: [https://bitbucket.org/account/settings/gpg-keys/](https://bitbucket.org/account/settings/gpg-keys/)  
2. Click **Add key**.  
3. In the **Label** field, give your key a name.  
4. In the **Key** field, paste your public key.  
5. Save. 💾

And that’s it! Now your GPG keys are added to the services, and you can start signing your commits with them. 🚀

---

## 8. How to Sign Commits ✍️

Now that you’ve configured your GPG keys and added them to your services, it’s time to learn how to sign your commits. Don’t worry, the process is pretty simple! Let’s go? 🚀

You can sign your commits in two ways: **automatically** or **manually**. I’ll show you how to do both, so you can pick whichever suits you best. 😉

### Signing Commits Automatically

To sign your commits automatically, just run the following command in the terminal:

```bash
   git config --global commit.gpgSign true
```

This command basically adds the following line to your `.gitconfig` file:

```ini
   [commit]
      gpgSign = true
```

That way, every commit you make will automatically be signed with the GPG key you’ve configured. And the best part: you don’t have to change anything in your workflow! Just commit as usual and you’re done. 🚀

### Signing Commits Manually

If you don’t want to sign every single commit, you can sign commits manually (I can’t imagine why you wouldn’t want to sign all your commits, but hey — some developers are quirky). To do this, just add the `-S` flag to the commit command:

```bash
   git commit -S -m "Commit message"
```

This command will sign the commit using the GPG key you configured. And again, you can use this command in any repository — no need to change anything in your usual flow! Just commit like always and boom. 🚀

---

## 9. Additional Settings and Troubleshooting 🛠️

Setting up GPG keys is usually smooth, but sometimes things can go sideways (especially on Windows 😠). So here are a few extra settings and troubleshooting tips to help you fix any hiccups you might hit along the way. 💡

Sometimes your computer can’t find GPG, and this might happen for a few reasons. A simple solution in many cases is to add the GPG path to your `.gitconfig` file. To do this, just run the following command, replacing the path with the correct one for your GPG (the default GPG path on Windows is `C:/Program Files (x86)/GnuPG/bin/gpg.exe`):

```bash
   git config --global gpg.program "C:/Program Files (x86)/GnuPG/bin/gpg.exe"
```

Now that you understand a bit more about GPG, you can also add this line manually to your `.gitconfig` file. Just open the file and add:

```ini
   [gpg]
      program = C:/Program Files (x86)/GnuPG/bin/gpg.exe
```

---

## 10. Conclusion 🎉

Look at how far you’ve come! You now know how to generate keys, configure Git to use each of them, and paste everything properly into the services you use. Not bad, huh? 🚀  

With GPG keys, each commit becomes **your business card** (complete with a “Verified” badge and all), showing that you take security seriously in your workflow. Plus, having different keys for each account (personal, work, freelance...) keeps things organized and avoids confusion when you’re in the zone committing like crazy.

Now it’s time to enjoy the feeling of having your commits signed and fully “verified” across any repo. And if you ever want to create new keys for other projects or accounts, you already know the way. So go on and keep exploring the endless possibilities of Git and GPG — your commit history will thank you! ✨

---

## 11. References 📚

- [GPG Documentation](https://www.gnupg.org/documentation/manuals/gnupg/)  
- [Use GPG keys to sign commits](https://support.atlassian.com/bitbucket-cloud/docs/use-gpg-keys-to-sign-commits/)  
- [How to set up two or more SSH keys to manage multiple Git accounts on the same computer (Windows, Linux, and MacOS)](https://medium.com/@tanabebruno/como-configurar-duas-ou-mais-chaves-ssh-para-ter-diversas-contas-git-no-mesmo-computador-b9567621ce13)

---

## Who is Bruno Tanabe?

If you’ve made it this far and still haven’t asked yourself “who the heck is this guy who made me set all this up?”, congrats on your patience! But if you’re curious, let me introduce myself real quick. 👋

I’m **Bruno Tanabe**, a developer focused on backend and artificial intelligence, always working on scalable and innovative solutions (or at least trying to). If you enjoyed the tutorial and want to chat, here’s how to reach me:

Find me here:

- [LinkedIn](https://www.linkedin.com/in/tanabebruno/)  
- [GitHub](https://github.com/BrunoTanabe)  
- [Email](mailto:tanabebruno@gmail.com)  
- [Medium](https://medium.com/@tanabebruno)

Now yes — mission accomplished! 🎯

---
