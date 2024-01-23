+++
title = "The Markup iceberg"
date = 2024-01-17
draft = false

[taxonomies]
categories = ["software"]
tags = ["markdown", "productivity"]

[extra]
lang = "en"
+++

# Word and WYSIWYG editors
I have been using Linux for some years now, and one dealbreaker that people name is "I cannot use Word on Linux and I need that". Granted, some people really do need Word: if you need to collaborate on files and your company has Office365, you don't really have a choice. If you don't have Office365 and work by yourself, an often heard rebuttal to the first question is "Just use Libreoffice or Onlyoffice", but I understand that these programs, while very powerfull in their own right, are not a true replacement. You can also use Word online. It works, most of the time :tm: but can have terrible issues. I could go on forever about the the half-broken, sluggish and bloated software suite that is called Office365, but that's besides the point.

No, a real Word replacement does not exist. But what do we mean when we talk about a "Word replacement". Most people think about Libreoffice or Onlyoffice like I mentioned earlier. These are so-called What You See Is What You Get editors and where invented in the early 90s to make it easier for the  average user to edit documents. Most people just use these editors and call it a day, but what if I told you there is another way.

# Top of the iceberg: Markdown as text

Many people are first introduced to Markdown by Github or some other developer-oriented tool. In these contexts, Markdown is mainly used to make some simple files like READMEs. Some other use-cases include Github Wikis and if you have worked with some of these kinds of text-first tools, you may have noticed how nice using Markdown is. It takes a bit of time to adjust, but it is quite intuitive and very readable as plain text. Another advantage is that writing with Markdown doesn't require you to stop everytime you want a title: instead of selecting the text you want to make into a title, clicking the "title" button", pressing enter and pray that you subsequent text is normal, you can just type `#title` and be done. Yes, at first you forget some things like the markup for a link, but you eventually get the hang of it. You can even use Markdown in a WYSIWYG editor which is the best of both worlds: you see your changes but you can still type fast.

You may think to yourself: "Why is this guy so enthousiastic about Markdown. Yes it is nice, but so far, I've seen nothing revolutionary"
You are right. the power of Markdown is not in text alone.

# Level 2: Layout as configuration
Markdown on its own is not very reMarkable (see what I did there): the power comes when it is combined with a layout configuration. Explaining this idea is easier with some examples. Take this very blogpost you are reading right now. It is written in Markdown and then taken by Zola to be rendered with a template. Three types of layout are used:

## Template level
The template layout is an html file. In this HTML file, I define how everything in and around the text should look. In the example I have the text of a blogpost which is made purple by the Tailwind class.
```html
...
<div class="text-purple-300">
{{ page.content | safe }}
</div>
...
```

The Template is where everything that is unrelated to the text should be put: it shouldn't matter what the text is. The things that do change should be defined in the:

## Frontformatter

Some things do change per text. In this case, frontformatters can be used. Frontformatter differ per use-case and app. The following frontformatter is for this very blogpost:

```toml
+++
title = "The Markup iceberg"
date = 2024-01-17
draft = false

[taxonomies]
categories = ["software"]
tags = ["markdown", "productivity"]

[extra]
lang = "en"
+++

The blog post text...
```

Like the name suggests, a frontformatter is put in front of the text in the markdown file itself. In this case, we define things like the title, the categories etc. In the case of Zola, the values that are defined in the frontformatter are used in the template like this:
```html
<h1>{{ page.title }}</h1>
```

This allows the template to use some dynamic values while still being generic.

