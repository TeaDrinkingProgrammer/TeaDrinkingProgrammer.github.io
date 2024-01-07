+++
title = "2024 Will Be The Year Of the Linux Desktop !(?)"
date = 2024-01-06
draft = false

[taxonomies]
categories = ["markdown"]
tags = ["markdown", "guide"]

[extra]
lang = "en"
+++

# The Year of the Linux Desktop

Before I start: if you're reading this around the time this is published: happy new year! I hope you have had a fantastic winter holiday (I sure did). 

2024 is going to be an exciting year, especially in Linuxland. I even think this year holds so much promise that it might be the long-awaited "Year of the Linux Desktop": the mythical year when the Linux Desktop becomes mainstream which is always one year away, kind of like fusion power. It has been one year away for so long, that the concept has become a meme in and of itself. Hence, this title is kind of tongue-in-cheek: I don't actually think that next year will magically be the year where everyone suddenly starts using Linux. I do think that Linux will become accessible for far more people though. Before I get into why, I first need to give some context.

# Linux as a desktop operating system

Linux is pretty old by software standards: it's first release was all the way back in 1991. Although it started as a one-man project, it quickly garnered popularity as a server OS. This is not so strange, as the appeal of a license-free OS is very appealing when you have hundreds of computers running that OS. You can save a lot of money by using Linux on servers. This popularity on the server has only grown: Linux is now the de-facto standard on webservers. It is so ingrained in fact, that even Microsoft has a Linux distribution now for it's Azure cloud service. 

Linux being the standard on servers has slowly but surely made Linux more appealing for developers, because using the same OS for both your server and work machine avoids bugs and complexity when the time comes to deploy an app. This is why Microsoft have now included the confusingly named "Windows-subsystem-for-Linux" or WSL. It should have been named LSW because Linux is the subsystem but I digress. WSL has made it possible for Windows users to use Linux on Windows and has become quite popular or even, depending on the field, pretty much mandatory (think of Docker).

For gamers, Linux has also become a more and more attractive option. Since Valve has released their Steamdeck, they have been heavily investing in a software called "Proton". It is a collection of programs that translate Windows system and graphics calls into Linux system and Vulkan calls. You can compare it to a translation software: Spanish in, English out. The main benefit of this approach is that it is very lightweight. It is so lightweight in fact, that [a Linux distro tuned for gaming (Norbora) can beat Windows at playing Windows games](https://www.tomshardware.com/software/linux/three-gaming-focused-linux-operating-systems-beat-windows-11-in-gaming-benchmarks). You heard that right: in a benchmark by Computerbase.de of four games, Windows has _less FPS_ than a Linux distro when playing _Windows games_. Is this the case for every game? No. Even within this benchmark, sometimes Windows 11 is faster. But the fact that it is even close and on average faster, shows that Linux is better or equal to Windows at running Windows games. Keep in mind we haven't even talked about native Linux games versus native Windows games.

{{ figure(src="assets/norbora-vs-windows.png", alt="Norbora is at 100% while Windows 11 is at 94% relative performance.", caption="Relative FPS performance to Norbora Linux") }}

The amount of Windows games that can run using Proton is very high: looking at [protondb.com](https://www.protondb.com/), 80% of Windows games on Steam are either verified by Valve to be playable on Linux or deemed playable in some capacity by popular vote. Only 20% is downright unplayable. This isn't even a fault of Proton most of the time: most games are "borked" because of game developers purposefully blocking games from running Proton with anti-cheat. In other words: pretty much everything that isn't multiplayer with match-making is all but guaranteed to work.

For the average user, things have been improving as well. With many things moving to browser apps, many productivity tools can now be used on Linux. Think of apps like Teams, Word or even Photoshop which can now be used online. Speaking of Word, I am going to make a post about using Markdown as a replacement for it, so stay tuned for that.

This all sounds great, but there are still very few people using Linux. Why is that?

# The dealbreakers

Despite all the progress that the Linux desktop has made, there are still some dealbreakers. One complaint I have often heard is screen issues of all kinds: screens tearing when they're not supposed to, second monitors not working or scaling not working properly for 4K screens. A second problem which has been a dealbreaker for many is Nvidia. Nvidia graphics cards and Linux have been a terrible combination for a long time. As Linus Torvalts himself put it ["Nvidia has been the single worst company we've ever dealt with. So Nvidia: fuck you"](https://youtu.be/OF_5EKNX0Eg?si=CzVRNMiuO7KR0fhG). This …  constructive criticism was made some years ago, and thankfully, Nvidia has come around to Linux [open sourcing some parts of their drivers](https://www.phoronix.com/review/nvidia-open-kernel). That said, some parts remain closed source and the drivers are still not great, causing many issues. The difference between Nvidia and AMD is so big that I am willing to say that Nvidia is 5 to 10 years behind on AMD with their drivers.

This status quo is not going to last though: the great people at Collabora are making a brand new fully open source driver called [NVK](https://news.itsfoss.com/nvidia-nvk/). The drivers are written from scratch and focus on new GPUs. The progress on the NVK drivers is at a break-neck speed: [after just one year, the driver can already run at least one game faster than the old driver](https://www.phoronix.com/news/Nouveau-NVK-One-Win). Let me be very clear: the driver is far from ready. The trajectory is clear though: when the driver is finished, I expect it to outperform the current open source driver all while having less bugs. The reason for me expecting it to be more stable is simply because it has been built from scratch and has people building it actively that are in touch with the Linux Desktop community. I don't know when NVK will come out, but I wouldn't be surprised if it would be next year.

These developments come at a time where Gnome and KDE (the two main desktop environments of Linux) are also doing a lot of work to make their experience more user-friendly and more bug-free.

If or when all these things come together, the main reasons to not use Linux for gamers and developers will be lifted. Whether this means that people will actually switch is another question altogether. I think that the number of developers switching could increase quite quickly once word spreads that Linux is "actually good now". In fact, I think this is already happening on a smaller scale.

Gamers are also slowly switching to Linux. already There is one opportunity that may increase this greatly together with the previous considerations: the end-of-life of Windows 10. When Windows 10 is not supported anymore, many people will be forced to either upgrade their set-up for Windows 11 or switch. Some may upgrade, some may just stay on Windows 10 but some may look into Linux. If they find that it suits their use-case better, which I think it does for many people, many more gamers may start switching to Linux.

# Reading tea-leaves

In the end, many predictions in this analysis are just that and all of this can very well turn out to be all wrong. That being said, I do think that Linux is at a turning point where it starts to be a serious option for people outside the "open source" inner crowd. I don't think it is going to become mainstream, but I think it is on a trajectory to become a large minority in the desktop space: some 10 or 20% of the developers and gamers for instance. This future isn't certain, but one can hope.