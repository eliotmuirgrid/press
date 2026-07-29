# Reality

## How real is Flow Publish right now? I'll be very honest.

Not as real as I would like it to be.

That said, I can add documents to this website within a minute or two, and I can quickly edit the content by invoking ChatGPT from within **NEOVIM**, which is a new port of the VIM editor.

The source code is in Markdown:  
[https://github.com/eliotmuirgrid/press](https://github.com/eliotmuirgrid/press)

The publishing system is implemented using PHP. Frankly, it's a pain to set up. PHP is a stack of, ummm... very interesting and ultimately fragile dependencies.

[https://github.com/eliotmuirgrid/press-release](https://github.com/eliotmuirgrid/press-release)

It's ultra fast for me to publish a page—this is for you, Ashley ;-)

Some useful commands:  
- [`press:publish`](https://github.com/eliotmuirgrid/flowshell/blob/master/commands/press%3Apublish)  
- [`press:sync`](https://github.com/eliotmuirgrid/flowshell/blob/master/commands/press%3Async)  
- [`press:open`](https://github.com/eliotmuirgrid/flowshell/blob/master/commands/press%3Aopen)  
- [`git:publish`](https://github.com/eliotmuirgrid/flowshell/blob/master/commands/git%3Apublish)

Ed Worthington and his team put the PHP together for me in record time - faster than I could have done myself.  He and his
team are ultra competent.  It's not their fault that PHP has some issues in the longer term.
