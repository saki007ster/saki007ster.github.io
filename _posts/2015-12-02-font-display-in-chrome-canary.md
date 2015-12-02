---
layout: post
title: CSS font-display property is now available in Chrome Canary!
---


**font-display** is a new @font-face descriptor and a corresponding property for controlling how a downloadable font renders before it is fully loaded. It allows you to customize how web fonts are displayed when the page is being rendered -- e.g. should the browser block text rendering until the font is fetched (default in Chrome, FF, Safari) vs. use fallback and then swap the font once fetched vs. check cache and use first available font vs... check out the full spec at: [here](http://tabatkins.github.io/specs/css-font-display/)

#### To test drive it in Chrome Canary:
- Boot up Chrome Canary
- Open chrome://flags
- Enable "enable-experimental-web-platform-features" flag
- Reboot Canary
