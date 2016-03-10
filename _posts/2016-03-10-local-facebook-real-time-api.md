---
layout: post
title: "How to Setup Local Development of Facebook's Real-Time API"
excerpt: "Developing against facebook's real-time webhooks requires a static url utilizing SSL. This may seem impossible to do locally, but in a matter of 15 minutes, you can be ready to recieve updates from facebook on your local machine."
tags: [facebook, ssl, webhook, real time]
comments: true
---

Developing against facebook's real-time webhooks requires a static url utilizing SSL. This may seem impossible to do locally, but in a matter of 15 minutes, you can be ready to recieve updates from facebook on your local machine.

## Requirements

In order for Facebook's real-time webhooks to talk to your application, it requires 2 things:

- Static URL to talk to
- HTTPS URL

Both of these present a huge problem for local development, as you most likely have a dynamic IP for your local network, and SSL's aren't cheap, nor are they easy to setup.

## Static URLs

Many people have a use case for needing a static IP for their local network. Whether it be for hosting a gaming server, or a web server, being able to have people connect to your machine from outside your local network can be a necessity. 

[No-IP](http://www.noip.com/) is a service that can help mitigate this issue. It's an application that you install on your machine, and whenever your ip changes, it updates your hostname so that other people can still access your local servers. By using No-IP, you can give facebook a static URL, and it will always know where to direct traffic.

## SSLs

SSLs aren't cheap, and in addition, they are expensive. Most of the time, you can get away with developing without SSL, just for testing and exploration. Facebook, however, wont' allow you to connect to their Real-Time webhooks without connecting to your service over SSL. 

[Cloudflare](https://www.cloudflare.com/) is a company that provides a varitey of services related to DNS (domain name services). They also provide "free" share ssl. If you signup with their free plan, you can associate the domain you have from no-ip with a SSL protected domain from cloudflare.

## TL;DR

Get a static domain with [No-IP](http://www.noip.com/) and get it SSL protected with [Cloudflare](https://www.cloudflare.com/)