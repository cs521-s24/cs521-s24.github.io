---
layout: default
title: SSH Local Setup
---

1. You need to be able to run `git` from your laptop, and `git` uses `ssh` to communicate with `github.com`
1. If you already have `ssh` keys and you can use them with `github.com` you can skip to Step 3. To check, try to `ssh` to `github.com` and ensure that you get the output shown below
    ```sh
    $ ssh git@github.com
    Hi username! You've successfully authenticated, but GitHub does not provide shell access.
    Connection to github.com closed.
    ```
1. If you can not successfully authenticate to `github.com` then follow the remaining `ssh` setup steps
1. Create the ssh directory (it's ok if it already exists)
    ```sh
    $ mkdir ~/.ssh
    ```
1. `cd` into the ssh directory
    ```sh
    $ cd ~/.ssh
    ```
1. Look for an ssh key pair in that directory
    ```sh
    $ ls
    id_ed25519 id_ed25519.pub
    ```
    `id_ed25519.pub` is your public key and can be shared with `github.com` or other servers. `id_ed25519` is your private key and should not be shared with anyone.
1. If you do not have a key pair, you should create them (substituting your own email address)
    ```sh
    $ ssh-keygen -t ed25519 -C "YOUR_USF_USERNAME@dons.usfca.edu"
    ```
    1. When `ssh-keygen` asks you to choose a filename, just hit return to take the default filename
    1. When `ssh-keygen` asks you to choose a passphrase for your private key, use a passphrase you will remember. Do not forget this passphrase!
1. Configure `ssh` on your laptop
    1. Create/edit the file named `~/.ssh/config` to add the following text (<a onclick="toggle_display('ssh_config_mac')">Mac</a>, <a onclick="toggle_display('ssh_config_win')">Windows</a>)

    <div id="ssh_config_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    ```
    Host github.com
      AddKeysToAgent yes
      ForwardAgent yes
      IdentityFile ~/.ssh/id_ed25519
      UseKeychain yes
      User YOUR_GITHUB_USERNAME
    ```
    </div>

    <div id="ssh_config_win" class="div-toggle" style="display:none" markdown=1>
    For Windows Git Bash:
    ```
    Host github.com
      AddKeysToAgent yes
      ForwardAgent yes
      IdentityFile ~/.ssh/id_ed25519
      User YOUR_GITHUB_USERNAME
    ```
    </div>
1. Setup `ssh-agent`. The `ssh-agent` program runs in the background, waiting for an authentication request to verify using your private key. `git clone` and `git push` use ssh authentication, and `ssh-agent` does the work. (<a onclick="toggle_display('ssh_agent_mac')">Mac</a>, <a onclick="toggle_display('ssh_agent_win')">Windows</a>)

    <div id="ssh_agent_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    - Nothing to do. macOS runs `ssh-agent` automatically
    </div>

    <div id="ssh_agent_win" class="div-toggle" style="display:none" markdown=1>
    For Windows Git Bash:
    1. Edit `~/.bashrc` to include these lines
        ```sh
        env=~/.ssh/agent.env

        agent_load_env () { test -f "$env" && . "$env" >| /dev/null ; }

        agent_start () {
            (umask 077; ssh-agent >| "$env")
            . "$env" >| /dev/null ; }

        agent_load_env

        # agent_run_state: 0=agent running w/ key; 1=agent w/o key; 2=agent not running
        agent_run_state=$(ssh-add -l >| /dev/null 2>&1; echo $?)

        if [ ! "$SSH_AUTH_SOCK" ] || [ $agent_run_state = 2 ]; then
            agent_start
            ssh-add
        elif [ "$SSH_AUTH_SOCK" ] && [ $agent_run_state = 1 ]; then
            ssh-add
        fi

        unset env
        ```
    1. Save and exit the editor. Then reload your shell environment
    ```sh
    $ source ~/.bashrc
    ```
    </div>
1. Copy your public key to the clipboard (<a onclick="toggle_display('clipboard_mac')">Mac</a>, <a onclick="toggle_display('clipboard_win')">Windows</a>)

    <div id="clipboard_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    ```sh
    $ cat id_ed25519.pub | pbcopy
    ```
    </div>

    <div id="clipboard_win" class="div-toggle" style="display:none" markdown=1>
    For Windows Git Bash:
    - Open Notepad, File > Open, navigate to c:\Users\YOUR_WINDOWS_USERNAME\.ssh
    - Open your public key (`id_ed25519.pub`)
    - Select All, and Copy it to the clipboard
    </div>
1. Paste your public key into your `github.com` account
    1. Create an account on [github.com](https://github.com) if you don't already have one
    1. Go to Profile > Settings > SSH and GPG Keys and click a New SSH key
    1. Give the key a Title, and paste the contents of the clipboard into the Key box
1. To test that the preceding steps were successful
    1. Close the terminal you were using, open a new one, and type
        ```sh
        $ ssh git@github.com
        PTY allocation request failed on channel 0
        Hi YOUR_GITHUB_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
        Connection to github.com closed.
        ```

<script>
    function toggle_display(id_name) {
        var e = document.getElementById(id_name);
        if (e.style.display === "none") {
            e.style.display = "block";
        } else {
            e.style.display = "none";
        }
    }
</script>
