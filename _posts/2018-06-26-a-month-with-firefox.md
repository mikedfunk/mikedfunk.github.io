---
layout: post
title: A Month With Firefox
---

I was browsing reddit recently and found a topic about how Chrome is suprisingly poor on privacy. By default it collects data on what sites you browse and when. I had also heard that Firefox quantum has surpassed Chrome in speed and that the dev tools are just as good if not better than Chrome's. So I thought what the heck, I'll try out Firefox as my default browser for a bit and see how it goes.

Let's see how the two browsers compare from a web developer's point of view.
<!--more-->

## General Impressions

* Profiles are FUCKED. I had to use [MultiFirefox](https://davemartorana.com/multifirefox/) (`brew cask install multifirefox`) to even get close to what I was used to with chrome. And then I had two firefox apps running at once with no differentiation in the logos. My biggest complaint. I had to get used to cmd-tab rather than cmd-\`. This actually adds up to a lot of lost time because I cmd-tab to the wrong firefox, then cmd-tab to the right one, then cmd-tab back but end up at the wrong firefox again, etc.

<img src="{{ site.url }}/public/images/multifirefox-window.png" width="700" alt="MultiFirefox" />
*Eew.*

<img src="{{ site.url }}/public/images/multifirefox.gif" width="735" alt="Firefox Confusion" />
*How do I know which profile this is?*

* There is no easy way to create a keyboard shortcut to show/hide the bookmark toolbar. I tried setting it up in mac keyboard settings but it didn't work until I did it once via the menus first :/ And for some reason even then it only worked on my work profile.
* Columns in the network tab of the inspector are not reorderable... and not even _resizable_! This is really frustrating when you're just trying to see where a request came from without having to select each one. Can't I at least expand the address column??? WTF! (This is a filed bug on Mozilla's bug tracker btw)

<img src="{{ site.url }}/public/images/network-tab.png" width="600" alt="Network Tab" />

That "File" column - that's as big as it gets. If you have any query string params you can't see what the damn url is unless you open the detail pane!

* UI uses less room at the top if you right-click the toolbar, click Customize, and select Density: Compact. The boxy look of the tabs actually looks good and allows fitting more tabs on the screen.
* You can still drag tabs to reorder or to a new window.
* I never had any slowdown issues, which was one of the reasons I wanted to try it out.
* Notifications in firefox have a bling sound that sometimes plays _in addition_ to the sound you (or the app) have configured for an app's notifications. This is really annoying!! Only solution I know of is to go into system preferences -> notifications -> firefox and uncheck "Play sound for notifications". Not what I wanted but at least got rid of the blingbadonk.
* Toolbar customization is pretty much just like it used to be. You can make it look very minimal just like chrome. The only thing is you can't move the search bar from the bottom to the top.
* `about:config` is equivalent to `chrome:flags`. It is _way_ uglier and has no descriptions on each flag. It barely even has titles as they are just the actual `snake_case.flag.keys.with.dots`.

<img src="{{ site.url }}/public/images/about-config.png" width="600" alt="about:config" />
*Blech*

* You can't make your own search engines like in Chrome! "Get more search engines" takes you to the addon page. Frustrating! That was really useful to open jiras, zendesk tickets, pull requests, etc.
* Firefox account works fine to save all of my settings. They push you to get the mobile app when you register, which is kind of annoying. They also keep bringing up little notification bars to try to get me on this beta program which does optimizely-like experiments with ui. Not interested, but there is no "stop showing me these"
* It's fast and I never got any slowdowns like I did in chrome.
* In the dev tools, Instead of "Application", there is a "Storage" tab, which works just as well. There is also a "Debugger" tab which does what it says... but there's no editing in place like Chrome. It only shows html and javascript, so you can't view css and source-mapped source files.

## Extensions

* [LastPass](https://www.lastpass.com/) seems to be a bit behind the chrome version. You can't click to copy a generated password for instance.
* Firefox has tab reordering with keyboard shortcuts built in so you don't need an extension!
* It also has a gorgeous interactive json preview built in
* Markdown preview is not great - the only one I could get working had no themes :/ I also had to go into about:config to let it access file:// urls. In chrome this is done via extension permissions. Chrome version: [Markdown Preview Plus](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl). Firefox equivalent: [Markdown Viewer Webext](https://addons.mozilla.org/en-US/firefox/addon/markdown-viewer-webext/).
* You can completely hide extension icons unlike Chrome. You can also put them in an overflow menu sort of like Chrome. I like this flexibility.
* [SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega), [Stylish](https://addons.mozilla.org/en-US/firefox/addon/stylish/), [React DevTools](https://github.com/facebook/react-devtools), [Redux DevTools](https://github.com/reduxjs/redux-devtools), and [OctoLinker](https://github.com/OctoLinker/OctoLinker) all work great
* I found an alternative to [Jirafy](https://chrome.google.com/webstore/detail/jirafy/npldkpkhkmpnfhpmeoahhakbgcldplbj) (chrome) called [Github Jira Ticket Link](https://addons.mozilla.org/en-US/firefox/addon/github-jira-ticket-link/). It's really bare bones but it does what I need.
* Addons install almost instantly just like in Chrome now
* Themes are fantastic - you can even preview them very quickly before choosing one.
* There are a lot of old extensions in the addons store that are not available for my version of firefox. I'm not sure why they even show up in search results if I can't even install them.
* Mozilla has a cool [Facebook Container](https://addons.mozilla.org/en-US/firefox/addon/facebook-container/) extension that sandboxes facebook to prevent other sites from accessing facebook data.

## DuckDuckGo

* I also switched to [duckduckgo](https://duckduckgo.com) as my search engine. This is almost as capable as google and has an even nicer design with keyboard navigation built in. (j,k,enter)

<img src="{{ site.url }}/public/images/duckduckgo.png" width="600" alt="duckduckgo" />

* It does github repo details when you find a matching repo
* Image, video, and maps search are not as good. They just don't show as many of these rich results, sometimes none at all.
* Awesome color themes and generic cloud saving with just an anonymous passphrase. You can customize everything from colors to fonts to fixed header, center layout, wide layout, etc. Prettier than google by far.
* On chrome it prompts you to install their extension which improves privacy.
* Super fast.
