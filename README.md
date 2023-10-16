# Configuring Git for Work and Personal Projects

This guide explains how to configure Git to work seamlessly with different signing keys and user profiles for both work and personal projects.

## Prerequisites

- Git installed on your system.
- Separate SSH keys for work and personal use. *(Optional)*
- GPG signing enabled for commits.
- The path to the GPG SSH program, in this case "/Applications/1Password.app/Contents/MacOS/op-ssh-sign."

## Step 1: Create a Global .gitconfig File

1. Create or edit the global Git configuration file in your home directory:

   ```bash
   $ nano ~/.gitconfig
   ```

1. Add the following to your global Git configuration:

    ```bash
    //.gitconfig

    [includeIf "gitdir:~/Code/Work/"]
    path = .gitconfig-work

    [includeIf "gitdir:~/Code/Personal/"]
    path = .gitconfig-personal

    [user]
    name = Your Name

    [gpg]
    format = ssh

    [gpg "ssh"]
    program = "/Applications/1Password.app/Contents/MacOS/op-ssh-sign"

    [commit]
    gpgsign = true

    [core]
    excludesfile = ~/.gitignore_global

    ```
1. Save and exit the text editor.

## Step 2: Create Separate Git Configuration Files

1. Create a file named ``.gitconfig-work`` in your home directory.

1. Add your work-specific Git configuration, including your work email address and the GPG SSH program path:

    ```bash
    //.gitconfig-work

    [user]
        name = Your Work Name
        email = your.work@email.com
    ```
1. For personal projects, follow the same steps as for work but create a file named ``.gitconfig-personal`` with your personal Git configuration.

1. Save and exit the text editor.

Now, Git will automatically load the appropriate configuration (work or personal) based on the repository's location. This setup ensures that you use the correct signing key and user profile for each project.

### More details

Git supports cascading configuration. Meaning it will build on top of existing configuration stored somewhere lower in the directory structure.

Three most common places to find and edit git configuration are:
- .gitconfig at system level
- .gitconfig at user level (overrides system level)
- .gitconfig at project level (overrides user level)

In order to see which configurations are active in the current context (directory) run `git config --list`.
