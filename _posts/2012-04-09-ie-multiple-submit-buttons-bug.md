---
layout: post
title: IE Multiple Submit Buttons Bug
---

I ran into a nasty bug recently that was totally unexpected. I had a form that needed to be submitted to multiple possible locations such as submit item and save draft. I am trying to chill on JQuery overuse lately so I Googled a solution for this. Turns out I'm in luck! You can have multiple submit buttons with the same name but different values. Whichever one you click will be submitted, while the other won't. Yay!

So I thought.

Unfortunately, if you Google "multiple submit buttons" and open an article, most of them don't mention a nasty IE 6-7 bug where this simple process fails silently. It's not a CSS bug. It's not a javascript bug. It's a bug in the way IE handles submit events, and it sucks.

Here's an example form. It just submits to itself and displays the value of the "action" button submitted. Check the source:

<script src="https://gist.github.com/mikedfunk/2344500.js"></script>

Here's what happens in IE6:

![IE6](https://dl.dropboxusercontent.com/u/28657/images/ie6_submit_test.png)

And here's IE7:

![IE7](https://dl.dropboxusercontent.com/u/28657/images/ie7_submit_test.png)

In both IE6 and IE7, It treats buttons strangely. It submits the text between the button tags rather than the value of the button. WTF? On top of that, IE6 just submits the value as the last submit button in the source order with that name, no matter which button you click. WTF! At least it seems to work as expected in IE8 and IE9.

So how do we fix it? With some JQuery duct tape.

First we strip the ```name``` and ```value``` attributes of the buttons. Retard IE can't figure them out. We'll replace them with some [twitter bootstrap](http://getbootstrap.org) style metadata:

    <button data-value="value one" class="btn" type="submit">Submit One</button>
    <button data-value="value two" class="btn" type="submit">Submit Two</button>

Then we add a hidden input for the action. We set a default value so the enter key will still work:

    <input type="hidden" name="action" value="one" />

Then we add some simple jquery to the top:

    <script type="text/javascript">
        $(function()
        {
            // on clicking one of the submit buttons
            $('button').click(function()
            {
                // get the data-value and assign it to the hidden action field
                var submit_val = $(this).attr('data-value');
                $('[name="action"]').val(submit_val);
            });

            // form submit, just to allow js to set the value before submitting
            $('form').submit(function(e)
            {
                e.preventDefault();
                $(this).unbind('submit').submit();
            });
        });​
    </script>

Now we're all set! The ```click``` event always fires before the ```submit``` event, even in IE6. It sets the value of the hidden input and submits the form. Here's our working file:

<script src="https://gist.github.com/mikedfunk/2344684.js"></script>
