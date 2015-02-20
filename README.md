# Dot Files for West Arete

These are the common dot files that we share across our home directories.

As of yet, there is no fancy installation script; just manually put these in
place, or blend them with what you have now.

They're named here without the leading dot, so that the repository is easy to
work with. You'll need to rename them e.g. from `gemrc` to `~/.gemrc` when you
install them.

# Pimp my command line

I would suggest using [Iterm2](https://iterm2.com), it's like the standard Mac Terminal but better, if for no other reason than it makes it really easy to install color schemes. But it's also generally better than Mac Terminal overall. 


## Vim
Vim _can be_ very powerful, but as it ships out of the box it's basically
terrible. The solution is to install a zillion plugins and write a long and
complex configuration file for it. Or have your coworkers do that for you. Lucky you.

### Install the things
1. `brew install vim` The one that ships with OSX isn't very good. You like copying-and-pasting, right? Then install the homebrew version.
2. `brew install the_silver_searcher` Mega-fast implementation of the ack command, used in our vim config for searching and quick-opening files.
3. `git clone https://github.com/gmarik/Vundle.vim.git ~/.vim/bundle/Vundle.vim` Vundle, as the name suggests, is like Bundler for vim plugins.
4. Move all config files (described below) into place.
5. Open vim and run `: PluginInstall` to tell Vundle to install all the vim plugins.
6. If it's your first time using vim, please record a screencast of you trying to quit vim, then post to Slack. [Vim Adventures](http://vim-adventures.com) is a really fun way to learn if you don't know vim already.

### Configuration
I've split the vim config up into several files, here's the breakdown. (Full disclosure: this is heavily inspried by how Thoughtbot does it.)

* `.vimrc` Main config file, contains the boilerplate configuration that all of us can agree upon. You _should_ skim through this because it's well commented, you _should not edit_ this file to your own personal tastes, there's a better way...
* `.vimrc.local` Is where you put your own personal configs if you desire. If you find a config you just can't live without, send a pull request and maybe we'll add it. Likewise if you think I went totally overboard on the main .vimrc, send a pull request and we can pare it back.
* `.vimrc.bundles` Is like the Gemfile of our vim config, which contains a boilerplate set of plugins that we can all agree upon. You _should_ read through it because I took the time to comment everything, you _should not edit_ this file.
* `.vimrc.bundles.local` Is where you can add your own bundles until your heart's content. If you discover a really cool bundle you can't live without, maybe we can add it to the main .vimrc.bundles file.
* `.vimrc.themes` The prettiest vim themes require you to install a corresponding theme in your terminal. This presents a problem when tmux pairing with someone who has a _less than pimped_ terminal. I split the theme configs out into their own separate file so when someone goes "Ugh, how can you read that yellow text on a white background?!" you can quickly switch to a different theme. _Do not delete the lines in here, just comment them out/in!!_
* `.vimrc.rails` West Arete goes rogue when it comes to the Rails spec directory structure. This file teaches Rails.vim about our unique structure so you can still quick-switch between classes and their specs. You probably won't ever need to edit or open this.

### Highlights

It's in your best interest to skim/read the .vimrc and the various plugins' readmes, because there's lots of stuff in there and it's well documented, but here's a few highlights to get you started:

`jk` works as escape; you'll find it challenging to type "jklolz" (a common git commit message) in insert mode but otherwise you'll be fine. Move between splits with `Ctrl h/j/k/l`. The Leader Key has been remapped to spacebar. Double-tapping `<Space>` will toggle between last two open files. In insert mode, hitting `<Tab>` will autocomplete variable names. `Ctrl n` toggles Nerd Tree. `Ctrl p` rules the wasteland.

Plugins of note:

[Nerd Tree](https://github.com/scrooloose/nerdtree) Pops out a filesystem tree on the left. I don't use it much but when I do I'm glad it's there. Toggle this open/closed with `Ctrl n`.

[Ctrl-P](http://github.com/ctrlpvim/ctrlp.vim) Fuzzy-match file finder. I use this most of the time that I open files. Enact it with `Ctrl p` as the name suggests.

[Rails.vim](https://github.com/tpope/vim-rails) Quick navigation around Rails projects. I use `:A` and `:AV` quite a bit. Even though West Arete uses a nonstandard spec directory structure, I've patched it so things mostly work.

[Vroom](https://github.com/skalnik/vim-vroom) Run your rspec/cucumber tests from vim. `<Space> r` runs the entire current spec/feature file. `<Space> R` runs the current _line_ of the current spec/feature file. `<Space> l` runs the last test again, regardless of what file you're currently editing. Even more fun if you're running in tmux. I've also configured vroom use spring if it detects a `./bin` directory, which can occasionally get you into trouble if `./bin` exists but `./bin/rspec` doesn't. If this happens to you just search .vimrc for 'binstub' and you can comment out the line while working in that project, or generate an rspec binstub.

[Fugitive](https://github.com/tpope/vim-fugitive) Outstanding git interface for vim. It can do some truly amazing stuff, like stage only specific lines in a file to commit, but still really handy for just day-to-day commits and stuff too.

[CTags](http://github.com/vim-scripts/ctags.vim) Indexes all the classes and methods in your code. Allows you to quickly jump to definitions. As of right now you must manually index your stuff by hitting `<Space> ct`. Once you do that, place your cursor on a class or method and hit `Ctrl ]` to jump to its definition. I'm open to the idea of having ctags indexed automatically if everyone else is into it too. Here's a [good intro](http://andrew.stwrt.ca/posts/vim-ctags) to learn more. 

[tComment](http://github.com/vim-scripts/tComment) Quickly un/comment lines. Remember what I said about `.vimrc.themes` right?

[Syntastic](https://github.com/scrooloose/syntastic) Checks your syntax and tells you that your code is broken. Has a pretty pony in its readme.

## Tmux

Tmux is like the next generation of screen. It lets you have multiple split-panes and tabs open in your terminal and quickly navigate between them. When I'm working I typically have one tmux split with vim, another for running rspec, and finally a rails console. Tmux also rocks for pair programming with very low latency.

### Install the things
1. `brew install tmux`
2. `brew install reattach-to-user-namespace` Copy/Paste to and from the system clipboard with tmux can get weird. This fixes it.
3. `git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm` [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm) is like Bundler for tmux plugins. Still in its infancy but I like two of the plugins, so go for it.
4. Move `.tmux.conf` into place in your home directory
5. Start tmux by typing `tmux`
6. Install plugins by hitting `Ctrl a [release, then hit] I`
7. To quit tmux, just type `exit` like a bunch of times

### Configuration
Unlike vim it's not complicated. Just `.tmux.conf`

### Highlights

This config file is also well documented, but here's really all you need to know to get started.

The biggie: I remapped tmux's prefix to `Ctrl a`. Many people do, because it's the same as screen's prefix, and it's really easy to type, especially if you've remapped your Caps Lock key to Ctrl which I have. Whenever you see `prefix` below, that means to hit `Ctrl a`, then release, and hit the next key in the command.

Move between split-panes with `Ctrl h/j/k/l` just like vim; you can seamlessly navigate between vim splits and tmux panes. _(Coincidence??)_ Create new split panes with `prefix -` and `prefix |`; that's hyphen and pipe, aka horizontal and vertical lines which make horizontal and vertical splits. Cute huh? Resize splits with `prefix <Alt><arrow-key>`; sounds weird, makes sense when you do it. `prefix c` creates a new tab, you'll see it appear on the bottom of the screen. `prefix [1-9]` selects the tab of the corresponding number; I rarely have more than 2 tabs open, usually just one. `prefix ,` lets you rename tabs, which is helpful. `prefix z` will zoom the currently-focussed split full screen; I use this one tons.

Thanks to the [vimux](https://github.com/yunake/vimux) plugin, when running vim inside tmux, hitting `<Space> r` and its associates in vim will run the spec in a tmux splitpane, so you can see both the tests and your code at the same time. It will automatically create a split for you if none exists. If the test explodes, I will often navigate down to the split, then `prefix z` to zoom in full screen to read the stacktrace, then `prefix z` again to zoom back out to fix the problem in vim.

[Tmux Sensible](https://github.com/tmux-plugins/tmux-sensible) provides a bunch of boilerplate config, like utf-8 support, colors, bunch of other uninteresting stuff.

[Tmux Pain Control](https://github.com/tmux-plugins/tmux-pain-control) Adds those handy `prefix -` and `prefix |` bindings, and a few others.