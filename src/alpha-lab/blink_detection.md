---
title: "Detecting eye blinks using Pupil Lab’s blink detection pipeline"
description: Perform posthoc and real-time blink detection
permalink: /alpha-lab/blink-detection/
tags: [Pupil Invisible, Neon, Realtime Python API]
---

# Detecting eye blinks using Pupil Lab's blink detection pipeline

<font size = 2>Products used: [Neon](https://pupil-labs.com/products/neon/), [Pupil Invisible](https://pupil-labs.com/products/invisible/), [Realtime Python API](https://pupil-labs-realtime-api.readthedocs.io/en/stable/)</font>


![GIF](../media/alpha-lab/eye_blinks_anim.gif)

# <font size=4>The importance of eye blinks</font>

The accurate detection of eye blinks serves a vital role in numerous eye tracking applications. Its importance is twofold: firstly, it helps identifying time periods affected by blink-related artifacts, and secondly, isolating key physiological, cognitive, and clinical parameters, such as blink rate and blink duration. This guide shows you how to apply Pupil Labs' blink detection algorithm to recordings made with Neon or Pupil Invisible.

# <font size=4>Running eye blink detection locally</font>

Eye blinks are automatically detected once your recording is uploaded to Pupil Cloud. This guide shows how to apply Pupil Labs' blink detection algorithm <i>offline</i> (i.e., without using Pupil Cloud) to recordings made with Pupil Invisible or Neon. This allows you to build novel applications or simply satisfy your curiosity and develop a deeper understanding of the underlying algorithms. That's why we decided to put together this guide that shows you how to achieve this.

::: tip
If your are interested in learning more about the technical specifics of the underlying blink deteciton pipeline, we also invite you to have a look at our [**white paper**](https://docs.google.com/document/d/1JLBhC7fmBr6BR59IT3cWgYyqiaM8HLpFxv5KImrN-qE/export?format=pdf).
:::

# <font size=5>Getting started</font>

To get started, we invite you to check out the accompanying [**GitHub repository**](https://github.com/pupil-labs/real-time-blink-detection), where you can find a detailed instruction on how to install all required packages as well as a [**Jupyter notebook**](https://github.com/pupil-labs/real-time-blink-detection/blob/main/blink_detection.ipynb) that contains all the code needed and instructions on how to run everything.

# <font size=5>Results</font>

# <font size=4><strong>Part 1</strong>: Posthoc blink detection</font>

After you have run the first part of the notebook, you will have an output from which we can derive a number of statistics, such as the total number of detected blinks, the estimated blink rate (in Hz), and the average blink duration (in seconds). Additionally, you will get the eyelid closing and re-opening durations. All of these statistics can provide meaninful insights into the state of your participants.

![Blink statistics](../media/alpha-lab/eye_blinks_statistics.png)

<font size=2>**Figure 1.** Blink statistics extracted from the provided example Neon recording.</font>

You will additionally get a plot with a visual representation of the detected blinks, providing further insights into the temporal distribution of the detected blinks:

![Visual blink representation](../media/alpha-lab/eye_blinks_timeline.png)
<font size=2>**Figure 2.** Visual representation of the detected blinks in the example Neon recording. Green shaded areas depict detected blink events.</font>

When examining blink durations and the eyelid closing and re-opening times, you may notice that the total blink duration doesn't consistently equate to the sum of the durations of the closing and re-opening phases. This discrepancy arises because there are some frames during the period between closing and reopening of the eyelids where there is negligible movement, and thus, they are not classified as part of either the opening or the closing phase. However, blink duration is calculated from the start time of the eyelid closing to the last frame identified as part of the re-opening sequence and will, thus, almost always be marginally longer than the sum of the individual events.<br>

# <font size=4><strong>Part 2</strong>: Real-time blink detection</font>

Detecting eye blinks in real-time can be beneficial for tracking blink rate over time (potentially serving as a biomarker of [mental fatigue](https://pubmed.ncbi.nlm.nih.gov/8070793/)) or even for leveraging specific blink patterns to control external devices. This part of the guide will show you how to utilize Pupil Lab's Realtime Python API to do this.

## <font size=5>2.1. Real-time blink rate estimation:</font>

After you run part 2.1. of the guide, you will be able to estimate blink rate in quasi real-time. From this, you will obtain a graph, as shown below, that is updated with every blink and shows the current estimation of blink rate.

<img src="https://hackmd.io/_uploads/B1zIstcb6.png" alt="Blink statistics" width="550"></img>

<font size=2>**Figure 3.** Realtime blink rate estimation. Shown is the blink rate estimated over the last 30 s (solid line) as well as the average blink rate for the entire recording (dashed line). </b></font>

## <font size=5>2.2. Toggle recordings remotely through eye blinks</font>
In the last part of this guide, you will learn how to control a Neon or Pupil Invisible device through a rapid sequence of three eye blinks. Upon detection of said sequence, the companion device will initiate a new recording or stop an ongoing one, as illustrated in the video below:

<iframe width="512" height=258 src="https://www.youtube.com/embed/idAHOysl37Q?&mute=1&controls=0&autoplay=1&loop=1&playlist=idAHOysl37Q&rel=0"></iframe>

# <font size=5>Conclusion</font>
In this Alpha Lab, we have shown you how you can use our blink detection pipeline offline (i.e., outside of Pupil Cloud) and how you can build simple applications with it. We're excited to see what you will build using these tools. If you need assistance in implementing or building your own application, reach out to us by email or visit our Support Page for dedicated support options.
