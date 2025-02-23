---
description: Powerful tool to map gaze data from the scene camera onto a reference image 
permalink: /enrichments/reference-image-mapper
---

# Reference Image Mapper

Reference Image Mapper is a powerful tool to automatically map gaze onto features/objects in the environment.

<Youtube src="IF8f1Z3ZkEo" muted="1"/>


A heatmap of gaze data mapped onto the reference image can be generated, and mapped gaze and fixation data can further be downloaded as [CSV files](/export-formats/enrichment-data/reference-image-mapper/#fixations-csv). 

## Setup

<Youtube src="ygqzQEzUIS4"/>

As described in the setup video, you will need two things in addition to your eye tracking recording(s) to produce a Reference Image Mapper enrichment:
1. A reference image
2. A scanning video of the object/feature(s) taken with Invisible/Neon’s scene camera

:::tip
**Reference Image**<br/>
Only the scanning recording needs to be taken with Invisible/Neon. The reference image can be taken with any camera. It can be also be a scanned image.
<br/>
<br/>
<b>Duration</b><br/>
The **3 min** duration limit only applies to the scanning recording, the rest of your videos can be as long as you like. <br/>But to avoid long processing times and get the best results, we recommend spliting the recordings into relevant parts where you expect the image to be mapped. <br/>
:::

In this guide, we will show you how the Reference Image Mapper can be used in a few different situations. This should help you get set up using the enrichment in your own testing environment!

Below, gaze is mapped in four very different environments: to a **magazine cover**, a **basketball backboard**, a **supermarket shelf**, and even a **whole building**!

<PhotoGrid :images="[
  require(`../media/enrichments/rim/heatmap-0.jpg`),
  require(`../media/enrichments/rim/heatmap-1.jpg`),
  require(`../media/enrichments/rim/heatmap-2.jpg`),
  require(`../media/enrichments/rim/heatmap-3.jpg`),
]"/>

Let's take a look at what the Reference Image and Scanning Recording look like to produce these heatmaps.
### 1. Magazine reading

<div class="mcontainer">
  <div class="col-mcontainer">
    <h4>Reference image</h4>
    <v-img
    class="rounded" 
    style="margin-bottom:14px;"
    max-width="100%" max-height="300px" contain 
    :src="require('../media/enrichments/rim/magazine-img.jpg')"
  ></v-img>
    First, we need a high-resolution .jpeg of the page.
  </div>
  <div class="col-mcontainer">
    <h4>Scanning video</h4>
    <Youtube src="SplYZK-ZzE8"/>
    Then, we need a scanning recording, about <i>15 s</i> long, taken on a blank background and in good lighting (natural light works well). Note that the magazine page is clear with good contrast
  </div>
</div>


### 2. Basketball

<div class="mcontainer">
  <div class="col-mcontainer">
    <h4>Reference image</h4>
    <v-img
    class="rounded" 
    style="margin-bottom:14px;"
    max-width="100%" max-height="300px" contain 
    :src="require('../media/enrichments/rim/basketball-img.jpg')"
  ></v-img>
    Here we can take a photo of the basketball hoop and court background.
  </div>
  <div class="col-mcontainer">
    <h4>Scanning video</h4>
    <Youtube src="4MB5o4W_XJo"/>
    The scanning recording, in this case, is about 45 s long – note that the angles and distances cover what a player might see when dribbling towards the basket or taking a shot
  </div>
</div>

### 3. Supermarket shelf

<div class="mcontainer">
  <div class="col-mcontainer">
    <h4>Reference image</h4>
    <v-img
    class="rounded" 
    style="margin-bottom:14px;"
    max-width="100%" max-height="300px" contain 
    :src="require('../media/enrichments/rim/supermarket-img.jpg')"
  ></v-img>
    This photo captures the assortment of packagíng in the coffee aisle of a supermarket.
  </div>
  <div class="col-mcontainer">
    <h4>Scanning video</h4>
    <Youtube src="d3Yk3nKDIOQ"/>
    Notice that the scanning recording is fairly slow to reduce motion blur for this feature-rich shelf.
  </div>
</div>

### 4. An entire building

