---
title: "Build My First Split Keyboard"
date: 2026-10-18T00:00:00+00:00
draft: false
tags: ["Keyboard"]
---

# Overview

One day in 2025 (or maybe early 2026 — I don't remember), I was focusing on my task and engineering work. And boom... my wrist started to hurt... It was the first time I had felt this kind of pain, so I tried to research how to fix it.
At first, I thought it was caused by the switch: I had only been using the laptop keyboard, and around that time I switched to a normal keyboard. I was typing too much on the new keyboard, and the area around my wrist hurt. I researched more and came across the keyword: "Carpal tunnel syndrome"[^cts].

So I surfed the internet and randomly jumped down the rabbit hole of split keyboards. A split keyboard lets you place each half at shoulder width, keeping your wrists straight and your shoulders relaxed, which greatly reduces the strain that causes the pain.

I ordered my first split keyboard: the **Sofle** (58 keys). However, I was not happy with it, so I bought a new one: the **Corne** (42 keys) — you can easily find images of both online. The Corne was better, but I still felt it was not built for me. I needed Choc switches, not MX, and after watching a [video by Ben Vallack](https://www.youtube.com/watch?v=8wZ8FRwOzhU), I decided to build the **Ferris Sweep**: it is easy to build (the wired version), it is Choc-spaced, and there are a ton of layouts I can copy from the internet.

{{< youtube 8wZ8FRwOzhU >}}

This was a super interesting process, but also an awful one. However, in the end, I finally got my dream keyboard. I am going to share the mistakes I made in this project, and I hope they help you avoid a few problems if you decide to DIY[^diy] a keyboard.


# The Build: One Mistake at a Time

Well, I think I made a lot of mistakes. Haha, this was my first time, and first times are always messy for sure.

But first, let's see what we need to build the keyboard:

- **The PCB** (Printed Circuit Board)
- **34+ keyboard switches** and keycaps
- **34+ hotswap sockets** (so I can swap in new switches whenever I want)
- **2x RP2040 Pro Micro** and 4 pin headers
- **A TRRS cable**
- **2x reset switches**

Oh, and yes, you also need soldering tools:

- **A soldering iron** with temperature control
- **Solder wire**
- **A soldering iron stand**

The flow is simple:

1. Solder the PCB and MCU (Microcontroller Unit)
2. Solder the hotswap sockets
3. Flash the firmware using QMK
4. Mission accomplished

Most of these parts you can buy from a local shop or from e-commerce sites. The PCB is the exception — it has to be manufactured. After googling, I saw that people use [JLCPCB](https://jlcpcb.com/), so I used a third-party service to ship it from China to my country.
I downloaded the PCB design from [davidphilipbarr/Sweep](https://github.com/davidphilipbarr/Sweep), and the version I chose was the **Sweep Bling LP**.
**After 2 weeks**, I got my PCBs — 5 pieces, so in theory I could build 5 keyboards. Wow... And so the process of trial and error began.

## First Mistake: Soldering — Nothing Went Like in the Videos

In the first step, you need to connect the Pro Micro to the PCB. To do this, you just solder the headers to the PCB, and after that, solder the Pro Micro to the headers. This sounds easy, right? But... I failed at it.

Somehow, soldering the Pro Micro did not go as smoothly as in the videos I had watched. The hotswap sockets went just as badly.

I spent some time investigating these problems. My first assumption was that the iron tip was oxidized. I thought that when I used the iron for the first time, I adjusted the temperature too high (the recommendation is 350°C or 250°C — I don't remember exactly), but I saw it sitting at around **400°C**, and that oxidized the tip.
I searched for a fix and tried a few things, including tip tinner and cleaner. But nothing worked. So I concluded that my iron tip was completely destroyed.
And I moved on to plan B: buying a new iron tip.

Yes, I bought the new tip. It was delivered to me **after 3 days**. And you know what? The problem was... still not solved. So I thought maybe the soldering iron itself was the issue — maybe the temperature controller was showing the wrong numbers — and I bought a new iron without a temperature controller to test my assumption.
And once again: one more attempt, one more failure. **After 1 week** of soldering, I had ruined 2 PCBs, plus a lot of sockets and headers. You can see the best result here:

![My first failed Ferris Sweep build](/images/first-failed-ferris-sweep.jpg)

I tried googling and asking on forums. People were friendly and generous with their help, but nothing solved it. I almost gave up on this project and even contacted a shop to solder the keyboards for me.
I put this project on hold... maybe I will come back to it in a few weeks.

## Second Attempt: Flashing the Firmware

After a week of working and calming down, I had a new idea: "Okay, maybe I can't solder, but surely I can flash firmware — it's a software task, so I should be good at it, right?"
I could ask for help with the soldering, but I could customize the keymaps and flash the keyboard by myself. So I started studying how keyboards work and how to flash them.

I recommend watching this video — it explains really well how keyboards work in a nutshell:

How to Build a Handwired Keyboard:

{{< youtube hjml-K-pV4E >}}

> **TL;DR:** a keyboard is a matrix — when we press a key, it connects two pins on the Pro Micro, and the MCU sends a signal to the computer telling it which character we want to type. Bonus: the Ferris Sweep is diode-less by design (the QMK firmware detects ghost keys in software), so no diode soldering is needed.

Now the dilemma: should I use the [QMK Configurator](https://config.qmk.fm/) or the CLI? I went with the CLI because it is cooler :D and somehow this actually helped me.
I will skip some of the process, but here is the basic idea:

1. Install QMK: [Getting Started guide](https://docs.qmk.fm/newbs_getting_started)
2. Connect the Pro Micro to the computer
3. Put it into bootloader mode and drop the firmware file into the bootloader drive
4. Do it again on the second half (but I couldn't do that yet, because I couldn't connect the second MCU — soldering still not working :D...)

Yes, this was for one MCU only :D — and I hadn't even practiced it yet.

## The Breakthrough: It Was the Solder Wire

Maybe **1 week later**, I was lying lazily on my bed when I suddenly realized there was one thing I hadn't tried: the soldering wire. Could that be it — was I using the wrong type?
I checked, and it wasn't the wrong type — it was **63/37 solder wire**. However, I noticed something: I had bought a cheap no-name solder wire for about 2 USD, while a good one costs about the same — 2 USD for 5 meters.
So I ordered the good one — and just like that, the problem was gone. The soldering process was smooth and worked perfectly, and the only thing remaining was flashing the keyboard.

I ran into many more issues along the way — perhaps I'll cover those in *Build My First Split Keyboard — Pt. 2*.

![My completed Ferris Sweep](/images/complete-keyboard.jpeg)

[^diy]: DIY stands for "Do It Yourself" — building something yourself from parts instead of buying it ready-made.
[^cts]: Every developer should know about carpal tunnel syndrome: hours of typing with poor wrist posture put pressure on the median nerve, and if ignored, it can lead to numbness, lasting pain, or even surgery.
