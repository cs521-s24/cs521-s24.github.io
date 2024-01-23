---
layout: default
permalink: docs/ssh-stargate-setup.html
title: SSH Stargate Setup
---

## Step 0: Set up your terminal environment

1. If you are not familiar with the Unix shell, please review my [Shell Basics](https://github.com/usfca-cs-tools/docs/blob/main/shell-basics.md) document.
1. Terminal setup (<a onclick="toggle_display('terminal_mac')">Mac</a>, <a onclick="toggle_display('terminal_win')">Windows</a>)

    <div id="terminal_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    - Apple's Terminal app should work ok
    - I prefer [iTerm2](https://iterm2.com/) because it works well with my preferred terminal-mode editor, [micro](https://iterm2.com/)
    </div>

    <div id="terminal_win" class="div-toggle" style="display:none" markdown=1>
    For Windows:
    - I recommend using [Git For Windows](https://gitforwindows.org/). Git Bash offers a Unix-like shell environment.
    - If you already have [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install), that's also fine
    </div>

1. You may use the terminal-mode editor of your choice (e.g. micro, nano, vim, emacs)
## Step 1: Set up `ssh` to connect to `stargate.cs.usfca.edu`

1. From your laptop, edit `~/.ssh/config` and add these lines (<a onclick="toggle_display('config_mac')">Mac</a>, <a onclick="toggle_display('config_win')">Windows</a>)

    <div id="config_mac" class="div-toggle" style="display:none" markdown=1>
    For Mac:
    ```
    Host stargate
      AddKeysToAgent yes
      ForwardAgent yes
      # HostName 138.202.168.64
      HostName stargate.cs.usfca.edu
      User YOUR_USF_USERNAME
      UseKeychain yes
    ```
    </div>

    <div id="config_win" class="div-toggle" style="display:none" markdown=1>
    For Windows:
    ```
    Host stargate
      AddKeysToAgent yes
      ForwardAgent yes
      #  HostName 138.202.168.64
      HostName stargate.cs.usfca.edu
      User YOUR_USF_USERNAME
    ```
    </div>

1. From your laptop, copy your public key to `stargate``
    ```sh
    $ ssh-copy-id stargate
    ```
    You should answer "yes" to this question
    ```
    The authenticity of host 'stargate.cs.usfca.edu (138.202.168.64)' can't be established.
    ED25519 key fingerprint is SHA256:Xs9bYMh0ClrRptx1JjkPf0g9QmaF+a49xKRU21S+91Y.
    This key is not known by any other names
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```
    
1. Your default password for `stargate` is your student ID (CWID). Your CWID will not be shown (in case someone was watching over your shoulder) but just type it followed by the Return/Enter key.
    1. Be careful not to type the wrong student ID three times. If you do, your account will be locked until unlocked by the [CS Support team](mailto:support@cs.usfca.edu)

1. Once connected to `stargate`, type `^D` (aka `CTRL-D`) to log out of `stargate`

1. From your laptop, you should be able to connect without being prompted for a password, thanks to the `ssh` handshake. 
    ```
    $ ssh stargate
    ```
    
    If you are prompted for the passphrase for your private key, you probably don't have the `ssh-agent` setup correct (especially for Windows, where this is complex)

## Step 2: Set up `ssh` from the lab environment to `github.com`

1. From `stargate` edit `~/.ssh/config`` and enter the following text
    ```ssh
    Host *
      ForwardAgent yes
    ```
1. From `stargate` test `ssh` to `github.com`
    ```sh
    $ ssh git@github.com
    ```
1. Answer "yes" to this question
    ```sh
    $ ssh git@github.com
    The authenticity of host 'github.com (192.30.255.113)' can't be established.
    ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
    This key is not known by any other names
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```
    If successful, you expect to see this reply
    ```
    Hi YOUR_GITHUB_USERNAME! You've successfully authenticated, but GitHub does not provide shell access.
    Connection to github.com closed.
    ```

## Step 3: Choose one of the lab systems to work on
1. **Do not do class work on the stargate host.** SSH to one of the lab hosts listed by `rusers`
    ```sh
    YOUR_USF_USERNAME@stargate:~ $ rusers
    vlab01.cs.usfca.edu
    vlab02.cs.usfca.edu
    ...
    $ ssh vlab01
    YOUR_USF_USERNAME@vlab01:~ $ 
    ```

## Step 4: Configure `git` in the lab environment

1. From a lab host, add your name and email address so that `git push` knows who you are
    ```sh
    $ git config --global user.name "YOUR_FIRST_NAME YOUR_LAST_NAME"
    $ git config --global user.email "YOUR_USF_USERNAME@dons.usfca.edu"
    ```
1. Configure your `git` merge strategy (more on this later)
    ```sh
    $ git config --global pull.rebase false
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
