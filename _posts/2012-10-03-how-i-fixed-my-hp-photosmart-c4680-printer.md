---
layout: post
title: How I fixed my HP Photosmart C4680 Printer
categories:
- blog
---

Here's how I just saved ~$300 by fixing my *HP Photosmart C4680* printer/scanner.

# The Problem

After I [risked everything and moved to Florida](http://www.ericmitz.com/why-i-risked-everything-and-moved-to-florida/), I found that my HP printer was having a little...issue. It seems liked it had a mind of its own. The touchscreen panel in front that's used to control the printer would select menus and options without even going near it. It would cancel itself in the middle of printing and scanning and generally became unusable. I figured it was busted in the moving process and we would have to buy a new printer.

<!--more-->

Luckily I did a little research first. I found [this discussion thread](http://h30434.www3.hp.com/t5/Other-Printing-Questions/My-HP-Photosmart-C4680-has-been-possessed-by-the-devil/td-p/561635) that appeared to be the exact same problem I was having. The printer being "possessed by the Devil" sounded about right. 

Thanks to user "CamelJockey", I learned that it was a fairly common problem and had a relatively easy fix as long as you didn't mind "getting your hands dirty" a little bit. 

It turns out the problem was a blown capacitor on the control board. You could verify this by opening the top of the printer and looking at the little green capacitor. If the top of the capacitor is "bowed" at the top, it's probably blown.

# The Fix

To fix it, I ordered a [330uF 6.3v](http://www.amazon.com/gp/product/B0084PA3JQ/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B0084PA3JQ&linkCode=as2&tag=wwwdigmyhonda-20) capacitor on Amazon for a whopping $0.92 cents. 

1. Disassemble the top of the scanner (there are four, black [Torx head screws ](http://www.amazon.com/gp/product/B000S8ZZG8/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B000S8ZZG8&linkCode=as2&tag=wwwdigmyhonda-20) holding it down). 

2. Reach behind the control panel where the power button is and release the clip holding the panel in place. It will come free. There is one screw behind the panel that's a bit difficult to get to.

3. Disconnect all the cables and connectors from the logic board towards the back of the printer where the power and USB cables plug in.

4. There are three silver torx head screws holding the logic board in place. Remove those and gently remove the board.

5. Identify the blown capacitor. It's green and should say TEAPO on the side. Here it is circled in red.

![HP4680 logic board](http://i.imgur.com/Z4y1J.jpg)

6. Fire up your [soldering iron](http://www.amazon.com/gp/product/B0006NGZK0/ref=as_li_ss_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=B0006NGZK0&linkCode=as2&tag=wwwdigmyhonda-20) (it doesn't have to be anything fancy) and heat up the leads to the capacitor underneath the board. 

7. Pull on the capacitor while you heat up the leads and it should pop free once the solder is melted. 

8. Insert the new capacitor leads into the board. Make sure the negative side of the capacitor lines up with the white shaded part of the logic board.

9. Heat up the capacitor leads and apply a small amount of solder to each lead.

10. Re-installation is the reverse of removal. Enjoy!