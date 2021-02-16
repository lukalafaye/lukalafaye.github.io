---
date: 2019-02-09T00:00:42.000Z
layout: post
title: Obtain a free domain name!
subtitle: Did you know that you could get a free domain to develop a website?
description: Did you know that you could get a free domain to develop a website?
image: /img/2019-02-09.jpg
category: web
tags:
  - Domains
  - Education
  - Free Domain
paginate: false
---

Thanks to GitHub education, it is possible do obtain free domains provided by Namecheap or Name.com. You can also host your website for free on GitHub if you don't have a personal server!

# Requirements

* Be currently enrolled in a **degree** or **diploma** granting **course of study**
* Have a **verifiable school-issued email address** or **documents** that prove your current **student status**
* Be **at least 13 years old**

<hr>

#### 1. Create a GitHub account

First of all, you need to visit [github.com](https://www.github.com) and create your account with your **school email address** if you have one, else use a normal email address. Once you finished filling the registration form, click the verification link in your inbox and log in on your account. 

If you already have an account, just make sure that your school email address is marked as default and public in the settings.

<hr>

#### 2. Join GitHub education

Now you'll need to head over to [education.github.com/discount_requests/new](https://education.github.com/discount_requests/new) and enter all details asked. Make sure to select the correct **school-issued email address/documents** and **school name**. Once you have received your **student pack**, you may continue with the last step!

<hr>

#### 3. Get your free domain name

##### 3.1 Free .me domain from NameCheap

Visit [nc.me](https://nc.me/github/auth) and search for an available **.me** domain. Add it to your cart and complete the order.\
If asked, ensure you enter your **primary email** on GitHub (if you have a **school email** address you need to enter that one)!

* If you're planning on hosting your website with GitHub, select **GitHub pages** and check out [the official documentation](https://help.github.com/en/github/working-with-github-pages) on what to do next. 
* If you're planning on hosting your website on a personal server, select **Ghost Machine, Managed by Namecheap**

<hr>

Once you've finished creating your account, log in on [namecheap.com](https://www.namecheap.com/). Click your username and move to your **dashboard**. In the nameservers section, select **Namecheap BasicDNS** and apply by clicking the green tick mark.

Move to **Advanced DNS** in the top menu and add a new record. Fill with:

| TYPE     | HOST | VALUE   | TTL    |
| -------- | ---- | ------- | ------ |
| A record | @    | 0.0.0.1 | 30 min |
| A record | @    | 0.0.0.2 | 30 min |
| A record | @    | 0.0.0.3 | 30 min |
| A record | @    | 0.0.0.4 | 30 min |

<br>

Where 0.0.0.1/2/3/4 is your server's or GitHub's **IPv4 address(es)**. You can get your server's IP it by executing curl:

```bash
curl -s checkip.dyndns.org | sed -e 's/.*Current IP Address: //' -e 's/<.*$//'
```

<br>

GitHub's IPs should be: 

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

If they do not work, check [the docs](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain) for the updated records.
