+++
author = "Ryan Belgrave"
categories = ["lab", "vmware", "hardware"]
date = 2018-08-04T10:49:52-05:00
description = ""
featured = "switches.jpg"
featuredalt = "Home Lab Pic"
featuredpath = "img/2018/08"
linktitle = ""
title = "My homelab and why it cost way too much"
type = "post"

+++

## Introduction

Welcome to my blog! I finally got around to actually writing something. Who knew it could be hard to find a decent theme. Anyway I am going to do my best at putting out two posts a month (maybe more) going over various tech related things I am doing. Some of them will come in the form of a series while others will be one offs. There are no garentees on the amount of conent in each post, some might just end up being code snippets for fixing bugs while others might be more in-depth. Alright here we go!

## Why I have a homelab

Well I mean why not? Having "free" hardware laying around online 24/7 is great for developing and testing projects that I typically would have to pay Digital Ocean, AWS, or Google Cloud for. Of course there is the electric cost, it can be more expensive when the hardware is sitting doing nothing, but if you are not convinced just head over to [r/homelab](https://www.reddit.com/r/homelab/) and they will suck you right in.

### Hardware

#### Network

* ARRIS SURFboard SB6183 DOCSIS 3.0 Cable Modem
* PFSense Netgate-2220
* Ubiquiti Unifi Cloud Controller
* Ubiquiti Unifi PoE+ 1Gbps 24 Port Switch
* Ubiquiti Unifi 10Gbps SFP+ 16 Port Switch - not used at the time of writing

#### Compute

To seasoned homelabbers the compute hardware listed bellow is going to look horrible, and yes I know it was a horrible choice. Don't worry I cover all the issues later in the post.

##### Server 1

This computer was my old daily driver with a few parts changed and taken out. I didn't have any other use for it so why not put it to work.

* Intel i7-4770k
* 32 GB DDR3 Ram
* 40 GB SSD
* 500 GB WD Black HDD
* 2 Broadwell 1 Port NIC PCI-E cards

##### Server 2

* Intel i7-5820k
* 64 GB DDR4 Ram
* 128 GB NVME SSD
* 1 TB WD Black HDD
* Intel I350T4V2 4 Port NIC

##### Server 3

* Intel i7-6900k
* 128 GB DDR4 Ram
* 128 GB NVME SSD
* 1 TB WD Black HDD
* Intel I350T4V2 4 Port NIC

### Software

* VMWare vCenter + ESXI on every host
* Sandwich Cloud
    * A cloud-like api and control system for virtual machines running in vCenter
    * https://github.com/sandwichcloud

## Regrets and why new isn't always the best

Let me start out with **do not buy consumer hardware**. 

When I started building my homelab I didn't do any research on what a homelab should consist of and what hardware to look for. I initially searched ebay for cheap server hardware and found 3 servers for what seemed to be a great deal. However as I found out, after about 20% load it was impossible to be in the same room with them due to noise. They were also very old and relatively slow compaired to modern consumer hardware.

I took my knowledge of building gaming computers and built not one but eventually two "servers". I found the best and most expensive consumer enthusiest hardware and slapped it into a slient mid tower ATX case and called that good. It turned out to be a waste of money and I apparently didn't learn and did that twice...

Consumer hardware, even if it is old it is not good for a homelab, it is **way overpriced** and way under performant. For around the same amount of money I could have very easily peiced together slightly older Intel Ivy Bridge systems using used Xeon and Supermicro parts with tripple the number of physical cores and ram. 

Building servers however is not always the best idea, unlike consumer gear it can be more expensive, buying a used Dell R710/720 from ebay is usually better in most situations. Yet, I will continue to build my own servers. Why? Mostly for noise reasons, pre-built rack mount servers (and some tower variants) can be pretty loud when under load and modding in custom fans can be difficult. I do also enjoy searching for the various parts online and building it all when they get delivered.

I guess this turns into one of those "do what I say not what I do" type of things. 

## Future Expansion

Having compute hardware is great but not having shared storage is a pain. When I need to take a host down for maintance I need to wait for storage vMotion to move everything. I also run a few kubernetes clusters and they need to be isolated on each node due to wanting to use persistent disk. 

I have a few options, but I have decided to build a FreeNAS storage server instead of relying on VMWare VSAN. 

VSAN is great however due to having consumer hardware with no ECC memory, no room for pci expansion for raid cards, cases that aren't made for mass storage, and only 3 compute nodes, it isn't worth it trying to fix everything to ensure data reliability. 

Due to wanting to use my homelab as a "mini cloud" I don't want to deal with any storage bottlenecks, this is where the 10Gbps switch comes into play. It probably will be way overkill but the storage server will have a few Intel Optane SSD as caches which have been shown to saturate a 10Gbps link. I am still a few months away from building the storage server though and some of the hardware decisions may change. I will be making a blog post once I do get the hardware so stay tuned for that!

