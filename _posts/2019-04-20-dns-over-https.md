---
date: 2019-04-20 00:00:42
layout: post
title: DNS over HTTPS
subtitle: DNS over HTTPS is a new concept which consists to perform DNS queries over encrypted HTTPS
description: DNS over HTTPS is a new concept which consists to perform DNS queries over encrypted HTTPS
image: /img/2019-04-20.jpg
category: web
tags: 
- DNS
- HTTPS
- Information
paginate: false
---

# DNS over HTTPS

**DNS over HTTPS** is a relatively new concept developed by the Internet Engineering Task Force (IETF) which consists to perform DNS queries over encrypted HTTPS, therefore enciphering the requests.

## The goals
DNS over HTTPS, as defined in RFC 8484, has the main purpose to provide user privacy when the end-user connects to a particular website. As we know, the website will be pointed to an IP address with the DNS resolver, but DNS over HTTPS provides security and prevents eavesdropping and manipulation of the DNS answers...

## Technicalities
DNS over HTTPS uses several technologies which make it blatantly useful:
* HTTPS to secure communications
* HTTP/2 to decrease latency + eventually H/2 Server Push (predictability)
* Wire format DNS and its own MIME type

## Implementation
**DNS over HTTPS** is implemented in a way that it resembles a relationship between a DoH-enabled DNS resolver and its client.
There are no native clients that exist within operating systems, although third party clients (e.g.: browsers) do support it like Mozilla Firefox.
Alternatives for DoH support are DoH proxies, which do the DoH queries but then relay the data as a normal DNS resolver to the non-compatible application/system through UDP port 53.
The current implementation allows the queries to be encrypted, but some elements as the Server Name Indication header (SNI) will still be transmitted in cleartext, before a TLS connection.

## Current DoH-enabled services
* Cloudflare (https://cloudflare-dns.com/dns-query)
* Google (https://mozilla.cloudflare-dns.com/dns-query)
* CleanBrowsing (too many endpoints for the URL to be listed)

You may also host your own using DNSCrypt...

## Configuration
Configuring DNS over HTTPS might not be an easy task.
It really depends on the level of support for DoH for your app or OS.
Here is a [guide for Mozilla Firefox](https://gist.github.com/bagder/5e29101079e9ac78920ba2fc718aceec), which now has native support for it.
