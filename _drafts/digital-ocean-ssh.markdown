---
layout: post
title:  "Deploying Django Cookiecutter with Docker on Digital Ocean"
categories: blog
---

These are the steps needed to deploy a Django-Cookiecutter project with Docker to a Digital Ocean droplet.

[Create your account](https://m.do.co/c/2bf12675e601) and by using that link, you'll get $10 credit.



## Get your root password

To access your droplet for the first time, get your root password to ssh into the instance. (I think DigitalOcean will email you the root password if you do not have SSH keys setup. I had previously setup my keys, so this section could be different than)

    sudo nano /etc/ssh/sshd_config
    PasswordAuthentication yes
    service ssh restart

    ssh root@<ip_address>

Once logged in, update the instance. For this example, I'm using an instance running Ubuntu 16.04.4.

    sudo apt-get update
    sudo apt-get -y upgrade
    sudo apt-get dist-upgrade

## Add your SSH Key & Disable PasswordAuthentication

After you've updated the instance, you'll want to secure your server by disabling password authentication. The way you'll access the server is with your SSH key.

    Generate your key
    ssh-copy-id root@<your_id_address>

Open a new terminal and make sure you can then ssh into the instance.

    ssh root@<ip_address>

Then you'll want to disable password authentication.

    sudo nano /etc/ssh/sshd_config
    PasswordAuthentication no
    service ssh restart

From this point you are all setup.
