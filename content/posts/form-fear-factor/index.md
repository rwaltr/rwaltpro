---
title: "HomeCompute - The Form Factor Fear Factor"
descripton: "What even is a rack unit?"
date: 2024-04-16
tags: [Diary, HomeCompute]
draft: false
topics: [Homelab]
series: ["HomeCompute"]
series_order: 4
---

# Not all computers are in the same size
We have talked power in the past, (and more details are coming, I swear). But we have not talked about the physical size of computers in the homelab.

This can be a bit of a touchy subject, as the form factor of your computer is large dictated by the era you bought your computer, how powerful it is, and even its architecture.

Lets start with a history lesson, shall we?

# The early 2000s of home computing

![A older computer](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fupload.wikimedia.org%2Fwikipedia%2Fcommons%2Ff%2Ff0%2FDell_Desktop_Computer_in_school_classroom.jpg&f=1&nofb=1&ipt=1dea0197a5baf5e62e64cfb255457dbda2e6434a7553f9c870050ef60755ba1f&ipo=images)

Life was simple, You AOL'd your dial up with your netscape on yahoo. I think. 

In this age, Homelabbing was running your own ISP, BBS, or simple web server with maybe another desktop tower.

# The 2015 era of home computing


![Cuteboi84's Homelab'](https://preview.redd.it/my-new-server-rack-v0-69m5xw98hkca1.jpg?width=640&crop=smart&auto=webp&s=3f6df51f1d1b8d933fbf4f9fdf3a9839c4e59857) 
Source: https://www.reddit.com/r/homelab/comments/10e7dry/my_new_server_rack/

Ebay flows with surplus hardware, power is cheap, your wallet is thin, but the soul is willing. You just finished your ESXI Vmug purchase, and nothing can stop you and your 42U rack from computing perfection. 
Your life is ran buy one standard, Rack units.

## What even is a rack unit?
A rack unit is the height of a computer in a server rack, it is 1.75 inches, which is a bit thin.

Most devices in a server rack tend to be above 1u except for dedicated compute, or network switches, 2u is the minimum, 4u being the most common size for servers, both DIY and industrial

## The mid 2020s of home computing
> Holy COFLATION Batman!

Power cost has gone up, Raspi has died, and the mini-x86 revolution is in full swing!

We are trying to hold onto the glory of the 19in rack, but with some issues.

Most of the rackmount gear is made for intel nucs, a somewhat dying platform, and that gear is all over 50 USD, this still does not solve power density, or form how the ports on intel nucs are all over the place.

# What standards already exist for small device mounting?

There are a few preexisting sub computer mounting standards, surely we dont need to make another standard, right?

## DIN Rails
![din rail computer](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fwww.welotec.com%2Fwp-content%2Fuploads%2F2021%2F07%2Fsubstation-edge-controller-industrial-pc-din-rail-front-top-800.jpg&f=1&nofb=1&ipt=618f6d892dd501e522aec0b72e0636f4ec7c50729b261b2c8edb878636c72d4f&ipo=images) 
These are used in industrial settings, and are a bit of a pain to use, while the din rail itself is cheap, the actual computers and power supplies for this are expensive. This also limits you to small devices like SOCs and dedicated industrial computers. 
## Blade servers

![Blade server](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fbladesmadesimple.com%2Fwp-content%2Fuploads%2F2009%2F09%2Fbladecenter-h-front1.jpg&f=1&nofb=1&ipt=86140cd1ecce6c6d97bc54e276b92c7fc3186f56efc10bb080ab81192805c72d&ipo=images) 

Blade servers are typically vendor locked in vendor specific chassis, and are not very common in the homelab space, as they are expensive and power hungry, and have no interchangeability. 

## Open19's Bricks

![brick](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fupload.wikimedia.org%2Fwikipedia%2Fcommons%2F7%2F7e%2FBrick_pile.jpg&f=1&nofb=1&ipt=3f168403bfa76e53538df27dcd4b0f286bb114dc557b077c69cf2f95e1e68cb4&ipo=images) 
If you remember from my first HomeCompute, I mentioned Open19, and their bricks. I think this has some merit, but the actual execution of this is difficult to execute in the home, due to their specialized dense cables. 

# It might be time to ditch the 19in rack.

A 19in rack only gives you about 17.5in or useable space for internal dimensions, 17.5 x 3.5in x 25in is not optimized for your home space, you either have to sacrifice in additional upward Us, or a deeper rack. At that point, you wont be able to reach the back of your rack easily, and most of your space will be wasted.

If only there was some shape that is common and cheap enough for us to use and work with on a normal basis...

## The KubeLab


