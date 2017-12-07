---
title: "Post: First MLBLR MeetUp HandsOn Tutorial is Up!"
categories:
  - Tutorials Video
tags:
  - Tutorials Video
---

> Here's the video of the First MLBLR MeetUp HandsOn Tutorial.

<div class="fluid-width-video-wrapper">
<iframe markdown="0" width="640" height="360" src="https://youtu.be/MEnNymMOQJE" frameborder="0" allowfullscreen></iframe>
</div>

There were few additional learnings from this simple uploading exercise.

## Why the delay?
We start with apologies for the delay in uploading the video. Here is what happened:
1. video we took on the iPhone 7 plus, with latest HEVC compression, stored the 2.5-hour video with an astonishing file size of 27GB!
2. all file transfers ended at 96% for some reason. All apps on iStore couldn't load the video. iPhone's own "Upload to YouTube" feature in iMovie failed! Each time we undertook any transfer it took more than an hour, so a lot of time was wasted here!

## But!
That wasn't it!
1. Audio recorded was shitty
2. 3 files have FPS of 59.96 and one had weird 50.21 fps.

## What to do next if you're stuck with a similar situation?
Here is what we did:
1. We trimmed the original file into 4 pieces
2. Extracted the sound with Audible
3. Removed the background noise with Audacity
4. Kept only the tutorial parts and removed rest
4. Stitched the video with ffmpeg
5. Added back the music with ffmpeg
6. Amped up the volume with ffmpeg

Here are the ffmpeg commands in case you're interested:

```yaml
    #strip the audio from the video
    ffmpeg -i INPUT.mp4 -codec copy -an OUTPUT.mp4

    #combine/concat videos
    ffmpeg -i "concat:INPUT1.mp4|INPUT2.mp4" -codec copy OUTPUT.mp4

    #amp up the audio
    ffmpeg -i INPUT.mp4 -vcodec copu -af "volume=10dB" OUTPUT.mp4

```

## What to make sure in next HandOn Tutorial?
1. get proper AV system to record better
2. get a **good** microphone
3. if possible set-up live YouTube recording

Suggestions are appreciated!

See you in next HandOn and sincere apologies for not good recording for HandsOn1


