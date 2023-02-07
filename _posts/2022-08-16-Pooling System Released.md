---
layout: post
title: Studious Pooling System
date: 2022-08-16 21:52
category: [unity_packages]
tags: [unity,pooling]
---

Is a small very simple library, that helps Pool Objects.

Why another Object Pooling System?

I wrote this a long time ago for my projects, as there was nothing that would work the way I needed a pooling system to work. I have since modified it slightly and decided that it would be good to share it with others.

So what makes this Object Pool any different to others, well others focus more on a GameObject rather than be generic. What that means is you can instantiate a prefab by its script rather than its Game Object, then store that in the Object Pool instead of the GameObject. This helps reduce having to use GetComponents, when everything from the GameObject to Transform will be stored.

<a href="https://github.com/Studious-Games/StudiousPoolingSystem">Visit the Pooling System Repository</a>