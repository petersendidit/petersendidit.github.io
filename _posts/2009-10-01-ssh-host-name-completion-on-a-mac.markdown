---
layout: post
title: SSH host name completion on a Mac
categories:
- Posts
tags:
- mac
- osx
- ssh
- tab completion
comments: true
meta:
  dsq_thread_id: '138 http://blog.petersendidit.com/?p=138'
---
The list of servers I have to ssh in to is continually growing many of them I need to have an ssh tunnel to get to so I fully use the ~/.ssh/config file to help me out.  Now that my .ssh/config file has grown I am starting to forget what name of that one server was.  On some unix boxes [bash_completion](http://www.caliban.org/bash/) is installed which allows you to type: ssh se[tab] and get: ssh servernamethatisreallylog.com. bash_completion is not installed on the Mac by default.  You can install it with [macports](http://www.macports.org/) but I have yet to run in to a real need to install macports yet so I started searching for any other ways to get this working on my Mac.

What I found was a comment on a [MacOSXHints hint](http://www.macosxhints.com/article.php?story=20080317085050719).
All you need to do is throw this in your ~/.bash_profile file.

```bash
_complete_ssh_hosts ()
{
        COMPREPLY=()
        cur="${COMP_WORDS[COMP_CWORD]}"
        comp_ssh_hosts=`cat ~/.ssh/known_hosts | \
                        cut -f 1 -d ' ' | \
                        sed -e s/,.*//g | \
                        grep -v ^# | \
                        uniq | \
                        grep -v "\[" ;
                if [ -f ~/.ssh/config ]; then
                        cat ~/.ssh/config | \
                                grep "^Host " | \
                                awk '{print $2}'
                fi
                `
        COMPREPLY=( $(compgen -W "${comp_ssh_hosts}" -- $cur))
        return 0
}
complete -F _complete_ssh_hosts ssh
```

This will read in your .ssh/known_hosts file and your .ssh/config file and create a list of host names that you can now tab complete with the ssh command.  Comes in very handy.
