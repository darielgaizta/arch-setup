# SSH Key Guide

You probably encounter a problem with SSH because you haven't set anything for SSH on your Arch. Suppose you want to connect your GitHub account to your PC via SSH, then you should do the following:

1. Check whether you already have an SSH key, it is stored in your `.ssh` directory.
```
ls ~/.ssh
```

2. If you don't have one, generate a new SSH key for your PC locally:
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Note that `ed25519` is a type of cryptographic key. By doing the above command, now you should have a **private key** and a **public key** stored in your `.ssh` directory. The public key has an extension of `.pub` on its file name (e.g. ~/.ssh/id_ed25519.pub).

3. Start SSH agent and add your private key
```
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```
Here, the `ssh-agent -s` will print out a string of command to run SSH Agent in the background, which then will be executed by the terminal through `eval` command. So, `eval` was like: "Hey, terminal, I got this string, please run it for me!".

SSH Agent is a job (task, service, or anything you want to call it) that is responsible to store the decrypted private key so you don't have to reinput your passphrase. It also performs cryptographic on your behalf. So the way we do `ssh-add ~/.ssh/id_ed25519`, it means that we give our private key to the agent and let it stores it for us.

4. Lastly, put your public key to GitHub SSH Keys
```
cat ~/.ssh/id_ed25519.pub
```

Get your **public key** by running the above command.