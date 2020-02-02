---
layout: post
title:  "Add Comments/Notes to a GameObject in Unity"
date:   2019-10-19 16:35 +0700
tags: unity gamedev
---
In order to add a note to a `gameObject` in Hierarchies window.

- Create a script called "ThisIsComment". Remove everything from the script and copy the following code to it:

```
using UnityEngine;
/// <summary>
/// Attach this script to any gameObject for which you want to put a note.
/// </summary>
public class ThisIsComment : MonoBehaviour
{
    [TextArea]
    public string Notes = "Comment here.";  // Do not place your note/comment here.
}                                           // Enter your note in the Unity Editor.
```

- Attach this script to all of the `gameObject`s to which you want to add note (you can drag this script to the `gameObject`s or to use "**Add Component**" button in the corresponding Inspector window)

> **Note**: Do not change the content of the script. To add your note, go to the Unity Editor and write your note there (not in the script!).

Obviously, each `gameObject` can have a different note with this method.

- **(Optional)**: To make your note stand out from the other components in the Inspector window, move the "ThisIsComment" script up. To do so, click on the `script` name and drag it below the `Transform` component.

> **Note**: After moving the component up, Unity might warn you that "This action will lose the prefab connection. Are you sure you want to continue?". Don't worry. Select "**Continue**" and then click on the "**Apply**" button on the top-right of the Inspector in order to apply this change to it's prefab.

Source: [How to Add Comments/Notes to a GameObject in Unity3D](https://www.codeproject.com/Tips/1208852/How-to-Add-Comments-Notes-to-a-GameObject-in-Unity)
