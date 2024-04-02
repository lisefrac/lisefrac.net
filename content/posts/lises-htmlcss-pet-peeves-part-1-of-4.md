---
title: "Lise's HTML/CSS pet peeves, part 1 of 4"
date: "2014-10-02"
categories: ["web-development"]
tags: 
  - "css"
  - "html"
  - "lises-htmlcss-pet-peeves"
---

_Edit Mar 25, 2024: Much of this is wildly out of date, as the web has changed dramatically in ten years. But I'm keeping it around for posterity, as fundamentally the opinions are still ones I hold. Of course, as you can see, I never wrote part 3!_

I've been a front-end web developer full-time since 2010, but I've been playing with HTML and CSS since 1997. I remember the paradigm shift from tabular layouts to CSS positioning. I remember IE for Mac. I recall the dark days before Firebug and Chrome Developer Tools. I remember \*shudder\* the <blink> tag.

And in that time, I've seen a lot of bad code\*, mang.

In particular, there are **four things I see again and again that bug me.** They are newbie goofs, or they are the kind of things non-specialist\*\* developers do. They are common mistakes which I guarantee I made a metric shitload of when I was first starting out.

I only hope that by sharing this, I can save you some time :)

The four pet peeves I'm going to address in four posts are:

1. **Extraneous markup**
2. **Clearer divs** (and general float/clear madness)
3. **Over-using absolute/relative positioning for "nudging."**
4. **Over-using the !important flag.**

Let's get right to the first one: **Extraneous markup**

This is rather broad, but let me give you an example, based on something I see a lot in my job:

<div id="box">
   <a href="#">
      <p>line 1 of text</p>
      <p>line 2 of text</p>
   </a>
</div>

The purpose of this markup is to make a link that spans multiple [block-level](http://www.impressivewebs.com/difference-block-inline-css/) elements. This is not default behavior for a link--<a> tags are inline elements by default in most browsers--but it is possible and a common need. <div>s on the other hand are block-level by default. **In essence you're making the link block level by wrapping it in a block-level element.**

It works, but you have to make sure the link expands to fill the <div> so the whole block is clickable, being sure to account for padding, etc...

... or you could **_just make the <a> block level._** Seriously. It's one line of CSS: `display:block;`. Just do it, and can the <div>. It gives you this slightly neater HTML:

<a id="box" href="#">
   <p>line 1 of text</p>
   <p>line 2 of text</p>
</a>

(I just did a test in Chrome, and it looks like these days you don't even have to set `display:block;` on the <a>. I'm pretty sure this was not always the case).

Other things that get my goat: - **"Spacer" blocks**, i.e. empty elements that exist only to add space to a site design. Remember those days before CSS borders, when creating a vertical rule was hard? This is no longer the case! These days we have margin and padding and borders and outlines, and we should use them. - **Elements with no styles applied to them.** If a tree falls in the forest and no one is there to hear it, does it make a sound? If an element has no styles attached to it, can it really be said to live at all? - **[non-semantic markup](http://www.vanseodesign.com/web-design/semantic-html/) in general**, i.e. things like <p class="red">.

That's all for now, but the next post deals with my favorite (not really) non-semantic markup bugaboo: **clearer divs.**

\* I used to be pedantic about not calling HTML/CSS "code" because it's not procedural. But a) I am softening in my old age, b) I also write JS these days, too, so I can get away with it. \*\* Unsolicited opinion time: I think "full-stack development" is getting to be a worse and worse idea every day. The body of knowledge in front-end development has become large, and I think it's unrealistic to expect someone who's spent their career hacking at C++ to have a thorough understanding of floats and clears, the cascade, and cross-browser quirks.