<div class="mcontainer" display="grid | inline-grid">
  <div class="col-mcontainer">
    <h4>Reference image</h4>
    <v-img
    class="rounded" 
    style="margin-bottom:14px;"
    max-width="100%" max-height="300px" contain 
    :src="require('../media/enrichments/rim/building-img.jpg')"
    ></v-img>
    This is a photo of the <i>entire</i> building
  </div>
  <div class="col-mcontainer">
    <h4>Scanning video</h4>
    <Youtube src="0U4H-uOIHlw"/>
    We take a longer scanning recording, about 2 min. The angles and distances cover what a person might see whilst walking past or standing in front of the building.
  </div>
</div>

## Scanning best practices
Try to follow these best practices when recording a scanning video:
- Make the recording while holding Neon in your hand rather than wearing it on your head.
- Record the object of interest from all possible angles and from all distances a subject may view them. More diversity is better. Collecting sufficiently diverse viewpoints for a large object, like a building, may require you to move accordingly large distances.
- Move the glasses slowly while recording to avoid motion blur.
- Make sure to have good contrast and that your scene lighting during scanning is similar to that during mapping.

What works and what doesn’t?
- The scene must be **feature-rich** like in the examples above. There has to be enough salient visual content to produce a successful mapping.
- The scene needs to have relatively **static** features in the environment. If there is a lot of movement or the objects change in appearance or shape, the mapping *can* fail.

::: tip
**Ready to go?**<br>
Why not try replicating the above examples? Or even try it with your own use cases! If you haven’t already, we recommend you check out the [Cloud Getting Started Guide](/neon/getting-started/analyse-recordings-in-pupil-cloud/#analyse-recordings-in-pupil-cloud), which covers the basics of working with enrichments.
:::

## Validate the gaze mapping

<div class="pb-4" style="display:flex;justify-content:center;">
  <v-img
    class="rounded" 
    style="margin-bottom:32px;"
    :src="require('../media/enrichments/rim/rim-in-cloud.png')"
    max-width=90%
  >
  </v-img>
</div>

To check if gaze has been mapped successfully, use the side-by-side view:
1. Select a recording.
2. Select the Reference Image Mapper Enrichment.
3. Select the Scene / Reference Image View.
<!-- 4. If you want to visualize and evaluate the 3D model generated (white dots), just turn on the Point Cloud toggle! Not in the new cloud UI (to be deleted if no toggle is added)-->

Now when you play back the recording you can see where gaze is mapped to on your reference image for validation.

## Occlusions

<div class="pb-4" style="display:flex;justify-content:center;">
  <v-img
    class="rounded" 
    :src="require('../media/enrichments/rim/basketball-occlusion.png')"
    max-width=400px
  >
  </v-img>
</div>


Sometimes an object will occlude the feature/object of interest. The reference image mapper may not recognize this, so a false positive mapping could occur. 

If you need to remove the falsely mapped data points, there are a few workarounds.

1. Use Events and Sections to trim out false positive sections.
2. Manually remove the affected data points in the reference image mapper export, by finding the timestamp and deleting the row in the .csv export.

## Repetitions
In cases such as supermarket shopping, where features of the environment like freezers and aisles are repetitive and overlapping, it can be useful to divide recordings into shorter sections using [Events](/neon/basic-concepts/events) for enrichment. This way you can ensure gaze is only mapped to portions of the recording during which you know the user is looking at a particular part of the store.


::: tip
**Want to know more?**<br>
Under the hood, the Reference Image Mapper uses a method called Structure from Motion (SfM) to build a model of the environment. You can see this model as a ‘point cloud’ on the left side video.
:::

<style scoped>
.mcontainer{
  display: flex;
  flex-wrap: wrap;
}
.col-mcontainer{
  flex: 50%;
  padding: 0 4px;
}
@media screen and (min-width: 1025px) and (max-width: 1200px) {
  .col-mcontainer{
    flex: 100%;
  }
}
@media screen and (max-width: 800px) {
    .col-mcontainer{
    flex: 50%;
  }
}
@media screen and (max-width: 400px) {
  .col-mcontainer{
    flex: 100%;
  }
}

</style>