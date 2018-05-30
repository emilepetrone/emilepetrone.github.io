---
layout: post
title:  "Deploying Django Cookiecutter with Docker on Digital Ocean"
categories: blog
---

These are the steps needed to deploy a Django-Cookiecutter project with Docker to a Digital Ocean droplet.

[Create your account](https://m.do.co/c/2bf12675e601) and by using that link, you'll get $10 credit.


# Why Digital Ocean

The decision on where to deploy your Cookiecutter project ultimately comes down to: Do you want to save money and manage your backend yourself? If so, it will be a much cheaper bill at the end of the month - but will take more of your time.

Out of the box Cookiecutter can be setup to deploy on Heroku. It is fast and easy to setup. The downside is you'll pay for it. Your Heroku bill quickly adds up as you add new services and your database grows.

Instead of paying for Heroku, you can deploy to a VPS. I chose Digital Ocean because it has great documentation for Django projects. The downside, you'll have to manage your droplets yourself.


## Add Domain to Digital Ocean

I've found it to be much easier to manage my domain's DNS settings in DigitalOcean's DNS console, so to point your domain to DigitalOcean, add the Digital Ocean name servers to your domain.

    ns1.digitalocean.com
    ns2.digitalocean.com
    ns3.digitalocean.com

For more in depth information, DigitalOcean has a longer ["Introduction to Managing DNS."](https://www.digitalocean.com/community/tutorials/an-introduction-to-digitalocean-dns#digitalocean-dns-at-a-glance)


### Create an access token

Once logged in, click the API link in the header. On this page, you'll see a button "Generate New Token". This will let you utilize the Digital Ocean API for setting up a new droplet.

### Create your droplet

A Digital Ocean droplet is the VPS ([virtual private server](https://en.wikipedia.org/wiki/Virtual_private_server)) you'll be deploying your project to. This is the command to create this droplet running Ubuntu.

    docker-machine create -d digitalocean --digitalocean-access-token=<your_access_token> prod

Note: "prod" is the name I'm assigning to the droplet but you can name it whatever you like.

### Point Domain to the droplet

You'll see the droplet in your DigitalOcean Dashboard. Once set up, there will be an IP address for the machine.

Copy the IP address and on your Domain, add an A record to this IP address.

## Build your Docker Images and deploy

eval $(docker-machine env prod)
docker-compose -f production.yml build
docker-compose -f production.yml up -d


## Make sure

-d

Those 2 characters are a gotcha. If you do not include them, you'll run the image in your terminal. When you CTRL+C, it will kill the processes.

-d will run your image in detach mode
