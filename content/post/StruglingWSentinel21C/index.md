---
title: "Struggling to Download Sentinel-2 Level 1C `.SAFE` Files with Python and AWS CLI"
summary: Trying to programmatically download Sentinel-2 Level 1C `.SAFE` files including metadata for ACOLITE atmospheric correction using Python and AWS CLI.
tags:
  - Python
date: "2025-09-22T00:00:00Z"

# Optional external URL for project (replaces project detail page).
#external_link: https://felipesbarros.github.io/test/post/hacktoberfest-2021/

image:
  caption:
  focal_point: center
---

## TL;DR ✅

> I initially struggled to download the full Sentinel-2 Level 1C `.SAFE` package (with metadata) for ACOLITE atmospheric correction.
> The solution, kindly shared by my friend **Luis Sadeck**, was to configure **S3 access keys directly in my Copernicus Data Space account**.  
>👉 You don’t need an AWS account for this — just generate your **access_key** and **secret_key** inside your **Data Space profile**, then use them when accessing the S3 bucket.
> Docs: [Copernicus Data Space S3 API](https://documentation.dataspace.copernicus.eu/APIs/S3.html)  
> Now the entire process works smoothly with a single Python library. 🎉  
> Big thanks to everyone who reached out with suggestions and support!  

---
I’ve been trying to download Sentinel-2 Level 1C data programmatically with Python, instead of manually going to the Sentinel Hub
 website.
The goal is to get the entire `.SAFE` package, including metadata, so I can later run atmospheric correction with ACOLITE.

So far, here’s what I’ve tried:

## Attempt 1: Using the sentinelhub Python library

With the [sentinelhub Python package](https://github.com/sentinel-hub/sentinelhub-py), I was able to find the asset I needed.
It even provides an href pointing to the AWS S3 bucket for the `.SAFE` product:

```
s3://EODATA/Sentinel-2/MSI/L1C_N0500/2023/01/15/S2B_MSIL1C_20230115T133829_N0510_R124_T21HWD_20240728T040848.SAFE/
```

At first, this looked promising.
But when I tried downloading the data with the AWS CLI, **I only got the bands and a few additional elements** — not the full `.SAFE` structure.

Unfortunately, that’s a problem: **ACOLITE requires all metadata, not just the imagery**.

## Attempt 2: Using STAC from Copernicus Dataspace

Next, I tried going through the [Copernicus Dataspace STAC API](https://stac.dataspace.copernicus.eu/v1).

This was encouraging: **it actually lists the full `.SAFE` structure, and I can see hrefs for each element**. So it looked like the full dataset might be accessible.

However, **when I attempted to download it using the AWS CLI, I ran into issues**. Here’s the command I used:
```
aws s3 cp --recursive \
  s3://eodata/Sentinel-2/MSI/L1C_N0500/2023/01/15/S2B_MSIL1C_20230115T133829_N0510_R124_T21HWD_20240728T040848.SAFE/GRANULE/L1C_T21HWD_A030609_20230115T135051/IMG_DATA/T21HWD_20230115T133829_B01.jp2 \
  ./S2B_MSIL1C_20230115T133829_N0510_R124_T21HWD_20240728T040848.SAFE/ \
  --request-payer requester
```
**Has anyone successfully managed to download the entire Sentinel-2 Level 1C `.SAFE` package, including metadata, directly through Python or AWS CLI, in a way that works for running ACOLITE atmospheric correction?**

Any hints, scripts, or alternative approaches would be hugely appreciated!
