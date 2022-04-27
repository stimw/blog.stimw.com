---
title: "Use Picgo & Cloudflare & B2 With Typora"
date: 2022-04-26T22:45:42+08:00
lastmod: 
draft: false

images: []
tags: ["Cloudflare", "Typora"]
categories: ["Dev"]
series: []
series_weight:
seriesNavigation:
featuredImage: ""
featuredImagePreview: "https://img.stimw.com/2022/39aadc4e6335a58cba789328440a6eb5.png"

hiddenFromHomePage: false
rssFullText: false
---

## Overview

- Backblaze B2: Cloud Storage for images
- Cloudflare: CDN for images
- Picgo-core: uploading the images to Backblaze B2

## CloudFlare

Follow [this reddit post](https://www.reddit.com/r/backblaze/comments/i3t104/using_cloudflarebackblaze_b2_can_i_remove/).

> 1. In Cloudflare, create DNS CNAME or ANAME record to your Backblaze bucket host (will be something like `f***.backblazeb2.com`). The record must be proxied by Cloudflare.
> 2. Under Rules > Transform Rules in Cloudflare, add a new Rewrite URL rule.
> 3. Upcoming requests match > Hostname equals your full sub/domain
> 4. Then > Rewrite the path, using Dynamic, to `concat("/file/<your-bucket-name>", http.request.uri.path)`
> 5. Requests to your sub/domain will be re-written transparently to append the bucket name and `/file` prefix to requests forwarded to Backblaze.

## Picgo-core

**Why Picgo-Core**: Picgo GUI for apple silicon is still in Beta, and Typora supports Picgo-core to upload.

First, download the Picgo-Core following [the github repo](https://github.com/PicGo/PicGo-Core).

Then we need to install the [Picgo s3 plugin](https://github.com/wayjam/picgo-plugin-s3) for Backblaze B2:

1. `picgo add s3` to install the s3 plugin
2. `picgo use`, select s3 and path
3. `picgo set uploader aws-s3` for configuration

![image-20220426231614533](https://img.stimw.com/2022/30504fb67419564fa914591e85b37a57.png)

Aside from the option of being punched in mosaics, the others can be in line with me.

## Typora

![CleanShot 2022-04-26 at 23.25.04@2x](https://img.stimw.com/2022/39aadc4e6335a58cba789328440a6eb5.png)

If you set `picgo upload` in the “Command” options, you need to input the absolute path for `picgo`.

For example, use `which node` and `which picgo` to get the path of node and picgo.

Then type:

```
{node-path} {picgo-path} u
```

Although I only used `{picgo-path} u`...

FYI: [Typora Official Guide](https://support.typora.io/Upload-Image/#picgo-core-command-line-opensource)
