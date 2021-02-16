---
date: 2019-02-17 00:00:42
layout: post
title: What is TLS?
subtitle: TLS stands for *Transport Layer Security*. It's a network communication encipherment protocol.
description: TLS stands for *Transport Layer Security*. It's a network communication encipherment protocol.
image: /img/2019-02-17.jpg
category: technology
tags: 
- Web
- Mathmatics
paginate: false
---

# What is TLS about?

TLS stands for *Transport Layer Security*, being a protocol which helps encryption of sensitive content over a network. Initially known as *Secure Sockets Layer*, or SSL, its goal is to protect clients and servers from eventual attackes and to guarantee transmission authenticity.

## Why should I install TLS?

The process seems to be quite complicated, but it's actually done in less than a second, in a regular computer it usually lasts 500ms or less.

There are actually a great number of incentives to install TLS:
* Secure page, data integrity
* Page visibly protected (a padlock can bee seen)
* SEO Boost at Google > Improvement of your page rank, so more visitorys
* TLS is free, thanks to Let's Encrypt, Buypass, Encryption Everywhere by Digicert or cPanel
* TLS support by all web browsers
* Protect several sites in the same time


Some problems can hinder the progress of TLS:
* The time required to install TLS (which can be remediated by automation tools like Certbot)
* Time required to validate SSL/TLS certificates that show the owner
* Only a protection of data transmissions
* Price can be a factor for SSL/TLS certificates that last more than 90 days
* Environments that do not support Server Name Indication

## How can I improve TLS?

Some other concepts can improve TLS although not directly related to the protocol
* [HSTS](https://hstspreload.org) (*HTTP Strict Transport Security*), forcing HTTPS through a header, which can also be preloaded
* HPKP (*HTTP Public Key Pinninng*), forcing a particular SSL/TLS certificate for the HTTPS connection
* CAA (*Certification Authority Authorization*), restrict certain CAs to issue any certificate for your domain
