---
layout: post
title: How I Use Tmux as a Development Environment
---

When I first started as an engineer at my current employer, I soon realized that I had to think a bit differently to keep things organized. At my previous employer, all code was basically in one codebase. We didn't use any complex build steps, just [vagrant](https://www.vagrantup.com/) for our backend/frontend and [gulp](https://github.com/gulpjs) to compile scss and [CoffeeScript](https://coffeescript.org/) assets (yes, this was a loooong time ago). So I could run a Vim instance and gulp in another tab in my terminal and I was good.

When I moved on, things were a lot more complex. We had at least five different services that needed to be running at once. Three of them needed front-end builds on save via [grunt](https://gruntjs.com/). Things have changed drastically since then - we now use a whole different, more modern stack, but it was more about the challenge of working with different services with different persistent processes. How could I stay organized and understand which context I was in? Where do I put persistent processes that I need to keep an eye on? [Tmux](https://github.com/tmux/tmux) helped me solve this problem years ago in an elegant way.
<!--more-->

## What is Tmux?

<img src="{{ site.url }}/public/images/tmux-blog-1.jpg" width="2452" height="1533" alt="Tmux" />
*Tmux in action with my fancy config*

Tmux is short for _terminal multiplexer_. It is a command-line program that runs in your terminal. You can install it with your package manager. For MacOS I use [Homebrew](https://brew.sh/): `brew install tmux`.

You might be saying, "I can already do this with my terminal emulator. Why do I need a command-line wrapper to layout my command-line sessions?" Well, the killer feature in Tmux is that it runs as a daemon. This means when you start a session with `tmux` or `tmux new-session -s my-session-name`, you can "detach" from it with `<prefix>d` and later "attach" to it with `tmux attach -s my-session-name` to continue working in that session. It continues running in the background, _even if you quit your terminal emulator_. If you restart and attach to that session, it will still be there.

Tmux allows you to split up your terminal into different contexts: Sessions, windows, and panes. What are those?

## Windows, Sessions, and Panes

### Session

A **session** is a top-level context. I think of it like the company I'm working for. Currently I work full time, so my only sessions are Work and Home. You can only view one session at a time, but you can open a handy switcher to switch between sessions. You can start a new session with `tmux` for the default session name or `tmux new-session -s Work` for a specific session name. You can open the session switcher with `<prefix>s`. I will explain what `<prefix>` means and some other foundational concepts shortly.

<img src="{{ site.url }}/public/images/tmux-blog-session-chooser.jpg" width="2452" height="1533" alt="Tmux session picker" />

### Window

A **window** is what I consider more of a tab in Tmux. I put everything related to one _codebase_ or _context_ in a window.

<img src="{{ site.url }}/public/images/tmux-panes.jpg" width="2452" height="1533" alt="Tmux windows and panes" />

For example, I use a [blog](https://github.com/mikedfunk/mikedfunk.github.io) codebase window with a Neovim pane, a [Tig](https://github.com/jonas/tig) pane for git operations, and a pane to run [Jekyll](https://github.com/jekyll/jekyll) to preview and generate my blog on save.

<img src="{{ site.url }}/public/images/tmux-blog.jpg" width="2452" height="1533" alt="Tmux blog window" />

I also use some windows not related to one codebase like [notes](/2018/07/09/my-note-taking-system/) and _mysql_ where I run [mycli](https://github.com/dbcli/mycli), [pspg](https://github.com/okbob/pspg), and Neovim for saved queries.

Finally, I run a _config_ window with these panes:

- [Neovim](https://github.com/neovim/neovim) to edit any user/system config files
- [Yadm](https://github.com/TheLocehiliosan/yadm) status to show my changes to my dotfiles
- [Ctop](https://github.com/bcicen/ctop) to show a dashboard of running docker containers
- [Htop](https://github.com/htop-dev/htop) to show what processes are taking up more CPU and memory

<img src="{{ site.url }}/public/images/tmux-config-layout.jpg" width="2452" height="1533" alt="Tmux config window" />

You can create a new window with `<prefix>c`. Close it with `<prefix>&`. Rename it with `<prefix>,`. Switch to next and previous with `<prefix>n` and `<prefix>p`. Switch to a specific, numbered window with `<prefix>{number}`. Or you could open the fancy window switcher to choose a window with arrows and enter with `<prefix>w`.

### Pane

A **pane** is also known as a split. It's a separate box in the current window that has its own shell running (e.g. bash or zsh). You can just have one pane, or you can have any number of panes, split up however you like.

There are even pre-defined pane layouts that you can cycle through with `<prefix><space>`. Some common pane shortcuts:

- `<prefix><down>`, `<prefix><up>`, `<prefix><left>`, `<prefix><right>` to move to the next pane in that direction
- `<prefix>%`, `<prefix>"` to create a new vertical or horizontal pane, respectively. `<prefix>x` to close a pane.
- `<prefix>z` to toggle zooming a pane to the full window size and back
- `<prefix>H` | `<prefix>L` to increase/decrease the vertical size of the paine , `<prefix>J`, `<prefix>K` to increase/decrease the horizontal size of the pane (these are custom bindings I have configured)
- `<prefix>{`, `<prefix>}` to move a pane left or right. `<prefix>r` to rotate the pane layout clockwise.

Some other useful panes I run for some codebases:

- Automatically run tests on save with [entr](https://github.com/clibs/entr). Jump to that pane to filter to a specific file or test. Send desktop notifications with [noti](https://github.com/variadico/noti) on success or failure.
- Open a persistent REPL for that codebase inside a running Docker container. If the container is down, keep trying to open the REPL until it's running.
- Monitor logs for that codebase with [multitail](https://github.com/halturin/multitail) This lets me combine multiple log sources and add custom regex-based coloring to the log output.

## What does `<prefix>` mean?

Since Tmux wraps your other command-line usage, they don't want to define a lot of keyboard shortcuts that could collide with what's running in a pane. So they use a "prefix" keyboard shortcut before running _any_ Tmux command. The default is `<ctrl-b>`. I like to remap it to `<ctrl-a>` which is the [Gnu Screen](https://www.gnu.org/software/screen/) default, just because it's more ergonomic. So once I start a Tmux session, if I want to open a new window, I would type `<ctrl-a>` followed by `c`.

## How do I configure Tmux?

You create/change keyboard shortcuts, change how Tmux looks, and more with a `~/.tmux.conf` file. If you want you can read `man tmux` to see how this works, or take a look at [my config](https://github.com/mikedfunk/dotfiles/blob/master/.tmux.conf).

My Tmux config is customized, which is why the status bar and colors look different. Tmux looks like this by default:

<img src="{{ site.url }}/public/images/tmux-default.jpg" width="2452" height="1533" alt="Tmux default" />

Some tools I use to make Tmux look and work the way it does in my screenshots:

- [Tmuxline](https://github.com/edkolev/tmuxline.vim) plugin for [Vim](https://www.vim.org) or [Neovim](https://neovim.io/) . This allows me to configure my Tmux statusbar colors and layout in lua and generate a new statusbar config on change. I then source that config in my main `~/.tmux.conf`. It can even use the same colors for your Vim and Tmux statusbars, background colors, etc. if you want.
- [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm) You can install vendor plugins to add pre-built functionality to tmux like jumping to the closest URL or file path, CPU and battery indicators for your statusbar, and other cool stuff
- [Navigator.nvim](https://github.com/numToStr/Navigator.nvim) If you use Neovim and want to navigate Tmux and Neovim splits seamlessly, you can install this Neovim plugin. I used it for a while but I found I prefer to keep the concepts of Neovim splits and Tmux splits separate.

## It's repetitive to set up Tmux windows and panes every time I use it. Is there a tool that automates this?

Yes, there are several. The one I use currently is called [Smug](https://github.com/ivaaaan/smug). It allows you to write pre-defined YAML layouts and spin up new sessions with one of those layouts. My favorite feature is manual windows. You can define some windows that don't get created by default, but you can run `smug start my-session-name:my-window-name` to _add_ them to the session for the configured layout. I do this with a Tmux keyboard shortcut. This means I don't have to start a session with every window/codebase ready to go. I can start some of them only when I need them, with all panes just how I like them. Saves a lot of memory usage.

Older alternatives to Smug:

- [Tmuxinator](https://github.com/tmuxinator/tmuxinator)
- [Tmuxp](https://github.com/tmuxinator/tmuxinator)
- [Teamocil](https://github.com/remi/teamocil)
- [Tmuxomatic](https://github.com/oxidane/tmuxomatic)

## Where can I learn more?

- [Tmux](https://github.com/tmux/tmux)
- [My Tmux config](https://github.com/mikedfunk/dotfiles/blob/master/.tmux.conf)
- [My Tmuxline layout](https://github.com/mikedfunk/dotfiles/blob/master/.tmux/tmuxline-dark.conf)
- My Smug [Home](https://github.com/mikedfunk/dotfiles/blob/master/.config/smug/home.yml) and [Work](https://github.com/mikedfunk/dotfiles/blob/master/.config/smug/work.yml) layouts

Thanks for reading!
