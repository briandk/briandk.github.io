---
title: Window translucency behavior is weird in Yosemite screenshots
date: 2014-10-20T18:26:27+00:00
author: Brian Danielak
layout: post
---
Apple&#8217;s [translucent design](http://www.apple.com/osx/design/) in OS X 10.10 (Yosemite) has some weird consequences.

My friend [Adam](http://alloy-d.net/) took a screenshot of Safari running on his Mac using Cmd+Shift+4. When he sent it to me, I used my iPhone to capture some odd behavior: when I tapped the image in our Messages thread, the appearance of the _screenshot_ changed depending on whether the background I was viewing it under was black or white. When the background was black, the Safari window completely changed in appearance.



This color-changing behavior struck both of us as weird, because Adam sent me a static _screenshot_. The only explanation we could come up with was that in the screenshot Adam took, OS X included some alpha channel information for the safari window itself.

To test our guess, we both fired up Preview.app, opened the screenshot, and captured how it looked when we adjusted Preview&#8217;s &#8220;Window background&#8221; setting:
<figure id="attachment_103">

  <img
    src="/wp-content/uploads/2014/10/Preview_app_settings.png"
    alt="In Preferences you can change the default background color of Preview windows." class="size-medium wp-image-103">
</figure>

With a background set to white, the Safari window itself appears light, with well-defined delineations to visually separate tab titles. When we switched the background color to black, the Safari window darkened considerably, and tab delineations were much harder to spot. Curiously, changing the background color in Preview didn&#8217;t affect how the underlying wallpaper in the screenshot (in this case, flowers) looked at all. The background color change only affected the Safari window, which itself was in focus.
<figure id="attachment_104">

  <img
    src="wp-content/uploads/2014/10/2014-10-20-yosemite-screenshot-translucency.jpg"
    alt="screenshot showing that in Preview.app with a black background color, the Safari window appears dark; in Preview.app with a white background, the Safari window appears light"
    class="size-medium wp-image-104">

</figure>

This behavior isn&#8217;t necessarily &#8220;bizarre,&#8221; though it did for awhile have me convinced of some kind of hidden voodoo when I [viewed the image on my iPad](https://vimeo.com/109505755).
