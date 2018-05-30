---
layout: post
title:  "The fast & right way to setup a Github Pages site with Cloudflare"
date: 2018-05-30 07:24:37 -0400
categories: blog
---

After trying Wordpress many times, I wanted a simpler blog platform that I had more control over. That led me to try [Github Pages](https://pages.github.com),a static website platform that lets you launch websites from a Github repo. It turned out much easier than expected. Just push updates to the repo, and your static website will be updated. This tutorial will walk you through that process, and how to set it up so that it will be fast for both [Pingdom Speed Test](https://tools.pingdom.com) and [Google PageSpeed](https://developers.google.com/speed/pagespeed/insights/).

* **Time**: Less than an hour
* **Difficulty**: Easy
* **Cost**: Free

## OVERVIEW
* **Tooling**: What tools are used?
* **Set up your Github repo, Domain DNS, and Cloudflare**
* **Set up your Local Developement Environment**
* **How to speed it up**: Enhancements for better performance


## TOOLING

* **Github** - you'll have a repo for your static site that must be named <username>.github.io

* **[Jekyll](https://jekyllrb.com/docs/home/)** - Jekyll is static website generator with pages written in Markdown.

* **[Markdown](https://daringfireball.net/projects/markdown/)** - Markdown is a language for formatting plain text 

* **[Cloudflare](https://www.cloudflare.com)** - Cloudflare provides distributed DNS services plus a few other services we will take advantage to speed up your static website.


## HOW TO SET IT UP
For this example I'll be using my domain as the example. Just replace my domain with your own for this to work.

Everything in `gray` should be replaced with your own information.


#### **1. Register a Domain Name**
After registering a domain name, we will need to update the DNS records.

My domain: `emilepetrone.com`


#### **2. On Github**
* Create a Github repo named: **`emilepetrone`.github.io**

Your Github Domain will be the repo name. So in this case, the default domain to my static website is: ```emilepetrone.github.io```

* In the repo's settings, add a custom domain pointing to your url: **`www.emilepetrone.com`**

Two things of note:

***Note:*** There was an option to check enforce HTTPS, I was unable to check this box on Github. We will enforce HTTPs with Cloudflare instead.

![Custom Domain settings in Github](../assets/imgs/2018-05-30-github-blog/domain.png)

***Note:*** Finally, Github will advise you to point your domain to your Github Pages url. We will not do that but point it to Cloudflare first.


#### **3. On Cloudflare**
Pointing your domain at Cloudflare and take advantage of their free features to enhance your site.

* Sign up for Cloudflare, and find your Cloudflare Nameservers

![Nameserver on Cloudflare](../assets/imgs/2018-05-30-github-blog/nameserver.png)

The values above are what you will then updated on your Domain with your Domain registrar.

#### **4. On your Domain Registrar**

* You'll take the Name Servers from Cloudflare, and update your Custom DNS settings by replacing your Name Servers on your domain with the values from Cloudflare

```
<somevalue1>.ns.cloudflare.com
<somevalue2>.ns.cloudflare.com
```

This will let you control your domain through Cloudflare and take advantage of their advanced features.

#### **5. Back On Cloudflare**

Now that your domain is pointed at Cloudflare, we will point the domain to Github.

![CNAME records](../assets/imgs/2018-05-30-github-blog/cname.png)

* Add a **CNAME** record for your Github Page domain: `emilepetrone.github.io`
* Add another **CNAME** record pointing `www` at your Github Page domain

At this point, the domain may take up to 24 hours to propogate.


## **Local Developement Environment**

While you wait for the DNS settings to propogate, we can setup our local developement environment. This will be installing Jekyll and setting up a new Jekyll website. 

Once you are in the directory of where you want this code to live on your local machine:

```
gem install jekyll
jekyll new <name_of_site>
cd <name_of_site>
jekyll serve
```
If you run into any issues, make sure **Ruby** is installed with 

```
Ruby -v
```

and that **gem** is installed

```
gem -v
```

At the time of this post, I was running:

```
ruby 2.5.1p57 (2018-03-29 revision 63029) [x86_64-darwin17]
gem 2.7.6
```

***Note:***
Within the new directory, there will be a `CNAME` file. It contains the domain you want a visitor to access. This file's contents must match the custom domain name you put in your repo's Github settings. If you make a change in either place, make sure these match.

![Custom Domain settings in Github](../assets/imgs/2018-05-30-github-blog/domain.png)


#### **6. Commit to your Github Repo & Deploy**
Next you'll want to push this repo.

```
git init
git add -A
git commit -m "First"
git remote add origin git@github.com:emilepetrone/emilepetrone.github.io.git
git push -u origin master
```

***Note***: You'll just make sure to add the git address to your repo instead of mine provided above.

