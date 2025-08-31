+++
title = "Less complexity, same interactivity, all with HTMX: adopting the Hypermedia mindset"
date = 2025-08-15
draft = false

[taxonomies]
categories = ["dev"]
tags = ["webdev", "Hypermedia", "HTMX"]

[extra]
lang = "en"
+++

## HTMX: beyond the hype

You might have heard about the buzz around HTMX and Hypermedia as of late. On the surface, HTMX sounds like it is solving a problem that doesn't exist: we have Single Page Applications, why would we need old-fashioned Multi-page applications. Well, it turns out old-school multi-page apps had one major advantage we abandoned when adopting SPA frameworks: server-side rendered websites do not have to synchronise state between the server and the client. But before I try to convince you that you can build interactive apps with server-side technology, let's see how we got here.

## How we got here

In the beginning God created the heavens and the earth. A bit later, in 1989, Tim Berners Lee created the World Wide Web. At the start of the internet, web-sites were simple compared to today: you requested a web-page and you got one back. Simple as that. Nevertheless, the idea of the internet was, and is still, quite revolutionary: a network of pieces of media (like text, video, audio), linked together through links. The term that was adopted for this idea was Hypermedia.

Hypermedia at the beginning of the internet had two problems, though: it was hard to make very dynamic or interactive problems. The first issue was quickly solved by languages like PHP, but a far more interesting one is interactivity. Because, as the internet progressed, people and companies were not just looking for static or even dynamic content, but for something resembling desktop applications. At the time, people started using JQuery to add little bits and pieces of interactivity to their websites, but as the interactivity requirements grew, people found that applications were becoming hard to manage. To solve this issue, people moved to ...

## Single Page applications

Single Page Applications were made possible by the rise of JavaScript as a language that could be used within the browser. Because single page applications run on the client-side, interactivity was not an issue any more at all. This is the reason most of the industry moved towards it and moved away from JQuery: we as developers want to make good experiences for the end-user. SPAs also come with a big disadvantage, though: they do not make use of the power of Hypermedia. In short, this means that, for SPAs, you need to keep state synchronised between the server and the client. This means that you have to do a lot of stuff twice: routing, authentication and authorisation, data validation/sanitation, translations, and most importantly: data serialisation and deserialisation.

## Hypermedia libraries: a modern spin on hypermedia

The new crop of hypermedia libraries, like HTMX and Datastar, promise a middle ground between both: most of the interactivity of a SPA, with the simplicity of an 'old school' hypermedia server. The way they achieve this is by leveraging a feature of hypermedia: hypermedia as the driver of state (HATEOAS). This is the central idea that, instead of sending JSON and then deserialising it and putting it in the DOM (the page), we can skip that and just send HTML and swap that into a specific place of the DOM. This simplified model means we can get rid of most complexity on the client side, while still keeping an interactive website.

## Hypermedia in action

One question I immediately had when hearing this HTMX approach, is how exactly you make apps with it that have a modern feel. I conceptually understood that it was possible, but I struggled with actually adopting the Hypermedia mindset. To show you how this works in practice, we will think through a problem I actually experienced: how to build a notification system. First we build think through the problem with a SPA mindset, afterwards we go through it with a Hypermedia mindset which will show us the advantages of the approach in practice. 

## The SPA way

I started designing it in the way I was used to: listen for a response to come in, take the message out of the response, then display it on the page, all with JavaScript. This is because I wanted a fade-out animation, and I didn't think you could use Hypermedia for that.

As some of you might expect, it got all got quite complex fairly quickly: how do I send the notifications to the client? How do I discard of outdated messages. In short: how do I sync the state of the server-side and the client-side..

In a SPA app, we would do something like this:
- The server sends down a JSON message with all the information you need:
```json
{
    "message": {
        "type": "success",
        "title": "Hi👋",
        "message": "Lorem ipsum dolor sit amet"
    }
}
```
- Receive the message on the client
- Set up a template with a for loop
- Call a library that displays your notification

If you wanted to display the notification without a library, you would also need to:
- Make a notification component, using a template if to make it visible or not
- Use for loop to list all notifications

As you can see, the main critique of SPAs is plainly visible here: you need to go from server -> JSON -> Client -> DOM

Let's take a step back and see what we actually need:
- A way to select a notification type
- A fade-out animation

From a SPA perspective, it seems like the most logical way is to translate JSON to HMTL and call it a day. It turns out though, that 90% of this problem can be easily solved with only a tiny bit of JavaScript logic if you use a Hypermedia approach.

## The HDA way

In Hypermedia, you start with, well, hypermedia! So let's start with a HyperText Markup Language (HTML) template with some Tailwind CSS styling (using DaisyUI):

