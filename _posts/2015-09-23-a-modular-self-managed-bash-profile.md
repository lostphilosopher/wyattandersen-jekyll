---
layout: blog
comments: true
title:  "A Modular, Self Managed bash_profile"
date:   2015-09-23
categories: programming, tooling
---

# A Modular, Self Managed .bash_profile

I’ve been an alias addict since I learned how to make them. There’s something to be said for the muscle memory to be gained by typing out `heroku run rails console --app APP` and `git pull origin master`, but doing so tends to drive me nuts. If `rake` was one more character I’d alias it. While the utility of aliases might be debatable bash scripts or methods are undeniably useful and often underutilized. Imagine you have a branch you’ve been working on, committing to, and pushing. You’re happy with it now and would like to rebase it. Having a single method to perform the incantations can be really helpful:

    rebase () {
      git checkout master   
      git pull origin master  
      git checkout $1  
      git pull --rebase origin master  
      git rebase -i `git merge-base $1 master`  
    }

The point being, **.bash_profile is a useful tool.**

For years I’ve had a git repo for my dot files (.bash_profile, .vimrc). This let me use the tools I’ve gotten comfortable with from any machine I’m on, AWS, Linode, my work issued Mac, my personal Mac, etc. My git repo had a .bash_profile for each of them. I had multiple .bash_profiles because I had a few things that were specific to a single machine that I didn’t want cluttering up the file for other machines, and a few commands that provided the same utility, but required different semantics depending on what box I was running them on. However, all of the files had my git preferences, and anytime I added a new alias or method pertaining to git I’d have to copy that change into each .bash_profile, or I’d be annoyed when I tried to use it on a different machine and it wasn’t set up for me. DRY principle be damned.

Clearly there had to be a better way.

## Modular

If there’s anything I love more than aliases, it’s modularity. (And also whiskey.)

I read some blog posts about modularizing your .bash_profile, but for some reason they made everything seem _really_ complicated. Since this was never a "must have” I kept putting it off, but recently I finally got around to doing it. Here’s how.

1. In the bash folder of my dot_files repo (which I keep in the home directory of any machine using it) I created a single bash_profile, and a lib/ directory.
   
2. In my bash_profile I put the few things that I’m sure to use universally. Bash history formatting for example:
    
    # Bash history  
    export HISTTIMEFORMAT="%h/%d - %H:%M:%S  "  
    export HISTCONTROL=ignoredups:ignorespace  
    shopt -s histappend  
    export HISTSIZE=10000  
    export HISTFILESIZE=5000  
    shopt -s checkwinsize

1. Under lib/ I created file for each of the domains that I covered in my various bash_profiles: git, heroku, ruby, vagrant, grep, etc.
   
2. In my bash/ directory, along with bash_profile I created a .manifest file and listed it in .gitignore.
   
3. In that manifest file I sourced all the domain modules I wanted pulled in on the machine I was working on.
   
    [ -r ~/dot_files/bash/lib/git ] && source ~/dot_files/bash/lib/git  
    [ -r ~/dot_files/bash/lib/grep ] && source ~/dot_files/bash/lib/grep  
    [ -r ~/dot_files/bash/lib/heroku ] && source ~/dot_files/bash/lib/heroku  
   
4. Finally in my bash_profile, I sourced the .manifest file.
   
    [ -r ~/dot_files/bash/.manifest ] && source ~/dot_files/bash/.manifest

With this done I could set up all my preferences with `cp ~/dot_files/bash/bash_profile ~/.bash_profile && source ~/.bash_profile`. Each machine I use now has it’s own .manifest that pulls in only what it needs.

(`cp ~/dot_files/bash/bash_profile ~/.bash_profile && source ~/.bash_profile`, geez that’s a lot of characters… You know where this is going.)

## Self Managed

I fiddle with my bash_profile configurations a lot. I also keep my dot_files on GitHub, but don’t follow any sort of elegant workflow since it’s just me working on it. And, since I do a lot of ssh’ed work on different machines I find myself setting up .bash_profiles pretty frequently. It was only a matter of time before my .bash_profile included scripts and aliases for managing… My .bash_profile.

Here’s what I have set up:

**Aliases for experimenting with / making quick changes to .bash_profile**

    alias bashedit='vim ~/dot_files/bash/bash_profile'  
    alias editbash='vim ~/dot_files/bash/bash_profile'  
    alias rebash='cp ~/dot_files/bash/bash_profile ~/.bash_profile; source ~/.bash_profile'

If I’m considering a new script for my .bash_profile I can type `bashedit` make some tweaks in vim, save the file, and type `rebash` to apply them. Pretty slick huh?

Note that I deliberately call the source file “bash_profile” and the file actually being used file “*.*bash_profile”. This reminds me that they’re different files, and I create two so I can follow standard conventions around keeping your .bash_profile in your home directory and still manage the contents with git.

**Easy committing**

    commitdots () {
      red='\x1B[0;31m'; # red  
      green='\x1B[0;32m'; # red  
      NC='\x1B[0m'; # No Color  
      cd ~/dot_files;  
      if git diff-index --quiet HEAD --; then  
        echo -e "${red}No local changes to dot_files to commit${NC}"  
      else  
        git pull origin master;  
        git add -A;  
        git commit -m 'Changes to dot_files committed via script';  
        git push origin master;  
        echo -e "${green}Local changes to dot_files commited${NC}";  
      fi  
      cd -;  
    }  

Since I’m not following a standard git flow with fancy branches and pull requests I might as well get the maximum benefit from my laziness!

If I make changes to any of my dot_files, bash, vim, or whatever else ends up in there, typing `commitdots` sends those changes to GitHub so I can get at them from anywhere.

**UPDATE 11.08.15:** I recently came across a situation where I needed to use an API key in one of my scripts. I didn't want to put the key out on GitHub, and felt putting it in the .manifest file would violate separation of concerns. I ended up creating a git ignored .private file underneath dot_files/bash/ to hold that sort of information. This has been working well so far.

## What’s next?

There’s a few more scripts and global variables to be written to further simplify, and cut down on duplication, and I haven’t fully ported all the contents from my various .bash_profiles to this new modular system.

In the mean time, this system has been working great for me. You’re welcome to peruse the full repo, or try it out for yourself - the code’s available here: [https://github.com/lostphilosopher/dot_files](https://github.com/lostphilosopher/dot_files). Along with instructions on how to set it up.

Happy bashing.
