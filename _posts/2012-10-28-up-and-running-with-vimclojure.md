---
layout: post
title: "Up and running with VimClojure"
category: clojure
tags: [vim clojure]
---
{% include JB/setup %}

This tutorial assumes a sane vim installation and the usage of
[pathogen](https://github.com/tpope/vim-pathogen) and
[homebrew](https://github.com/mxcl/homebrew).

1. Clone VimClojure into your vimbundles directory (which you should have for pathogen)

        git clone git://github.com/vim-scripts/VimClojure.git /path/to/your/vimbundles

2. Install the vimclojure-nailgun client

        brew install \
          https://raw.github.com/gist/3970910/072624c7fabb4ae5059aba70a1136d6ac869ba9b/vimclojure-nailgun-client.rb

3. Add the following to your .vimrc

        " VimClojure
        let g:vimclojure#HighlightBuiltins = 1
        let g:vimclojure#ParenRainbow = 1
        let g:vimclojure#WantNailgun = 1

4. Regenerate and _read_ the help tags!

        :helptags /path/to/your/vimbundles/VimClojure/doc

5. ... or if you're feeling lazy, feel free to peruse my [VimClojure Cheat Sheet](http://regretful.ly/clojure/2012/10/28/my-vimclojure-cheatsheet)
6. Enjoy! Emacs users needn't have all the fun, y'kno.
