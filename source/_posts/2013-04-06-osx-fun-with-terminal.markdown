---
layout: post
title: "[OSX] Fun with Terminal"
date: 2013-04-06 00:08
comments: false
categories: [osx, hack]
---

![Customize OSX Terminal](http://f.cl.ly/items/1c3C0z0t1g0e2K1y2X0M/Screen%20Shot%202013-04-06%20at%2012.00.21%20AM.png)

Some fun things you can do to pimp your OSX Terminal: (I'm using Mountain Lion fyi)

<!-- more -->

## Customize Terminal Prompt with Emoji

Add this line to ~/.bash_profile (Note: You should see the yellow emoji with shade below)

	export PS1='\[\e[0;37m\]⌘ \[\e[1;36m\]\W\[\e[1;33m\] <put_emoji_here>  \[\e[0m\]'
	
Replace `<put_emoji_here>` with any emoji you want. Alt+Command+T to open emoji window.
Above line not only adds emoji, but also remove name and hostname, and only show current directory name (not full path). Read [here](http://osxdaily.com/2006/12/11/how-to-customize-your-terminal-prompt/) for more information.



## Set Current Directory as Terminal's Tab Title

By default, the tab's title is 'bash' and it doesn't change. The window title does change. To make tab's title changes to current directory automatically, add this line to ~/.bash_profile

	PROMPT_COMMAND='update_terminal_cwd; echo -ne "\033]0; ${PWD##*/}\007"'
 
## Show Git Branch on Terminal Prompt

For developers, add this function to ~/.bash_profile

	parse_git_branch() {
	    git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\ <emoji> \ \1/'
	}

then update the PS1

	export PS1='\[\e[0;37m\]⌘ \[\e[1;36m\]\W\[\e[1;33m\]$(parse_git_branch) <emoji>  \[\e[0m\]'
	
## Show Random Quote on Terminal New Session

Install fortune

	sudo port install fortune
	
Add this line to ~/.bash_profile

	echo -e "\n\x1B[00;33m$(fortune)\x1B[00m\n"

Remember to restart the Terminal everytime you make changes. If you want to change some colors, check [here](https://wiki.archlinux.org/index.php/Color_Bash_Prompt#List_of_colors_for_prompt_and_Bash).

If you like this post, you might want to take a look at [NSMeme Facebook Page](https://www.facebook.com/nsmemepage) I made to share some interesting stuff in iOS development.