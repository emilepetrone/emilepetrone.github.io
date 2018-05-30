---
layout: post
title:  "Migrating from Heroku to Digital Ocean"
categories: blog
---

For the last few years, I've been launching personal projects to Heroku because of its simplicity. The downside though is you pay for that ease of use in your monthly bill. After paying $17.53 last month for a simple project, I figured it is time to move it to a VPS.

## Why Digital Ocean

Digital Ocean has great documentation for Django projects, and with the same pricing as Linode, I figure I'd go where it seems they have more interest in Django.

[Create your account](https://m.do.co/c/2bf12675e601) and by using that link, you'll get $10 credit.

## steps

Set up the instance

Set up the code

## Set up the instance

Register
Set up the instance

A record to the new IP address


Optional - move the domain management to Digital Ocean
- custom nameserver


## Set up the repo
Remove procfile
local.yml
production.yml


Add the compose

Update settings
- local

Remove the procfile
