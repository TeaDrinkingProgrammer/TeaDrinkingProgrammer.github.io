+++
title = "I built my own theme!"
date = 2023-10-04
draft = false

[taxonomies]
categories = ["dev"]
tags = ["webdev", "rust", "blog"]

[extra]
lang = "en"
+++

# So … I built my own theme
It's called [tranquil](https://github.com/TeaDrinkingProgrammer/tranquil) :smile:.

You might think: didn't you just release this blog? Yes, that's right. At launch I already used a great theme called [Serene](https://github.com/isunjn/serene). I liked the theme a lot but wanted to change it a bit which I had some troubles with. The Serene theme is made with a very common pattern where each component has their own separate CSS class. This means there is a lot of overlap in the content of the CSS classes. The classes also used a bit too much pixel padding values for my liking. I had also wanted to try out Tailwind for a while, so I figured that re-implementing Serene in Tailwind would be the perfect opportunity!

The result is called [Tranquil](https://github.com/TeaDrinkingProgrammer/tranquil). The main feel is still the same as Serene, but there are some differences. The main difference is the styling: all styles have been rewritten/reimagined in Tailwind. Besides this, the Table Of Contents has also changed quite a bit: Serene uses a sidebar, but the CSS to accomplish this uses a lot of CSS black magic to work. I went for a simpler implementation by putting the TOC at the top of the article.
One of the best things about Serene is that it had features that to me had a right balance between added complexity and minimalism: a projects page, image zooming, some callouts and extra syntax using [KaTeX](https://katex.org/) and [Mermaid](https://github.com/mermaid-js/mermaid). The thing I was most surprised about was the comment system which uses [Giscus](https://giscus.app/). Giscus enables comments despite the website being static and not having a backend. It accomplishes this by "abusing" the Github discussion feature. This feature is meant to enable discussion on repositories, but Giscus uses it as a backend for its comment system. It works like a charm and means I don't need to handle account logins and storage, which is always a plus.

The theme wouldn't have been possible without [Isunjns Serene theme](https://github.com/isunjn/serene), which stands on its own. I also got a lot of inspiration from [FasterThanLimes blog](https://fasterthanli.me) which is very well designed and has great articles, so go check that out as well.

And if anyone remembers: yes, I haven't forgotten my Linux article. It has been posted simultaneously with this article :).