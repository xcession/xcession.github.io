---
layout: article
title:  "Unity: Fade Between Scenes in Unity"
date:   2019-10-27 16:26:57 +0700
tags: unity gamedev transition
---

## Fade Between Scenes in Unity

- Add all scenes to Build Settings (just in case).
- In the **Hierarchy** window, create **UI > Image**. This will create a **Canvas > Image** and **EventSystem**.
    - The **EventSystem** can be delete if not using any UI input.
- Create an **Empty** game object then rename it to something like `FadeTransition`.
- Select **Canvas** and drag it into that **Empty** game object (in this case `FadeTransition`).
- Change the **Sort Order** of the **Canvas** to something very high, like `999`.
- Select **Image**, hold `Alt` and click the pinning option in the inspector to **Stretch to fill screen**.
- Change the color of the **Image** to black.
- (optional) Rename the **Image** to somthing like `BlackFade`.
- Select **Empty** (`FadeTransition`) and open **Animation** window (`CMD+6` / `Ctrl+6`).
- Click **Create** and save the first animation as `Fade_In.anim`. This will also create an **Animator Controller** named `FadeTransition`.
- Select the **Image** (`BlackFade`) and click the **Record** button in the animation window.
- Move play head forward **1 second** then click **Color** in the inspector and change **Alpha** value to `0`. This will create some keyframes in the timeline.
- At **1 second** uncheck the **Image (Script)** in the inspector to disable **Image** after 1 second.
- Click **Record** button in **Animation** window to finish.
- Click on the animation name in **Animation** window (`Fade_In`) then select **Create New Clip...** to create another animation.
- Save this second animation as `Fade_Out.anim`.
- Click **Record** in the **Animation** window.
- At **0 second** (frame 0) change the **Alpha** value to `0`.
- Make sure the **Image** (`BlackFade`) is enable at the begining of the animation by clicking the checkbox **Image (script)** in the inspector twice to create a keyframe.
- Move forward **1 second** and change the **Alpha** value to `1`.
- Click **Record** button in **Animation** window to finish.
- Select **Fade_In.anim** in **Assets** window and uncheck **Loop Time** in the inspector.
- Do the same with **Fade_Out.anim**.
- Double click the **Animator Controller** (`FadeTransition`) to open **Animator** window.
- In **Animator** window go to **Parameters** tab and click the **+** to create new **Trigger** and name it to `FadeOut`.
- Right click on the **Fade_In** animation in **Animator** window and select **Make Transition** then click on the **Fade_Out** animation to make a transition between the two.
- Click on the **Transition** between **Fade_In** and **Fade_Out** animation then add **Condition** in the inspector, select **Fade_Out** parameter as condition.
- Also in the inspector, disable **Has Exit Time** and expand **Settings** to disable **Fixed Duration** and change **Transition Duration (s)** to `0`.
- Back to **Hierarchy** window, select **Empty** (`FadeTransition`) then click **Add Component** in the inspector create a new script called `FadeTransition` and open it in Visual Studio then use following code:
```
using UnityEngine;
using UnityEngine.SceneManagement;

public class FadeTransition : MonoBehaviour
{
    public Animator animator;
    [Tooltip("Name of scene to load (case-sensitive)")]
    public string sceneToLoad;

    public void FadeToScene()
    {
        animator.SetTrigger("FadeOut");
    }

    public void OnFadeComplete()
    {
        SceneManager.LoadScene(sceneToLoad);
    }
} // class
```
- To use this simply drag the **Animator Controller** to the **Animator** box in the inspector and enter name of the scene to load.
- Call the `FadeToScene()` methode to start transition.

Source: [How to Fade Between Scenes in Unity](https://www.youtube.com/watch?v=Oadq-lrOazg)
