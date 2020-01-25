---
title: "So, My Network got Hacked"

date: 2020-01-25T10:02:21-08:00

tags: 
  - IoT
  - Malware
  - Security
  - "Home Networking"
  
categories: 
  - Malware
  - Security
  
hidden: false
keywords: []

description: "TL;DR; Seperate your data / laptop / desktops from your IoT devices."

slug: "TL;DR; Seperate your data / laptop / desktops from your IoT devices."

draft: false

---
TL;DR; Seperate your data / laptop / desktops from your IoT devices.

Came home from a conference, you know, one of those I'm not allowed to name.

## Suspicion
Anyway, I was working the next day and suddenly, I had no internet access.  It seemed odd, as my 
[Sonos](https://www.sonos.com/en-us/home) continued to play music from [SomaFM](https://somafm.com/).
So, I went to another machine and it had access, just my work machine.  I rebooted my work Macintosh, and
still no access to the network.  Weird.

Later that evening, I was using my home Mac, and it too developed this issue, yet my TV was still 
streaming.  Great... Gremlins!

## Initial Mitigation
So, the first thing I did was go into _System Preferences…_ > _Security & Privacy_ > _Firewall_ >
_Firewall Options_ and set **Enable stealth mode**.  I set most apps to "Block incoming connections" on
the [Principle of least Privilige](https://en.wikipedia.org/wiki/Principle_of_least_privilege).  I did
this on all my Mac's.  Surprisingly, this apparently fixed things.
 
## Being Proactive
I had been meaning to move all my [IoT](https://en.wikipedia.org/wiki/Internet_of_things) devices to a
seperate netowork (before the 
[FBI recommened it](https://www.fbi.gov/news/stories/cyber-tip-be-vigilant-with-your-internet-of-things-iot-devices) 
and it was clear I could no longer procrastinate.  My 
[OnHub](https://on.google.com/hub/) has a guest network and I could have just used that and been
happy, but it really wouldn't have told me the kinds of things I was interested in.  So, I purchased
a [Synology Router RT2600ac](https://www.synology.com/en-us/products/RT2600ac). It supports 
[2FA login](https://en.wikipedia.org/wiki/Multi-factor_authentication) - which, given the 
circumstances seemed like a win.  More importantly, it had 
[Threat detection and prevention](https://blog.synology.com/building-an-intrusion-prevention-system-for-small-businesses-and-homes/)
an incredibly useful feature that would tell me whats happening on my network.  Synology's Threat
Prevention uses [ET Lab's](https://twitter.com/ET_Labs) (aka [ProofPoint](https://www.proofpoint.com/us)) rules that it downloads
every night.

### Spliting the WiFi space
I moved all of my computers to their own network, after [reimaging](https://www.webopedia.com/TERM/R/reimage.html)
them. Taking a risk that my [printer](https://arxiv.org/pdf/1806.10642) wasn't infected and moved 
that as well.

The original network became my "legacy" network and I also created an IoT network for new devices.

### Mobile Devices
Most of my IoT devices need to be controled from a device on the same network as them.  So, I keep my
[phone](https://en.wikipedia.org/wiki/Pixel_2), even though it holds the most info on me on the IoT network - I replace it before software updates
cease.  My iPad, I move from network to network, but it mostly stays on the "data" network as it works
well with my Macs.

### Monitoring
I've set the RT2600 to automatically drop harmful packets, and to notify me when it detects bad behavior.
Well, that happens a lot more that I'd like to say. I knew that from years ago when I had my own
mail server on the net - but in 20 years things had gotten really bad.  It seems like every 5 minutes
something was happening.  After a week, I turned the knobs down to only see really bad things.
 
About once every few days, or so, I find a network trojan originating form my legacy network. (it's 
stopped by the router).

### Legacy Equipment
I have a >7 year old [Smart TV](https://www.fbi.gov/contact-us/field-offices/portland/news/press-releases/tech-tuesdaysmart-tvs/) 
which is no longer updated by it's manufacturer - a bit of a problem. I also have a [NordicTrak](https://www.nordictrack.com/ellipticals)
with a fancy screen that has an embedded processor using a well known ancient OS.  Along with maybe 20
other smart devices.  I've gone in to the devices that I no longer require use WiFi, and changed them
to stop using it. Limiting what they do, and making sure that they don't have access to my main network.

## Closing Thoughts
The FBI's recommendation to have at least two seperate networks: one for IoT devices, and another
for your Data holding devices is a good one.

I really like the Synlogy Router's Threat Prevention system - I've long believed that one of the
easiest places for us to protect the internet is at the router.  Find signatures of bad things and
stop them from being routed. (it's not the only mitigation, just an easy one)