---
title: "Pair programming with ChatGPT - an unexpected path"
date: 2023-01-24T13:00:00+01:00
lastmod: 2023-01-24T13:00:00+01:00
draft: false
author: "Nicola Massarenti"
authorLink: ""
description: "How ChatGPT showed me alternative solutions - like a Senior would do."
images: [""]

tags: ["blog", "ai", "chatgpt", "programming", "linux", "tools"]
categories: ["blog"]

lightgallery: true

share:
  enable: false
code:
  copy: true
  maxShownLines: 50
math:
  enable: true
comment:
  enable: true
---

ChatGPT is out there and everyone is talking about it. I have read tons of posts regarding how to write prompts, what prompt is going to give you **the** secret strategy for the business... yada yada yada...

My story, here, is not about prompt engineering.

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/pair-programming-chatgpt/robot-baby.png "")

It's about one unexpected outcome, about how, for the first time, I felt like I was getting help from a Senior peer: someone who understood my problem, someone located remotely (because I was chatting with him), someone that had more experience than me in Linux, someone I could learn from.

# The problem

My OS is Linux Ubuntu. My shell is [fish](https://fishshell.com/) and I love it (check out my [dotfiles](https://github.com/nicolamassarenti/dotfiles)). It allows the creation of functions (a.k.a. aliases) very easily.

My *note-taking tool* is [Obsidian](https://obsidian.md/), an open source software for building the second brain (it's also where I'm drafting this blog post).

On Ubuntu, I run the Obsidian app by running an AppImage, a format for distributing software on Linux. An AppImage file contains the software and all the dependencies you need to run the app. This means that to run the file you only type one command: `./path/to/file.AppImage`.


Well, running obsidian via AppImage implies the following steps:
* Opening a terminal - typing: `CTRL+T`
* Running the AppImage - typing: `./path/to/AppImage`
* Keeping the terminal open to keep the process up and running - the main problem, because I often do some house-cleaning and close all the pending processes and terminals

This means that I should repeat these three steps at least once a day. Every day.... This had to be automated!

# What I wanted to do

My initial goal was to create a `fish` function that allowed me to type `obsidian` and, in turn, run the app image.

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/pair-programming-chatgpt/terminal-1.png "")

This creates the following function (located in `~/.config/fish/functions/obsidian.fish`):
```shell
function obsidian --wraps=/opt/obsidian/Obsidian-1.1.9.AppImage --description 'alias obsidian=/opt/obsidian/Obsidian-1.0.3.AppImage'
  /opt/obsidian/Obsidian-1.0.3.AppImage $argv; 
end
```

However, this partially solved the my problem. I had to keep the terminal up and running. This is what the terminal was printing while Obsidian was running:

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/pair-programming-chatgpt/terminal-2.png "")

So I thought: I just have to redirect the logs to `/dev/null` and it's done! I can close or use the terminal for other stuff! Great!

At this point, I wanted a quick result since (I thought) I knew what was the path to follow. So, I decided to ask ChatGPT to solve the problem. I asked:
`write a fish function that runs a detached appImage at path "/opt/obsidian/Obsidian-1.1.9.AppImage"` 

Great! I got the solution:

```shell
function run-obsidian
    nohup /opt/obsidian/Obsidian-1.1.9.AppImage > /dev/null 2>&1 &
end
```

I modified the `.fish` file and tested the new function: obsidian was opened and the process was detached, but when I closed the terminal, obsidian was closed too!

Fair enough... With some disappointment, I wrote to ChatGPT: `the process should be alive even if I kill the terminal`. 

And here happened the unexpected! Here I was suggested a new path, something I knew could be used for such use cases but for a lack of experience I never considered. Here I learned something new, without searching for it.

# What I discovered it was possible

ChatGPT now shared an unexpected solution. It said that if I wanted to have the process running even if I logged out of the system, I had to use `systemd` service manager.

This is service file generated:
```shell
# Create a new service file
sudo nano /etc/systemd/user/obsidian.service

# Add the following content to the file
[Unit]
Description=Obsidian AppImage

[Service]
ExecStart=/opt/obsidian/Obsidian-1.0.3.AppImage
Restart=always

[Install]
WantedBy=default.target

```

And, I could use the following commands to enable and start the service:
```shell
systemctl --user enable obsidian.service
systemctl --user start obsidian.service
```

This was my reaction:

![](https://raw.githubusercontent.com/nicolamassarenti/nicolamassarenti.github.io/main/content/blog/pair-programming-chatgpt/reaction.png "")

I was stunned. This **kind of interaction** it's exactly what a person expects from a Senior colleague. I **felt enriched** from the answer. It was great.

Now, I had to automate the setup. I asked: `create a script that automates the generation of the file, the setup of systemctl, and that runs the latest version of the AppImage among those in the folder. Make it fish-compliant`

This was the output: 
```shell
#!/usr/bin/env fish

# Edit this line to specify the path to your AppImages
set APPIMAGE_PATH '/opt/obsidian'

# Edit this line to specify the service name
set SERVICE_NAME 'obsidian'

# Find the latest AppImage
set appimage (find $APPIMAGE_PATH -name "Obsidian-*.AppImage" | sort -r | head -n 1)

# Create the service file
sudo sh -c "echo '[Unit]\nDescription=Obsidian AppImage\n\n[Service]\nExecStart=$appimage\nRestart=always\n\n[Install]\nWantedBy=default.target' > /etc/systemd/user/$SERVICE_NAME.service"

# Reload the systemd configuration
systemctl --user daemon-reload

# Enable the service
systemctl --user enable $SERVICE_NAME.service

# Start the service
systemctl --user start $SERVICE_NAME.service
```

and it was done. Wow.