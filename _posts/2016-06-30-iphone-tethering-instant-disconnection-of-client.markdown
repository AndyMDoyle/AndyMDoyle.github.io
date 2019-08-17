---
layout: post
title: iPhone tethering - instant disconnection of client
date: '2016-06-30 15:33:54'
tags:
- it
- ios
---

Today one of our users grabbed me for a bit of help with their company issued iPhone and laptop. For months they have been unable to tether their laptop to their iPhone and couldn't work out why. They hadn't reported it to us and were living in silence, but that's another matter.

The issue manifested itself in the laptop (Windows 7-based) connecting to the iPhone hotspot and almost immediately disconnecting. If you were quick, you would spot the blue tethering bar appear for a second on the iPhone before vanishing just as quick.

Out of pure luck, Windows displayed a notification on the desktop that it wasn't able to connect to the Wi-Fi hotspot, and in the message it displayed the hotspot name. What stood out was the name of the hotspot. Mixed in with the standard "John Smith's iPhone" naming was a non-ASCII character code right where the apostrophe should be.

Thinking this was odd I jumped in to **Settings** > **General** > **About** > **Name** and discovered the name contained a non-standard apostrophe. It wasn't the normal apostrophe that you access on the **123** section of the keyboard. This was one of the other apostrophes that you can access by long-pressing on that apostrophe key and selecting one of the presented options in the popup.

Here's an example to watch out for:

![](/content/images/2016/06/iPhone-apostrophe-1.png)
<center>*Left - A good apostrophe; Right - The problematic apostrophe*</center>

Notice in the example on the right, the apostrophe has a slight slant to it. It isn't a completely vertical mark as on the left. This is the big telling point that something isn't right.

As soon as this unusual character was removed, Windows was happy and is tethering away nicely.

