---
layout: post
title: "My VimClojure CheatSheet"
category: clojure
tags: [clojure, vim, quicktips]
---
{% include JB/setup %}

	## Evaluation
	require current ns with :reload-all in Clojure Server
	    <LocalLeader>rF
	eval toplevel sexp containing cursor in Clojure Server
	    <LocalLeader>et
	eval current file in Clojure Server
	    <LocalLeader>ef
	eval current line in Clojure Server
	    <LocalLeader>el
	close Clojure Server buffer
	    <LocalLeader>p
	## Introspection
	lookup documentation for word under cursor
	    <LocalLeader>lw
	lookup (local) source for word under cursor
	    <LocalLeader>sw
	lookup (library) source for word under cursor
	    <LocalLeader>gw
	## Repl
	start a new repl in a fresh buffer
	    <LocalLeader>sr
	start a new repl in the current namespace in a fresh buffer
	    <LocalLeader>sR
	start a new repl while outside of a Clojure buffer
	    :ClojureRepl
	close repl
	    <LocalLeader>close