```jinja2
 <div class="bg-white relative rounded-md shadow-md w-96 h-30 mb-4 mr-6 flex items-center gap-3">
        <div class="
            w-2
            h-full 
            {% if message.tags == 'success' %}
                bg-success
            {% elif message.tags == 'info' %}
                bg-info
            {% elif message.tags == 'warning' %}
                bg-warning
            {% elif message.tags == 'error' %}
                bg-error
            {% endif %}
        ">
        </div>
        <i class="
            bi
            text-lg
            {% if message.tags == 'success' %}
                bi-check-circle-fill text-success
            {% elif message.tags == 'info' %}
                bi-info-circle-fill text-info
            {% elif message.tags == 'warning' %}
                bi-exclamation-triangle-fill text-warning
            {% elif message.tags == 'error' %}
                bi-exclamation-circle-fill text-error
            {% endif %}
        "></i>
        <span>{{ message }}</span>
    </div>
```

As you can see, we don't need to communicate any metadata, like the type of message to the client, because we deal with that on the server. This is HATEOS in action: the HTML _is_ the state.

This works quite well, but what if we want to add a fade-out? Here, we can use a mix of CSS and a sprinkle of Javascript to make it work.

The first thing we add is the fade-out effect. You can do this using 'vanilla' CSS, but I opted to use the excellent Tailwind CSS Animated. If you have never looked at it yet, you should take a look at [their excellent configurator](https://www.tailwindcss-animated.com/configurator.html), that allows you to trivially put together CSS animations.

The following will animate the HTML:

```jinja2
 <div
    class="<other CSS classes> animate-delay-[5000ms] animate-fade-left animate-reverse"
    style="pointer-events:all">
        <div class="
            w-2
            h-full 
            {% if message.tags == 'success' %}
                bg-success
            {% elif message.tags == 'info' %}
                bg-info
            {% elif message.tags == 'warning' %}
                bg-warning
            {% elif message.tags == 'error' %}
                bg-error
            {% endif %}
        ">
        </div>
        <i class="
            bi
            text-lg
            {% if message.tags == 'success' %}
                bi-check-circle-fill text-success
            {% elif message.tags == 'info' %}
                bi-info-circle-fill text-info
            {% elif message.tags == 'warning' %}
                bi-exclamation-triangle-fill text-warning
            {% elif message.tags == 'error' %}
                bi-exclamation-circle-fill text-error
            {% endif %}
        "></i>
        <span>{{ message }}</span>
    </div>
```

Notice how we don't need any code to fade out the notification. We leverage the fact that the CSS delay will start once the notification is in the DOM, in other words: we use the HDA flow to our advantage.

This will create a small problem, though: if we keep receiving notifications, the notifications will fade away but pile up in the DOM. I would also like the user to be able to dismiss the notification. If you are not very familiar with Hypermedia apps, you might think this is impossible to do within the paradigm and we need to grasp for "hacks". This isn't the case, though: we can do some scripting while still working within the constrains of the Hypermedia architecture.

Scripting? I thought Hypermedia Driven Apps were all about _not_ using JavaScript?

Well, this is partially true. The HDA archticture is all about using Hypermedia to transfer state instead of maintaining both client-side state and server-side state and having to synchronise it. Scripting can absolutely fit in this paradigm, as long as the script doesn't start maintaining state that is relevant for the server. Carson Gross, the guy behind HTMX who has lot's of excellent essays on SWE and Hypermedia, has written [a great article](https://htmx.org/essays/hypermedia-friendly-scripting/) about how scripting fits in to HDA apps.

In this example, we have already used our hypermedia response and some CSS to instruct the client to fade out the element after a certain time. We just need a tiny bit of scripting to remove the element after the CSS animation is done. We could do this in Vanilla JS, but there are tools that slot into the hypermedia paradigm a lot better, especially with regards to [Locality of Behaviour](https://htmx.org/essays/locality-of-behaviour/). The authors of HTMX have built [Hyperscript](https://hyperscript.org/docs/#introduction) for this purpose, but I prefer sticking with what I know, so I went with AlpineJS. [AlpineJS](https://alpinejs.dev/) is a lightweight Javascript library that makes it a lot easier to enhance HTML with some scripting. In that way, it is similar to JQuery, but it's syntax takes notes from modern SPA frameworks and it respects Locality of Behaviour.

In our example, adding this behaviour is a piece of cake:

```html
    <div
        x-data
        @click="$el.classList.replace('{{ default_delay_class }}', '{{ click_delay_class }}')"
        @animationend="$el.remove()"
        class="...">
        <div class="
            w-2
            h-full 
            {% if message.tags == 'success' %}
                bg-success
            {% elif message.tags == 'info' %}
                bg-info
            {% elif message.tags == 'warning' %}
                bg-warning
            {% elif message.tags == 'error' %}
                bg-error
            {% endif %}
        ">
        </div>
        <i class="
            bi
            text-lg
            {% if message.tags == 'success' %}
                bi-check-circle-fill text-success
            {% elif message.tags == 'info' %}
                bi-info-circle-fill text-info
            {% elif message.tags == 'warning' %}
                bi-exclamation-triangle-fill text-warning
            {% elif message.tags == 'error' %}
                bi-exclamation-circle-fill text-error
            {% endif %}
        "></i>
        <span>{{ message }}</span>
    </div>
```

In our case, we just needed to add three lines:
- x-data is needed to 'turn on' AlpineJS in this element.
- @click is an attribute that takes a function and executes on a click event. Click is not the only event, any event can be placed after @, including, very helpfully, HTMX events.
- $el is a 'magic' directive which returns the current DOM element.

With that, this code does two things:
- When the element is clicked, replace the 5000ms (5s) delay with a 1000ms (1s) delay.
- When the animationend event is raised, remove the current element.

That's all the JavaScript we need to make this notification _as dynamic as a SPA app_ with a fraction of the code.

To integrate this message system in my Django application, I created a simple middleware that adds the following snippet to the end of any response that was made using HTMX:

```python
class HtmxMessagesMiddleware(MiddlewareMixin):
    """Middleware to append the message partial to HTMX responses with messages."""

    def process_response(self, request: HttpRequest, response: HttpResponse) -> HttpResponse:
        """Process the response and chain message partials for HTMX requests."""
        # Is this request not an HTMX request? Let the normal response continue
        if not request.headers.get("HX-Request"):
            return response

        # If there are notifications for this request
        if messages.get_messages(request):
            # Render the notification template
            message_html = render_to_string("partials/messages-update-partial.html", request=request)
            # And add that at the end of the already existing response.
            response.content = response.content + message_html.encode()

        return response
```

To configure how this should behave, we only have to wrap the component inside this div: `<div id="messages" hx-swap-oob="beforeend">`. The `hx-swap-oob` attribute means that the contents of the div should be swapped in a different place than the main hypermedia. This allows us to 'tag along' this hypermedia snippet along with form errors, for example. The `beforeend` argument means it will swap it at the end of the div, so it is swapped in at the bottom.

The last thing we have to do, is put the following HTML in the base.html file:

```
<div id="messages"
        class="z-50 fixed inset-0 flex flex-col-reverse items-end justify-start h-screen w-screen"
        style="pointer-events:none">{% include "partials/messages-partial.html" %}</div>
```

It styles the div so that it is above everything else (`z-50`), puts it on the bottom left (`inset-0`) and reverses the order so the elements go from the bottom up. The include statement references our previous HTML.

And that's it. We have a full notification system that is responsive, modern and integrated with our messages framework all with minimal code and only a few lines of client side scripting and no meaningfull client-side state or logic.

## Conclusion

I hope I have convinced you that modern applications with good UX can be made with HTMX and do not require SPAs per se. Of course, not all applications are a good fit for hypermedia, Carson has already written a [great article](https://htmx.org/essays/when-to-use-hypermedia/) on that. But I always apply the 80/20 rule: 80 percent of websites are Wordpress, and of the other 20%, 80% websites are mostly fancy CRUD interfaces. In those cases, using Hypermedia can significantly decrease development complexity, with all the advantages that brings.

In my next blog post, I want to show some more advanced examples of creating interactive elements using HTMX and Django, so stay tuned for that.


## Further reading

Carson Gross is a great and engaging writer while also being a memelord at the same time. It's a combo that seems to be working well :).
- [His chaotic Twitter page](https://x.com/htmx_org)
- [His great articles](https://htmx.org/essays/)
- Hypermedia systems: a book written by Carson Gross, Adam Stepinski and Deniz Akşimşek which goes into the philosophy of Hypermedia. It is really easy to follow and I highly recommend reading it. The book is free to read online or about 10 euros as an ebook in most online retail stores.
- [The Grug Brained Developer](https://grugbrain.dev/): a hilarious article (??) in caveman language that actually contains some great advice.

I also want to highlight the [Bugbytes Youtube channel](https://youtu.be/akd7u69k27k?feature=shared). He has a lot of excellent videos about how to get hands on with HTMX and Django, as well as how you combine with other libraries like DaisyUI.

P.S: I wasn't listening to anything in particular when writing this post, but lately I have been listening to the album [Garden of Hera](https://www.youtube.com/watch?v=GvdPkclVeFE&list=PLP9SWLrsGSn93_66KMQBGVT-n5ASl5yhc) from OGENE. Dutch folks from my age might remember them going to the Junior Eurovision Contest in 2007. With this album, they have really chosen their own path and it shows. It's nice to see a bit more of that in the music business.