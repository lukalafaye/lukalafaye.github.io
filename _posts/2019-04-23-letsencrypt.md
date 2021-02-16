---
date: 2019-04-23 00:00:42
layout: post
title: Let's Encrypt
subtitle: An open and free certificate authority
description: An open and free certificate authority
image: /img/2019-04-23.jpg
category: web
tags: 
- SSL Certificate
- Free SSL
paginate: false
---

# Let's Encrypt

Let's Encrypt is a project of the ISRG (Internet Security Research Group), an American non-profit organization (501)(3)(c) which goal is to make SSL/TLS encryption universal, and therefore to offer free SSL/TLS certificates to everyone.

## How does it work?
Like a regular certificate authority, Let's Encrypt needs you to prove your control of the domain you wish to secure...Therefore, you must pass validation controls which are automated.

This automation lets you have free SSL/TLS certificates in an instant, but you will only get a Domain Validated (DV) certificate, which means you only proved your control of the domain. You cannot obtain OV or EV certificates due to the manual auditing process that has to be made for these kind of certificates, making automated issuance impossible and therefore not free.

## How can I obtain a certificate?

### I want it to be automated
It depends on the way you wish to obtain a certificate: do you want to set it up once and forget about it, or do you want to renew it manually so that you can have greater control? Do you wish to have a wildcard certificate, or are multi-domain certificates sufficient?

Usually, when you want automation or when you do not need a wildcard, people choose an ACME client. ACME stands for *Automatic Certificate Management Environment*, the PKI infrastructure for open certificate authorities. Validation challenges and messages between the CA and the server are made through this protocol, a technical mix-up of HTTPS and JSON.
Most ACME clients are free, including [Certbot](https://certbot.eff.org) which is the most used. Certbot was designed by the makers of Let's Encrypt for almost all Unix-based OSes (but not Windows yet) and for all web servers including Nginx and Apache.

What is good of ACME is that it has become a standard for free certificate authorities, is open-source and was initially made specifically for Let's Encrypt (now, many other CAs like BuyPass use this protocol).

### I do not want automation
If you do not want automation, the ACME client can still issue certificates manually by calling the client through the shell.
You can also use a browser-based client for Let's Encrypt like [SSLForFree](https://www.sslforfree.com) which uses the WebCrypto API, an application programming interface allowing certificate generation from within the browser and not server-side.

Manually-obtained SSL certificates have the advantage of supporting more kinds of certificates: the wildcard certificates. Since it is impossible to validate every possible subdomain that can exist, it is possible do perform a domain validation through its DNS, using the latter as a verification method with a TXT record.

## How does validation work?
There are 2 ways to validate your control of a domain:
* The DNS method mentioned earlier
* The File verification method, where a specific file is requested by the CA for validation that either the ACME client has uploaded to the server, or the server owner him/herself has installed on the document root of the website.

## How long do these certificates last?
Let's Encrypt certificates last for 90 days, which is short enough to:
1. encourage automation
2. faster expiration of certificate if the latter is compromised (since Chrome no longer recognizes certificate revocation lists)

## How did the project start?
It was an initiative of the ISRG, which was sponsored by most web giants like Google, Mozilla, Cisco, OVH...

Its annual budget is US$3.6M and participates in the CA/B forum which is the main discussion board for certificate authorities and new companies who wish to become CAs.
