---
layout: post
title:  "Using iTerm with Learn.co"
date:   2016-10-14 06:44:15 +0000
---


I use iTerm instead of the Mac Terminal app as part of my Learn  development workflow, [here](http://iterm2.com/features.html) are some of the iTerm offers.

### Learn open iTerm

When starting a new lab on you  can click the `Learn` button  and  the lab is then forked and cloned to the local environment and the Terminal.app is launched at the labs directory. please note, if you're using the Learn IDE, the lab opens in the IDE's terminal instead.

I wanted to open the lab in the iTerm app instead of the native Terminal.app, after asking some of the Learn devs if there was a way to switch Terminal app in the learn-config file (the default editor and learn directory can be changed at `cd ~/.learn-config` and open in editor) I was told that there currently wasn't a way to do so , and since most students use the Terminal app, and said app is pretty awesome, adding this feature, understatedly,  wasn't a top  priority, so I jest left it at that and continued using the Terminal app.

Then, one day I put on my procrastinator hat and set out on a mission to try to create a workflow to use iTerm with learn and here is how I did it (sort of!).

## Creating the Shell Script

A bit of googling how to open an app in terminal turned up [this](http://osxdaily.com/2007/02/01/how-to-launch-gui-applications-from-the-terminal/) article, so I tried `open -a iterm` in the terminal app and iTerm was launched but not in the same directory, it simply opened the iTerm app, after a while of tinkering and trying to figure out how can I save the  `pwd`  return to a variable and send that to iTerm I realized that `open` is just a bash command to open something, and in bash `.` stands for current directory so I tried  `open . -a iterm` and voila... it worked!

Next I created a bash [alias](http://www.techradar.com/how-to/computing/apple/terminal-101-creating-aliases-for-commands-1305638), like this; `alias itm="open . -a iterm` and lived happily ever after.... NOT, I now ended up with both Terminal and iTerm open and found it tedious to manually close the Terminal app every time I ran this alias, so back to google I went, oh google, my one true love....

### Quitting...

My first approach was to use the `exit` command, but all that did was end the process in the terminal, but it  didn't  actually close the terminal app, I needed a script or command to just quite the app  completely, google pointed me to [this](http://osxdaily.com/2014/09/05/gracefully-quit-application-command-line/) article, and this is what I ended up with `osascript -e 'quit app "Terminal"'` the `-e` is for Enter one line of code, and not a file containing a script.


### My First bash function

Spending some time in the bash_profile I noticed the Flatiron profile comes with a *desktop* function, that enables you to enter `desktop` in the terminal and it changes the directory to the desktop, so I figured if I create a function and combine the `itm` alias with the new quitting script it  would be pretty neat, here it is...


```shell
# open iTerm in currant directory and Quit Terminal

function itm {
  open . -a iterm  && `osascript -e 'quit app "Terminal"'`  
}

```


If you know of a better way to accomplish this, or have any questions please comment below.
