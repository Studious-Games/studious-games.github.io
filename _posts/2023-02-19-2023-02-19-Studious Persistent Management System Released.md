---
layout: post
title: Studious Persistent Management System Released
date: 2023-02-19 14:52
category: [unity_packages]
tags: [unity]
---

One of the most common problems when developing in Unity, is that there are times when we need to persist scripts across scenes. One of the more common ways is to use a Singleton to the do this, however, this is not always the best solution and is also frowned upon in the community. 

As they tend to get over used.

The Persistent Management System, was designed to be simple and easy to use and understand, and leverages of keep objects alive via the DontDestroyOnLoad option. Which allows for a script to then be made persistent with ease.

Like the Singleton pattern, this can still be over used, so do so with moderation.

Getting started is easy, create a script and add the attribute below, and you now have a component that will be persistent to the next scene.

```csharp
[Persistent()]
public class GameManager : MonoBehaviour
{
}
```

And that is all that is required to make it the class persist, and when you need to get access to the class, then all you need to do is something like the below.

```csharp
public Player : MonoBehaviour
{
    private void Start()
    {
        GameManager gm = PersistentLocator.Get<GameManager>();
    }
}
```

And now you can use the methods, fields and properties at your leisure.

<a href="https://github.com/Studious-Games/PersistentManagementSystem">Visit the Persistent Management System Repository</a>
