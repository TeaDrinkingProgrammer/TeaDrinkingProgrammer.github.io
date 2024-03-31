+++
title = "The last missing piece of my Markdown setup and a small update"
date = 2024-03-10
draft = false

[taxonomies]
categories = ["software"]
tags = ["markdown", "productivity"]

[extra]
lang = "en"
+++

# A small update
Hi all! It's been a while since my last post and, before I start with the main post, I would like to give a small update of what has happened in the meantime.

I put my last post up on [Tildes](https://tildes.net/~tech/1dqs/the_markup_iceberg) and the reactions were very insightful and helpful: some people liked my style, some people thought that my post was unfocused and the intro felt decoupled from the rest of the story, and I must say I can't disagree. That's why I have rewritten parts of the last post based on that feedback. Thanks again to all people who gave feedback, be it positive or negative. It has made me aware of some blind spots in my writing. 

I also got feedback from [Emily Baucom (Alias Oslypsis)](https://emilybau.com/) that my website could use a logo and that she could help me make one. The end result is the wonderful logo you can see in the top bar as a favicon and the logo on the homepage. I love the design!

With that out of the way, let's get into the story of today: the last missing piece of my Markdown setup.

# The last missing piece of my Markdown setup
One type of feedback I got, was on my spelling. This issue mainly had to do with the fact that I was overconfident in my ability to write correct English and thus didn't see the need for a spellchecker. I thus needed a spellchecker, and I wouldn't be the Teadrinkingprogrammer if I didn't look for some arcane solution.

I first needed to find something that met my requirements. My requirements were the same as always:
- Preferably open source
- Integrates with my existing tooling (this being [Zettlr](https://www.zettlr.com/) or VS Code)
- Good spellchecking, obviously

I first started digging into the settings of Zettlr to see if it had something to offer besides the default spellchecker: Hunspell. Hunspell is a simple spellchecker used in most browsers. It is a great default, but has pretty mediocre spellchecking. Besides Hunspell, I saw that there was an option to connect with a [LanguageTool](https://languagetool.org/) server. This immediately piqued my interest, as I had already heard a lot of great things about it.

For those who haven't heard of LanguageTool: it is to Grammarly what [Deepl](https://www.deepl.com/translator) is to Google Translate: more powerful AI versions that are more privacy-friendly to boot. Like Grammarly, LanguageTool suggests alternatives for style and grammar mistakes but unlike Grammarly, it is open source and has a self-hostable version. I have also found that it just gives better feedback, specifically when writing in Dutch.

When I had decided to use LanguageTool, I also found out that Zettlr had a [tutorial](https://docs.zettlr.com/en/guides/languagetool-local/) on their website about self-hosting it. It points to [this Docker image](https://github.com/silvio/docker-languagetool). Docker is an amazing tool, and works especially well with Linux or macOS. If you are using the Docker image, I recommend not using the N-grams files, as they are quite heavy and the base server is already quite slow on my, admittedly old, laptop.

I am, however, using Windows at the moment because I need to work with some Windows-only software. This meant that running the server in the Docker container incurred quite some overhead and the CPU-usage felt a bit overkill for what was essentially an advanced spell-checker, so I wanted to get it to work on Windows directly. This turned out to be a lot easier than expected.

# Getting LanguageTool to run on Windows
So how do you get LanguageTool to work on Windows? Well, you're in luck, because LanguageTool have pretty clear instructions on their [website](https://dev.languagetool.org/http-server). 
It pretty much comes down to these steps:
1. Install Java 17, which is as easy as `winget install Oracle.JDK.17`
2. Download and unpack the zip file from the link below “Getting the server”.
3. Make a script file to run the server:
Batch file:
```sh
@echo off
cd "C:\Path\To\LanguageTool\Folder"
java -cp languagetool-server.jar org.languagetool.server.HTTPServer --port 8010 --public --config server.properties
```
or a Nushell file like me:
```sh
cd C:\Path\To\LanguageTool\Folder; java -cp languagetool-server.jar org.languagetool.server.HTTPServer --port 8010 --public --config server.properties
```
(I am probably going to make a blog post about Nushell some day: TLDR: it's amazing)

4. Run the server by running the file. Put it somewhere you can get to easily, like the desktop, taskbar, etc.
5. Profit!

Actually, hold onto your profit for a bit if you want to use Zettlr with LanguageTool. 

Getting that to work also turns out to be a piece of cake. Just go into settings → Spellchecking and set LanguageTool Provider to Custom server. Set the server URL to `http://localhost:8010/` without Username or API key. Above these settings you can also set you Mother tongue. This enables LanguageTool to scan for so-called ["false friends"](https://en.wikipedia.org/wiki/False_friend).

{{ figure(src="assets/languagetool_settings.png", alt="Mother tongue is set to 'Dutch (Netherlands)', the LanguageTool setting to Custom server. The server URL is set to http://localhost:8010/ and the Username and API key fields are empty.", caption="An image showing the Zettlr spellchecking settings page.") }}

When writing, you might have to manually set the language in the bottom-right, as the automatic language detection on Windows is worse than macOS and Linux. Otherwise, I have found this solution has worked well.

# Using LanguageTool day-to-day
Now that I have explained _why_ you would want to use LanguageTool and shown you _how_ you can use LanguageTool, you're probably curious about the pros and cons of using it day-to-day.

The pros are simple: LanguageTool is more powerful than any spellchecker I have used until now. It is probably somewhere around two orders of magnitude better than Word. This is both due to the kind of feedback it gives and how it's formulated.

The cons are mainly due to the fact that I am self-hosting an AI-server on a 7-year-old laptop. It is not _slow_, but it isn't instantaneous either. I have adapted by changing my workflow to booting up the server when I am near the end of typing out a section, then wait for a bit and correct the mistakes it has found. It is not ideal, but it is a compromise I can live with.

The second disadvantage is that the open source server implementation of LanguageTool misses some features from the paid version, notably a dictionary function. This is a bit annoying because you have to ignore some warnings about names and such, but it isn't a dealbreaker.

Some of these issues could be fixed on the Zettlr side (result caching and local dictionary), and I have opened some issues, but I understand that this is probably not their priority.

# Conclusion
LanguageTool is a great piece of software and self-hosting it is easier than I thought. It has some drawbacks, but they aren't dealbreakers in my opinion. All in all, I am quite happy with how my set-up has turned out.

As for the next blog post: it's probably going to take a while and the posts are going to stay inconsistent for now, as I have a lot going on at the moment. 

As always, if you want to get notified when I post something on here, you can subscribe to the mailing list by filling in the form below. You can also subscribe to the RSS feed if that is more your thing. Thank you for reading my blog and until next time!