---
layout: post
title: "CREATING THIS BLOG SHOULD HAVE NOT HAVE BEEN THIS HARD"
date: 2026-08-24 21:06:00 -0700
categories: misc
---

*DISCLAIMER: this was written in haste and is horribly formatted. You should really only read this if you are trying to set up the github pages blog on nixOS or cachyOS, or are installing cachyOS for the first time. Thanks!*

# Wow.

Who knew that making a blog could be this frustrating. It didn't need to be, but I really wanted to make sure I knew and remembered everything that I was doing as I went along.

Let me start from the beginning.

## Making the first version of this blog with NixOS

When I began following the simple tutorial to make this blog on the github docs, I was using what I had heard was one of the coolest Linux operating systems out there right now: NixOS. Now, I have been falling down quite the rabbithole recently with Linux, which began around march when my friend put me on fedora. I quickly discovered hyprland and switched to arch, then put NixOS on my laptop (this is over the course of around 5 months, but I won't bore you with that). I thought it was niche and cool, and that it would be even more intuitive than arch due to its reproducible nature. I could not be more wrong.

I won't drone about my experiences with it before creating this blog (after all, that is what this post is about), so let's jump in to the blog making.

The first parts were easy. Add what I needed to nixpkgs (ruby and whatnot), then make blog. However, while it seemed quite intuitive, I didn't realize that I was missing essential C build tools needed for Ruby and other parts of the blog system to run.

While I should have known what to do, the error message saying "you need build tools" and nothing else made me first think that it was a problem with the Ruby build tools. I had always taken C build tools (clib and whatnot) for granted on all my other distros.

After a lot of troubleshooting, I turned to my last resort - claude. It told me that I needed to create a nix shell with the dependencies for the project, or else it wouldn't work. So I created a shell, added the dependencies, and it worked!

But why wouldn't it work if I just added everything to my configuration.nix (the file used to declare all the packages on your system)?

Answer? Claude was wrong. Glad that I always double check AI and try to understand things instead of blindly copying and pasting slop. Although, I did learn the importance of nix shells (only declaring niche packages in shells where they're needed instead of flooding your configuration.nix with packages you'll only use for one project), and ended up running the blog from a shell, which was cool!

# The Switch from NixOS to CachyOS

So everything was great! Until the next day I was working with jupyter notebooks and was fighting with NixOS again. SO many applications rely on paths like /usr/bin that NixOS simply doesn't agree with due to its strict "isolate packages for the things they're meant to create" philosophy.
- Now, I'm positive that I could have fixed these issues if I wanted to put in the time, and if you're a Nix enthusiast reading this blog, you're probably turning your nose up at me in disgust. However, I don't care enough to put in this much time to debugging problems that applications have with my OS. I have a life, and (more importantly) other things that I need to spend more time on coding.

So yesterday I switched to CachyOS. Long story short, the KDE installer consistently kept freezing before I could do anything due to my NVIDIA GPU, I worked around the issue by using the NixOS LTS kernel for the installer. Gotta love NVIDIA for keeping so much stuff closed source.

I will admit, and I really didn't want to because I thought my friend was bugging when he told me this, but Cachy is genuinely faster than arch. It's nuts how much faster my firefox is from NixOS to Cachy, and I swear it's not placebo because I really didn't want to believe it. However, it seems slower today, I don't know why. Okay, glazing over.

Things about Cachy:
- (imo) their hyprland config is dogshit. I had to spend an hour just returning it to the goated defaults. Cachy's keybinds are 100% centered around the windows key, and I personally believe that caps lock is the better option, mainly because it allows your hands to stay on the home row. Shoutout my vim enthusiasts.

After the struggle, I started to create this blog.

# Creating THIS Blog (that you're reading)

Since I had done it before and I'm familiar with pacman, it was easier to set this up. However, I ran into my own issues that others online had encountered, but every solution was different. Here is a quick list of my struggles and solutions:

## First issue

PATH was set wrong for gems. I followed the [generic advice on the jekyll page for setting up jekyll and the directories for ruby gems](https://jekyllrb.com/docs/installation/ubuntu/) (yes, i know it says ubuntu but this is what they direct all distros to do after installing the prereqs via their respective package managers) and ended up getting PATH confusion from CachyOS (quick reminder that Cachy is basically just arch with some hardware and software optimizations, but everything else is the same). Here's how i handled it.
- I turned to claude (you probably already know how that went), which helped me discover that a specific ruby gems path is baked in to the ruby installed by `pacman`, and I could write a gemrc file to override it. While that probably would have worked, I then realized that I shoud just:
- RTFM. For those unaware it means "READ THE FUCKING MANUAL". I opened up the arch wiki and read their ruby page, and within minutes was able to resolve my issue by adding the correct PATH to my ~/.zprofile (use .profile for bash) and restarting my computer. Amazing! Quick reminder that if you don't restart your computer though, you have to source your .zprofile every single time you want to use whatever you put in it (in this case, my PATH for gems).

## Second issue

I really wanted to use the `hacker` theme (i hope you know why), but troubleshooted for an hour and realized that if I wanted to build a blog around it, I have to write more code for it, which I am not particularly interested in doing right now as I am trying to focus on machine learning, not blogging (even though it may seem like it to you after reading this).
- TLDR if you just want a working blog out the box just stick with the default `minima` theme generated by jekyll when you follow the tutorial.

Alright, that's pretty much it. Thanks for reading! I hope this might help, if you have any questions at all, shoot me an email at the one linked in the blog. Have a good one!

