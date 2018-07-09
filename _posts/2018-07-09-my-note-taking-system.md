---
layout: post
title: My Note-Taking System
---

I was using [xolox/vim-notes](https://github.com/xolox/vim-notes) for a while, but I didn't like their format. I also disliked that you couldn't put anything in folders, and that their markdown support was sketchy. So I switched to [vimwiki](https://github.com/vimwiki/vimwiki). I didn't like that either - there's no automatic index, it clobbers my markdown syntax plugin in a way that screws up regular markdown files, and really it barely provided any helpful tools for regular notes except for enter to link a word. What I really needed was notes with tags, being able to browse tags, and fuzzy search notes, contents, and tags. I also needed to encrypt my notes and sync them in some way. I had been using a private git repo for this but I was looking for something more robust.
<!--more-->

For this I have settled on [joplin](https://joplin.cozic.net/).

<img src="{{ site.url }}/public/images/joplin.png" width="2452" height="1516" alt="joplin" />
*Joplin in action*

It has an awesome 3-paned layout to browse and preview notes, tags, and search results. Enter opens a note in vim. It all gets saved to a sqlite db file, which I then encrypt easily with [yadm](https://github.com/TheLocehiliosan/yadm) using gpg encryption. You can also sync with dropbox, box.net, onedrive, etc. Joplin also has desktop and mobile clients, which was a pain for me to access before. I'm much happier with this than the other solutions I've used. I love that it stays in the terminal and still lets me use vim to edit my notes. I can also preview notes as html - I just use a chrome extension for this: [Markdown Preview Plus](https://chrome.google.com/webstore/detail/markdown-preview-plus/febilkbfcbhebfnokafefeacimjdckgl). I open the file in the browser and done. It auto-refreshes too.

Some more cool features:

* You can create a simple json config file to change or add your own keyboard mappings (I didn't like the default ones). My `keymap.json` is [here](https://github.com/mikedfunk/dotfiles/blob/master/.config/joplin/keymap.json).
* Search operates on contents, tags, and title automatically so you don't have to do separate searches in different ways. It also saves all of your searches in each session until you restart it so you can go back to recent search results.

The only problems I have with it are:

* There is no easy way to see what tags are set on a given note.
* After creating a note, it doesn't take you right to it. You have to search for it or scroll to it, then open it.
* You can't really link between documents since they open with a hashed prefix in the editor.
* Dropbox (or several other alternatives) is the closest thing to a centralized service to store your notes. It relies on another service rather than a joplin-specific one. Dropbox setup takes a little bit of work.

These are not really critical issues - joplin is still far better than my previous approaches. [Check it out!](https://joplin.cozic.net/)