But frontformatters are very powerfull: you can put just about anything in them. Take this example from [Marp](https://marp.app/), an app that allows you to make presentations with Markdown:

```markdown
---

marp: true

theme: uncover

class:
	- lead
	- invert

paginate: true

---

Slide 1

---

Slide 2
```

An important other thing to note is that, because frontformatters and templates work independently from the content, you can do a one-time set-up and never worry about your layout again. This exactly how I write these blogposts: I just write them, push them to git and voila: they all look the same.

As you can see, the universality of a template and a frontformatter means that many things that you would usualy use productivity software for, can be done in Markdown: we have already replaced Powerpoint and Wordpress. But how about Word?

# Level 3: Pandoc: more than a Word replacement

Pandoc is a library that converts one kind of document into another. This doesn't sound very remarkable but it does much morethan just convert files. Pandoc takes everything I have just showed and takes it to the next level: it allows you to define the layout of an entire essay in a frontformatter and then just start typing. Take this frontformatter I used for an essay I wrote:
```yaml
\---

header-includes: |
	usepackage{titlesec}
	newcommand{\sectionbreak}{\clearpage}

title: "Title"
lang: nl
papersize: a4paper
geometry: margin=2cm
fontfamily: roboto
fontfamilyoptions: default
documentclass: extarticle
fontsize: 12pt
linestretch: 1.2
#Table of Contents
toc: true
toc-depth: 3
\#Support for \ newline
from: 'markdown+escaped\_line\_breaks'
bibliography: 'citations.json'

\---

```

This YAML frontformatter contains everything I need to tell Pandoc to make sure every essay I write looks exactly the same. Some things will look familiar: options like title, lang and fontfamily are quite selfexplanatory. Some of these options might look a bit out of place though, like the "header-includes" option. This is because this option uses

# Level 4: Latex: the mother of all markup

LaTeX is the mother of all typesetting languages. It is used widely in academia but largely unknown outside of it. That's a shame, because it is very powerfull. One reason why it might be less popular, is because its syntax is not very easy to read. Compare these two snippets of LaTex and Pandoc Markdown:

```latex
    \documentclass{article} % Starts an article
    \usepackage{amsmath} % Imports amsmath
    \title{\LaTeX} % Title

    \begin{document} % Begins a document
      \section{title}
      hello there
      \newpage
    \end{document}
```

```markdown
---
documentclass: article
header-includes: |
	usepackage{amsmath}
---

# title
hello there
\newpage
```
As you can see, the seperation between settings and content is very clear in the Pandoc Markdown and the syntax is a lot more concise and easy to read. Pandoc Markdown also allows you to use snippets of LaTeX. This is very usefull for the 5% of the time when you need to do something which you can't do in Markdown, like start a new page. The result is still 95% readable Markdown with some LaTeX commands here and there. 

When using this setup, the pipeline is like this:

Pandoc Markdown -> LaTeX -> _anything_

This is usefull to remember when you are debugging your frontformatter: if LaTeX has an error, first look in your Frontformatter/Pandoc.
This anything can be a PDF document for example.

This pattern of most of the content being Markdown and a small percent being some kind of "escape hatch system" is very common when using Markdown. For some systems, the escape hatch is HTML (which is support most of the time as Markdown is a superset of HTML), most static site generators have "shortcodes" and as we have just seen, Pandoc Markdown has LaTeX.

# Essays with Markdown

Writing essays with Pandoc uses the afforementioned techniques, but there are some specific things I want add.

The first is [Zettlr](zettlr.com): it is an app that allows you to write Pandoc Markdown and has some nice features like citation completion, WYSIWYG support and more. The citations work together with Zotero, which is hands down the best citation manager I have ever used. The instructions of how to use it is [here](https://docs.zettlr.com/en/core/citations/) and the end result is a fully automatic pipeline that automatically adds all your citations and it is amazing.

# Markdown Everywhere

As you can see, between Github, Pandoc and Marp, you can do a lot you can do in Office, all using the same paradigm. You can do many more things, like have compiled code snippets with Rmarkdown. Working with Markdown everywhere has a few advantages:

- Define your layout once, use it everywhere
- Familiar syntax for very different applications
- Plain text: manipulate your files with any program that can work with plain text. Noboilerplate has a great [video](https://youtu.be/WgV6M1LyfNY?si=GsaXCvjGgq-v6KWD) on this.

All in all, I think the time investment of working these systems out is well worth the advantages, but you might disagree: I'd love to hear what you think.

P.S: I was so focused on writing this I can't remember what I listened too, but one of the albums was [Pretzel Logic](https://youtube.com/playlist?list=PLGr1IYuG8Wwv0LOsD1PUbjQu3dchzoOAW&si=9ZaiCZeAA25hi76l) by the great Steely Dan.



