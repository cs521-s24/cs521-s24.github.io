---
layout: assignment
due: 2024-01-25 23:59:59 -0800
permalink: assignments/lab01.html
title: Lab01 - Environment Setup
github_url: https://classroom.github.com/a/7J8zbG0C
published: true
---

## Background

1. You will develop course assignments using Docker images on the `medusa.cs.usfca.edu` host
1. In order to connect to `medusa`, you will `ssh` through `stargate.cs.usfca.edu`, the CS department jump server.
1. To use `ssh`, you will set up an `ssh` keypair to connect securely
1. You will also use `ssh` to securely push your solutions to `github.com` using `git`

## Step 1: Configure `ssh` to use with `github.com`

1. Follow [these instructions](/docs/ssh-local-setup.html) to set up your `ssh` keypair on your laptop, and paste your public key onto `github.com`
1.  do that

## Step 2: Configure `ssh` to use with `stargate`

1. After you have `ssh` working between your laptop and `github.com` follow [these instructions](/docs/ssh-stargate-setup.html) to connect with the CS Labs network environment.


## Step 3: Finally, some code
1. Accept the GitHub assignment from the link above 
1. `ssh stargate`. Once you're on `stargate`, `ssh medusa`
1. Once you're on `medusa`, run the command `clab` to launch a Docker container where you can do work
1. Clone the assignment repository ("repo") into your home directory
    ```sh
    YOUR_USF_USERNAME@d122079067b8:~ $ git clone git@github.com:/cs521-s24/lab01-YOUR_GITHUB_USERNAME
    YOUR_USF_USERNAME@d122079067b8:~ cd lab01-YOUR_GITHUB_USERNAME
    ```
1. Compile the program
    ```sh
    YOUR_USF_USERNAME@d122079067b8:lab01-YOUR_GITHUB_USERNAME $ gcc -o hello hello.c
    ```
1. Run the program
    ```sh
    YOUR_USF_USERNAME@d122079067b8:lab01-YOUR_GITHUB_USERNAME $ ./hello
    hello world
    ```
1. Edit `hello.c` and change `"hello world\n"` to `"hello cs521\n"` in lower case exactly as shown
1. Save the file and recompile it
1. Commit your changes to the local repo on the lab machine
    ```sh
    YOUR_USF_USERNAME@d122079067b8:lab01-yourgithubid $ git commit -m"change world to cs521" hello.c
    ```
1. Push your changes from the local repo to the remote repo on `github.com``
    ```sh
    YOUR_USF_USERNAME@d122079067b8:lab01-yourgithubid $ git push
    ```
1. `^D` to log out of the Docker image, again to log out of `medusa`, and again to log out of `stargate`

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
