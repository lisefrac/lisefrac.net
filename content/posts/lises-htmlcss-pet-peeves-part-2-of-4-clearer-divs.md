---
title: "Lise's HTML/CSS pet peeves, part 2 of 4: clearer divs"
date: "2014-10-03"
categories: ["web-development"]
tags: 
  - "css"
  - "html"
  - "lises-htmlcss-pet-peeves"
---

This post is about another of my front-end web dev pet peeves: **clearer divs, and associated float/clear madness.**

(For those of you not webbily-inclined, we are _not_ talking about what happens when you flush the toilet. It is -- slightly -- more pleasant than raw sewage).

Clearer divs fit under the category of ["extraneous markup",](http://www.lisefrac.net/log/webdev-craft/lises-htmlcss-pet-peeves-part-1-of-4/) but I've given them their own bullet point because they INFURIATE me. Seriously, seeing a document riddled with this:

<div class="clearfix"></div>

Or worse yet:

<div style="clear:both;"></div>

...is enough to send me into a raaaaaage.

To explain the annoyance factor here, I need to explain a little about floats and clears for the front-end web dev n00bs in the audience. Most website layouts these days are based around multiple <div>s made into columns by applying the style "float:left" or "float:right" to them. Take this bit of markup:

<style>
#box {
   width:50%;
}
#left\_column {
   width:20%;
   float:left;
}
#right\_column {
   width:80%;
   float:right;
}
</style>
<div id="box">
   <div id="left\_column">This is the left column</div>
   <div id="right\_column">This is the right column</div>
</div>

The content within those <div>s will form themselves into two rudimentary columns which continue down the page indefinitely. Like this:

This is the left column and it goes on for as long as you have content to fill it

This is the right column and because it's wider it can go on longer and longer and longer and longer and longer

Unfortunately, it's that _indefinitely_ wherein the problem lies. **Elements that come after those two columns _will continue to contort themselves to accommodate that float, unless you tell them otherwise_**. This can cause a number of strange behaviors that are boggling to CSS newbies -- the source of 90% of problems when my friends come to me with their webpages and say, "You know CSS; make this work!"

"But Lise!" you say, "your two columns above aren't have any problems." Well, that's because I have cleared them. If you know your way around Firebug/Chrome Dev Tools, try toggling off the style on #box. You'll see something like this (picture):

![Screen Shot 2014-10-02 at 6.58.57 PM](http://ic.pics.livejournal.com/captainecchi/782718/23611/23611_300.png "Screen Shot 2014-10-02 at 6.58.57 PM")

So floats are tricksy, like hobbitses. But they can be countered by the `clear` CSS property. **I like to think of an element with "clear:both" on it as CSS Gandalf, spanning the width of the parent element and saying "None shall pass!"**

... I've just compared balrogs and hobbits. This LOTR analogy is breaking down, so let's leave it aside. Will miss pointy hat.

The easy, ugly way to clear a float is to put a new, empty element after it -- within the parent element -- with "clear:both" applied to it:

<style>
#box {
   width:50%;
}
#left\_column {
   width:20%;
   float:left;
}
#right\_column {
   width:80%;
   float:right;
}
.clear {
   clear:both;
}
</style>
<div id="box">
   <div id="left\_column">This is the left column</div>
   <div id="right\_column">This is the right column</div>
   <div class="clear"></div>
</div>

This will do the trick -- your successive content won't try to jump up into #box.

So what's wrong with it?

Well, it's non-semantic and extraneous markup, which [we've already talked about a little](http://captainecchi.livejournal.com/721665.html). That <div> isn't pulling its weight; it has no meaning on the page, and exists only for appearance reasons -- rather like a Wodehouse protagonist.

Moreover, **there are a bajillion (okay, five or so) _other_ ways to clear floats (more) semantically.** To name them:

**Floating the parent (in this example, #box).** Floated parent elements will expand to contain floated children. Understandably, this doesn't work everywhere; you may not want that element to jog to the left.

**Setting `overflow:hidden` or `overflow:auto` on the parent.** This is the method I used above to wrangle our columns. Like with floated parents, elements withÂ `overflow:hidden` on them will expand to contain floated children. It has a few cons to its use, however:

- It's not supported in IE7 or below. But none of us are supporting that any more, right
- `overflow:hidden` interacts weirdly with box-shadows
- Obviously, if you need a different value for the `overflow` property, this won't work for you

That said, I find a lot of use for this one, and it tends to be my go-to clear method.

**Set `clear:both` on an existing (unfloated) semantic element that follows.** Here you're doing what you're trying to do with a clearer div, on an element that would be on the page anyway. Dependent though it is on a very specific structure, this method is worth mentioning because this is common way of building a two column layout -- float one div left, float one right, and have a footer that spans the document beneath it. Put `clear:both` on the footer and you're good to go.

**The so-called [easy clearing method](http://www.positioniseverything.net/easyclearing.html)** (warning, dated), where you apply `clear:both` to an empty space inserted into the DOM via the :after pseudo-classes. I didn't use this one for a long time, due to lack of support in IE7 or lower for these pseudo-classes. It's also a tetch non-semantic. But with IE7 being phased out more globally, it has become the most generally applicable method of clearing something -- all the previous methods only work in a subset of cases.

**A slight improvement on this is the [micro clearfix](http://nicolasgallagher.com/micro-clearfix-hack/).** If you use Sass with Bourbon, it's the method you get if you use @include clearfix().

(And this is why I'm a front-end web developer -- so I can say my job involves sass and bourbon).

**One troubleshooting hint:** if you're seeing odd behavior on a page, and floats are involved, try inspecting the parent element in Firebug or Chrome Dev Tools. (You are using these, right?) If it appears with no height, and on selection doesn't appear to wrap its child elements, there's likely an uncleared float somewhere in there.

That's enough info, right?

. . .

All right, all right. I will acknowledge there may be corner cases where you have to stick `clear:both` on a piece of markup that wouldn't otherwise exist. But I have only rarely come across such cases.

In case this rant didn't help you to understand floats and clears, I point you towards a couple of my favorite resources. They are both a few years old, but -- aside from the browser bugs -- floats and clears haven't changed much in ten years. [http://alistapart.com/article/css-floats-101](http://alistapart.com/article/css-floats-101) [http://css-tricks.com/all-about-floats/](http://css-tricks.com/all-about-floats/)

Next time, HTML/CSS bugaboo #3 --Â **"nudging" with absolute and relative positioning.**
