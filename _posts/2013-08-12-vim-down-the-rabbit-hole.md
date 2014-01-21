It's been a strange journey into the annals of Vim, but I'm now pretty comfortable using Vim as a PHP IDE. How did I get here?

## It all started when I was born…

Well not that far back. I started out in Dreamweaver, which is still good at dealing with HTML markup. It sucks at everything else though. When Coda came out, it really looked great. After quite a few years with Coda, it was showing it's age.

I was about to start fresh on a new, large application in a team environment. I wanted to do things right from the start. I wanted an integrated debugger, PHPUnit support, PSR-2 validation, jump to definition, code folding, Git support, fuzzy searching, and more. Eventually I made a comparison chart with the features I wanted. Coda was missing quite a few. I added PHPStorm and Sublime to the chart.

I'd heard a lot of good things about Vim. I overcame my terminal phobia years ago, so I put Vim on the list too. As I colored the grid boxes green or red, I was shocked to learn that Vim was all green. Not only that, some of the features had a better implementation in Vim. I still feared the 90º learning curve but looking at the chart, the numbers didn't lie. So I dove down the rabbit hole.

## Learning to walk again

It was dark, I kept falling and was very slow. But like anything in life, hard work and determination will see you through. Here are some resources I used to get started:

* VimCasts - Awesome screencasts to teach you about vim features and plugins
* Shortcut Foo - keyboard drills to burn muscle memory
* Android Vim flashcards - look in the shared flashcards in this app. Someone posted a ton of great Vim ones.
* Learn Vim Progressively
* Using Vim as a PHP IDE - I started out using this, but later switched to a Vim distribution. It will really show you the power of Vim though
* The Vim learning curve is a myth - I was happy to hear this. :)
* Vim Genius - A great site to learn vim techniques
* Using Github to manage your dotfiles - This works great and makes my entire setup portable! Here are my dotfiles.
* Top 10 pitfalls when switching to Vim - Good to know

I learned about modes, text objects, motions, and search/replace. I was committed to finally making the switch, so I voraciously consumed any information I could find. I learned about themes, a file browser plugin, a fuzzy finder. I learned how to customize my .vimrc file and manage plugins with vundle. It wasn't long before I realized that Vim tends to end up with a bunch of plugins and a pretty hefty config file. I was doing ok with my mishmash of stuff I found on the web when I found a secret weapon.

## The BFG of Vim tools

This dude Steve Francis set up an open source package of Vim additions called spf13-vim. It has a one-line install script and includes a bunch of awesome plugins and configurations out of the box. What's even cooler is you don't have to edit his .vimrc directly - you make your own .vimrc.local file and edit that. You can even tell it to remove plugins you don't like and add ones you do. AWESOME!!

By this time I've gone well past the room of many sizes and the cheshire cat, but another game changer was about to appear.

## Here comes a new challenger!

Ok, it's only tangentally related to Vim but this tool is by far the most useful thing in Vim for me. It's called Tmux - the Terminal Multiplexer. It allows you to split your terminal into multiple terminal window panes with different processes in each. Oh, and it also gives you tabs of window panes. Oh, and it also has "sessions" aka contexts. For instance Home and Work. You can switch between them and the other stays running in the background. In fact, even if you quit the terminal, Tmux stays running in the background. When you come back, you can re-attach and everything is just as you left it! If that's not enough, you can also do pair programming remotely with Tmux. Whoa!

## I can dance all day

I could go on and on about all the stuff I've learned since that fateful day at the edge of the rabbit hole. But now I'm all in, having tea with the Mad Hatter. I am so used to the modes and faster movement commands, I get annoyed using other text editors or even browsers or the finder. Vim isn't a perfect silver bullet of course, there will always be things an IDE does better. But it does all the things on my list quite well for free. How many other editors have 30 years of development behind them? Vim's community is still vibrant, with new plugins coming out all the time and tons of cool people willing to help you learn. There are tutorials, articles, flashcards, interactive learning courses, cheat sheets, subreddits, and IRC channels.

> “Alice came to a fork in the road. 'Which road do I take?' she asked.
> 'Where do you want to go?' responded the Cheshire Cat.
> 'I don't know,' Alice answered.
> 'Then,' said the Cat, 'it doesn't matter.”
