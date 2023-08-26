+++
title = "How to make your blog more Blazingly Fast™"
date = 2023-08-26
draft = true

[taxonomies]
categories = ["dev"]
tags = ["webdev", "rust", "blog"]

[extra]
lang = "en"
toc = true
comment = false
copy = true
math = false
mermaid = false
+++

Hello there reader :wave:!

# A little introduction
I am Stijn A.K.A the TeaDrinkingProgrammer and you are currently reading the first blog post on my new blog! On this blog you are probably going to see posts about one of my main interests: cultures and languages, music and programming. The main content is probably going to be in the programming space, but some cross-overs are possible. In the programming space, I mainly follow developments in the FOSS space (I am writing this on [Zettlr](https://www.zettlr.com/) and Fedora Linux) and I sometimes play around with new technologies that interest me, like Rust or Svelte.

# Yet Another Blog
So why a blog? Isn't everyone and their dog making a blog nowadays? Yes, that's true. I mainly view the blog as an excercise in writing and web development, and a way to share my passions. I've had the idea for a while, but didn't have much to write about, until I made a _very_ long comment on [Tildes](https://tildes.net). I realised this comment would make for a good blogpost so now I had motivation _and_ an excuse!  I first thought that Medium would work well enough for me, until I found out that:
1. It has no native Markdown support
2. It will sometimes ask users to log in to read a post

Medium not having Markdown is not a dealbreaker perse, but it isn't great. The final straw was Medium nagging users to log in to read posts. I hate when websites do this so that made the decision final: I would try hosting my own website. Besides: it's a great excuse to figure out how to host a blog and learn some new tech :smile:.

I had already thought about how to go about this. I was always going to use a static-site generator. Not just because it is the obvious choice, but also because I had [the "don't flip the web-pyramid" mentality from the maker of Tildes](https://docs.tildes.net/philosophy/site-implementation#use-modern-versions-of-simple-reliable-boring-technology) in the back of my mind.

I had also heard about github.io being a good option, and it indeed seemed like the perfect fit: simple, free and no buts or ifs.

# Choice Paralisis
But now the age-old question: which of the 9000 static-site generators am I going to use? As I said, I wanted to use this project as an excuse to try out something new, and I have been experimenting with Rust for a while now, so why not (Re)write It In Rust:tm:. I quickly found [Zola](https://www.getzola.org/). It looked very enticing: no bloat, easy to use, generates plain HTML and CSS while still alowing me to write in my beloved Markdown, and last but not least: it's Blazingly Fast :tm:. Besides this, the documentation is top-notch and the configuration is great, which it has in common with most Rust projects. As an added bonus, there were a lot of themes to choose from. Sufficed to say: I went straight for Zola.

As for the theme: I ended up choosing the [Serene](https://github.com/isunjn/serene) theme, because it strikes the right balance for me: simplistic, but not _too_ simplistic. I like a lightweight website as much as the next guy, but a bit of CSS for a nice look and feel is a sacrifice I am willing to make.

I didn't change much about the theme. I only swapped out the font. This is because it uses a font from Google Fonts by default, and I block those using a plugin because I don't really trust Google. Under the motto of the golden rule, I swapped out the font with [one from a non-Google provider](https://brick.im/fonts/lato/).

# Deployment
After I filled in the settings, the website was really coming together. There was one last thing to do: the deployment.

This was surprisingly easy to do: There was already a plug-and-play Github Action! It takes your Github repo, runs Zola build in a Docker container and posts puts the result on the gh-pages branch. You then only have to set this branch to be used in the Github Pages settings and voila: a blog has been born!

At the end, I needed to do quite a bit of tweaking because my username is so long it breaks mobile :neutral_face:. It reminded me of why I hate working with raw CSS, especially padding. But, in the end I made it all work and it looks quite good if I say so myself.

# Conclusion
So, that's it then. It took me a while to write this post, so I will have to do the Tildes post later :sweat_smile:, so say tuned. To see what the source code looks like, you can take a look on [my Github](https://github.com/TeaDrinkingProgrammer/TeaDrinkingProgrammer.github.io). If everything works as intended :crossed_fingers:, there should be a RSS feed, so feel free to subscribe to that if you would like to be updated when I post something else.

Otherwise, thank you for taking the time to read my blogpost!


PS:
These were the songs I was listening to during the making of this post.

[Vulfpeck Live at Bonaroo](https://youtu.be/z1bgqUlMerI?si=X8Ak-H51KLgPXewI)
[Vulfpeck Live at Madison Square Garden](https://www.youtube.com/watch?v=rv4wf7bzfFE)
[Joni Mitchell Shadows And Light](https://www.youtube.com/watch?v=mWyfkFogGeU&list=OLAK5uy_k0IjOTynmaZNR9SldIRbJ5pdE8Y9ciD8k)

Note to self: I listen to a lot of live albums.