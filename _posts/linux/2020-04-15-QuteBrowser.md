---
title:  "Qutebrowser - Minimal and Vimmed!"
author: spandan
categories: [ Linux, minimalism ]
tags: [cover, intro]
description: "Qutebrowser : just the way I like it"
featured: false
hidden: false
layout: post
image: assets/images/linux/qute.png
comments: false
---
Being someone who strives to have a steamlined, minimal setup and someone who doesn't like to go and take his/her hands off the keyboard and 
place it on the mouse (too much work XD), I have been pretty bugged that I did not have a minimal browser to be used in my daily
workflow ie. not just for bragging rights. I had surf by suckless but somehow pags with too much graphics were not as responsive as 
Firefox (Maybe I am yet to set it up right).

Using Vim in my everyday workflow has further spoiled me. I love Vim keybindings. I love them so much that even if and when I set up Emacs,
(I love org-mode), the first thing I set up is the EVIL key bindings. First thing that fascinated me about qutebrowser : These beautiful
keybindings. I have also heard of VimB but I am yet to find a reason to move to it. So, make sure you are in INSERT mode while typing.
Here is the official keybinding cheetsheet from their <a href="https://github.com/qutebrowser/qutebrowser">Github page</a>.

![QuteCheetSheet](https://i.imgur.com/TnSFUCG.png)

As you start using these keybindings pop-ups with completion suggestions come up.

![Pop UP](https://i.imgur.com/a56sSBC.png)

There is an elaborate configuration process which is mentioned in detail in their doc. However , here is a quick setup to get you started.
Once qutebrowser is installed on your Linux system, go to your config folder 
```bash
$HOME/.config/qutebrowser
```
If that folder does not exist, create it. In that folder we shall use a slightly modified **autoconfig.yml** and a config.py to set you up with 
my working configuration.

The autoconfig.yml file is as follows:

```yml
config_version: 2
settings:
  aliases:
    global:
      q: close
      qa: quit
      w: session-save
      wq: quit --save
      wqa: quit --save
  bindings.commands:
    global:
      normal:
        ',v': spawn mpv -vo=gpu {url}
        u: null

```
Or open up your browser and type 
```vimscript
:config-set
```
The config.py file is as follows

```python
def bind_header(url_wild_card, alt_header='Mozilla/5.0 ({os_info}) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.122 Safari/537.36'):
    config.set('content.headers.user_agent', alt_header, url_wild_card)


config.load_autoconfig()

bind_header('https://web.whatsapp.com')
bind_header('https://accounts.google.com/*')
bind_header('https://*.slack.com/*')
bind_header('https://docs.google.com/*')
bind_header('https://www.netflix.com/*')
bind_header('https://www.primevideo.com/*')

# Type: Bool
config.set('content.images', True, 'chrome-devtools://*')

# Load images automatically in web pages.
# Type: Bool
config.set('content.images', True, 'devtools://*')

# Enable JavaScript.
# Type: Bool
config.set('content.javascript.enabled', True, 'chrome-devtools://*')

# Enable JavaScript.
# Type: Bool
config.set('content.javascript.enabled', True, 'devtools://*')

# Enable JavaScript.
# Type: Bool
config.set('content.javascript.enabled', True, 'chrome://*/*')

# Enable JavaScript.
# Type: Bool
config.set('content.javascript.enabled', True, 'qute://*/*')

config.bind(',v', 'spawn mpv -vo=gpu {url}')

```
I omitted out my colorscheme as the code would be too long to discuss. But an autoamated colorsheme may be setup using the 
qutebrowser base16 configurations as available <a href="https://github.com/theova/base16-qutebrowser">this repository.</a>

Let's end this by looking at two cool features:

1.  I want to play an youtube video while doing something else. So, I can spawn it onto mpv to play on my gpu using the keybinding
**,v** and this does consume lesser Ram and power than playing it on the browser.

![MPV-SPAWN](https://i.imgur.com/nfrU5KZ.gifv)

2. Suppose I want to download the current page as an html file. **:download** or **gd**

![Imgur](https://i.imgur.com/hCvbQaL.gifv)
