# How to sign-off commits

Print maker Lab requires a sign-off message in the following format appear on each commit in the pull request:

```text
This is my commit message

Signed-off-by: Random J Developer <random@developer.example.org>
```

The text can either be manually added to your commit body, or you can add either `-s` or `--signoff` to your usual git commit commands.

#### Creating your signoff

Git has a `-s | --signoff` command-line option to append this automatically to your commit message:

```bash
git commit --signoff --message 'chore: this is my commit message'
```

```bash
git commit -s -m "chore: this is my commit message"
```

This will use your default git configuration which is found in `.git/config` and usually, it is the `username systemaddress` of the machine which you are using.

To change this, you can use the following commands (Note these only change the current repo settings, you will need to add `--global` for these commands to change the installation default).

Your name:

```bash
git config user.name "FIRST_NAME LAST_NAME"
```

Your email:

```bash
git config user.email "MY_NAME@example.com"
```

#### How to sign-off commits using GPG, SSH
If your Git version is less than **2.34.0** (or if you just prefer GPG-signing anyway) you need to supply a gpg-key for signing.

```bash
git --version
```

There are many articles on how to generate and add a gpg-key to your hosted Git service, so we will leave that part to you (See, for example [GitHub's guide](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)):

Add the -S or the --gpg-sign flag to your commits:
```bash
git commit --gpg-sign -m 'chore: this will sign your commit'
```


Git introduced signing with ssh-keys from **2.34.0 and upwards**. This simplifies life, as you most likely already have a ssh-key for your Git chores, and don't need to keep track of an extra gpg-key.
The ssh feature also needs a fairly modern openssh version,8.8++, and finally, for visual candy your signatures are visually shown.
Note: Using gpg-keys after Git 2.34.0 is still perfectly fine.

Configure git to use ssh-key for signing instead of gpg:
```bash
git config --global gpg.format ssh
```

Give it your public ssh-key, inline or filepath:
```bash
git config --global user.signingKey 'path/to/yourkey.pub'
```

For more information you can read the [GitHub's guide](https://docs.github.com/en/authentication/managing-commit-signature-verification/telling-git-about-your-signing-key)

When committing changes in your local branch, add the -S flag to the git commit command:
```bash
git commit -s -m "chore: this is my commit message"
```


#### How to sign-off via Visual Studio Code

You can tell VS Code to append the -s flag to the git commit command, to use signed committing.
If you are using GPG or SSH sign-off, then open the settings, search for “gpg” and check the box “Enables commit signing with GPG”.
![Screenshot_GPG](vs_code_always_sign_off_gpg.png)
Alternatively you can add this line to your settings.json :
```
"git.enableCommitSigning": true
```

Overwise, open the settings, search for “sign-off” and check the box “Enables commit signing with GPG”.
![Screenshot](./assets/vs_code_always_sign_off.png)

Alternatively you can add this line to your settings.json :
```
"git.alwaysSignOff": true
```

#### How to amend a sign-off

If you have authored a commit that is missing the signed-off-by line, you can amend your commits and push them to GitHub

```bash
git commit --amend --signoff
```

If you've pushed your changes to GitHub already you'll need to force push your branch after this with `git push -f`.


#### DCO Failures

If you miss series of commits, you can use the rebase with `-i | --interactive` to edit and append into.
For example, if you have 4 commits in your history (Note the ~4):
???+ Example

    If you have 4 commits in your history.

    ```bash
    git rebase --interactive HEAD~4
    (interactive squash + DCO append)
    git push origin --force
    ```
