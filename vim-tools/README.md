# Five Awesome Tools I Wish I Knew When I First Started My Vim Journey

<img src="https://github.com/olgam4/articles/blob/main/vim-tools/oliver-schwendener-uWdzlMWijiI-unsplash.jpg?raw=true" width="400" />

Some years ago, I switched jobs and lended with a mentor who only swore by `Dvorak` and `vim`. Although I was not convinced I had the mental space to learn yet another keyboard map, I had heard of `vim` in uni and decided to give it a go. As for any good programmer, I had stumbled upon `vim` when working on servers and got myself stuck in a buffer because I didn't know that in order to quit the thing, I had to use `:q!`...I think it has happened to most of us and instead of admitting myself beaten, I had decided that one day, I would use this editor and never be fooled again.

At first, I added `NeoVim` to my `Visual Studio Code` and only used some key bindings for navigating my document. I looked up some tutorials online and ended up playing some `VimVendtures` which helped me with `ewbhjkl`. After that, I learnt about `AIai` and `ciw` and did not think I would ever need anything else... But oh boy was I wrong!

I would agree that for `vim` to be worth it in your workflow, you need to *at least* be as efficient in navigating a document as you were with the `Cmd`, `Fn` and arrow keys. So here we are: I threw around some keys and would definitely recommend looking up those online, but this article is not about navigation with `vim`: it is about some tools I wished I knew when I first started with `vim`.

`vim` can be used as a very powerful `IDE`, it is portable and you can save your settings so that your environment can be recreated in a whim on another computer. As I said, I plugged `vim` into my `Visual Studio Code` at first and used their `Marketplace` to add plugins and whatnot...

The awesome thing I didn't know was that you could find tools to upgrade your `vim` experience and stop using those other tools...So here's a short list of them!

## ~ Plugin 'unblevable/quick-scope'

What is quick-scope? Well as you can see from the `gif`, it makes your buffer a multicolored happy place. The keen-eyed might have understood how it does it: it highlights the first occurrence of a letter so that you can jump around (or quick-scope) words in a line. Instead of jumping from word to word using `bwe`, you find (`f`) the highlighted letter and jump straight there. Not only does navigating a line become a breeze, you also look very snazzy when people watch you code with all those beautiful colors popping around.

## ~ Plugin 'ThePrimeagen/harpoon'

To be honest, `ThePrimagen` is probably the guy I looked up to the most back when I was starting `vim`. He streams himself coding, uses a keyboard-cam to flex his rapidity and is very instructionnal. Obviously, he has coded some `vim` plugins and this one I quite enjoy.

At first, when I switched to `vim`, I missed having the everlasting terminal at the bottom of my screen...And this harpoon only makes it better by giving you four of them! I mapped the plugin to be `,t[qwer]` and it lets me jump to a terminal and let it run in the background whilst I code. It can be very useful for testing, running your application et cetera. You can always use `:!` but this one changes your whole buffer to a terminal, so after you've run something, you can `/` the output which is an awesome feat!

## ~ Plugin 'tpope/vim-surround'

`tpope` has made a lot of `clojure` plugins and this is how I bumped into his work. This `vim-surround` tool lets you... quite simply...surround something! If you need to add parentheses around some argument, highlight some word in `markdown` or comment something...This plugin comes to the rescue! I highly recommend you give it a try, it has helped me numerous times in the past.

## ~ Plugin 'dbeniamine/cheat.sh-vim'

Who always remembers every last detail a language has to offer? If you do, bravo. But if you don't: here's an awesome tool which does it for you. Simply hover over some word, press `K` and voilà, it shows you in a new pane how to use that thing in particular.

It is very useful when you read some code: if you don't know that keyword does, just `K`. It supports a lot of languages and tools and can even be navigated without coming from a word and from there, you can search for some functionality and then use it for your purpose...Give it a try!

## ~ Plugin 'vimwiki/vimwiki'

The latter was a cheatsheet...This one is a wiki! I mapped mine to `,ww` and with that, I jump straight to a personal wiki. From there, you can link pages, add data, take notes... It has proven to be very useful for taking notes on mappings I was learning in `vim` and some todo I had given myself for my current projects.

## Conclusion

There are a lot more tools which I use in my workflow. If you are interested in looking through my `.vimrc` or chatting with me for tips and cues, don't be shy and hit me up any time! Also, if you would be interested in hearing more of my learnings I gathered from my short adventure with `vim`, let me know and I might be interested in sharing those in a future article. Have a good one ❤️
