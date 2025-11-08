---
theme: default
title: Learned Display Radiance Fields with Lensless Cameras
transition: slide-left
background: linear-gradient(135deg, #0f172a, #1e293b)
class: text-white
colorSchema: dark
---

<!-- Title -->
<h1 class="font-semibold tracking-tight leading-tight -mt-46">
  Learned Display Radiance Fields with Lensless Cameras
</h1>

<!-- Subtitle -->
<p class="italic text-xl text-gray-300">
  Accessible, angle-aware display calibration
</p>

<!-- Authors -->
<div class="text-lg text-gray-200 mt-4">
  <a href="https://ziyang.space"><span class="text-white font-bold">Ziyang Chen</span></a>, <a href="https://augvislab.github.io/people/yuta-itoh">Yuta Itoh</a>, and <a href="https://www.kaanaksit.com/">Kaan Akşit</a>
</div>

<!-- Lab logo in corner -->
<div class="absolute bottom-10 right-14">
  <img src="/logo.png" alt="lab logo" class="h-[200px] opacity-100">
</div>
<div class="absolute bottom-20 left-14">
  <img src="/sigasia.png" alt="lab logo" class="h-[100px] opacity-100">
</div>

<!--
Welcome everyone, and thank you for taking the time to join my presentation.
Today, I’m delighted to share our work, “Learned Display Radiance Fields with Lensless Cameras.”
This project is a collaborative effort with Professor Yuta Itoh from the **Institute of Science Tokyo** and my supervisor, Professor Kaan Akşit.👆

-->

---
layout: cover
---

#  Motivation

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Why do we need display calibration and why it is useful, let's understand more about it 👆
-->

---

# Why Do We Need Display Calibration?

<v-click>

- Displays are ubiquitous in our life

</v-click>

<br>

<div v-click="['2']" class="absolute flex justify-center gap-8 mt-6 left-35" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
  <div>
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img src="/Laptop_computer_monitor_(Unsplash).jpg" 
          alt="sensor" 
          class="w-80 h-60 object-cover block">
    </div>
    <div class="text-center mt-2">
      Computer
      <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
        <a href="https://commons.wikimedia.org/wiki/File:Laptop_computer_monitor_(Unsplash).jpg">Taduuda taduuda</a>, CC0, via Wikimedia Commons
      </p>
    </div>
  </div>

  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/OpenStreetMap-on-Iphone15Plus.jpg" 
            alt="sensor" 
            class="w-80 h-60 object-cover block">
      </div>
      <div class="text-center mt-2">
        Smart phone
        <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
          <a href="https://commons.wikimedia.org/wiki/File:OpenStreetMap-on-Iphone15Plus.jpg">Infinite Bed</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons
        </p>
      </div>
  </div>
</div>

<div v-click="3" class="absolute flex justify-center gap-8 mt-6 left-35" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
  <div>
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img src="/Apple_Vision_Pro_on_display_in_Toronto,_Canada_-_Aug_2024.jpg" 
          alt="sensor" 
          class="w-80 h-60 object-cover block">
    </div>
    <div class="text-center mt-2">
      Video-see-through AR headset
      <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
        <a href="https://commons.wikimedia.org/wiki/File:Apple_Vision_Pro_on_display_in_Toronto,_Canada_-_Aug_2024.jpg">LR.127</a>, <a href="https://creativecommons.org/licenses/by/4.0">CC BY 4.0</a>, via Wikimedia Commons
      </p>
    </div>
  </div>

  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/2CR_Soldiers_use_virtual_reality_for_Counter-Unmanned_Aerial_Systems_Training_(8867750).jpg" 
            alt="sensor" 
            class="w-80 h-60 object-cover block">
      </div>
      <div class="text-center mt-2">
        VR headset
        <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
          <a href="https://commons.wikimedia.org/wiki/File:2CR_Soldiers_use_virtual_reality_for_Counter-Unmanned_Aerial_Systems_Training_(8867750).jpg">U.S. Army photo by Pfc. Brent Lee</a>, Public domain, via Wikimedia Commons
        </p>
      </div>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
👆Displays are everywhere in our daily life, from 👆 computers to smart phones. In recent years, we are also exposed to the virtual imagery with rise of 👆 both AR and VR headsets👆
-->

---

# Why Do We Need Display Calibration?

<v-click>
<span class="text-[2em] text-red-500">But,</span>
</v-click>
<v-click>
displays often suffer from defects such as:
</v-click>

<br>
<br>

<div v-click="[3, 5]"
  v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 250 }"
  :click-4="{ x: -1 }"
  class="absolute ">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/backlight_bleeding.png" 
            alt="sensor" 
            class="h-80 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Backlight bleeding
      </div>
  </div>
</div>

<div v-click=5
  v-motion
  :initial="{ x: -1}"
  class="absolute">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/backlight_bleeding_boxes.png" 
            alt="sensor" 
            class="h-80 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Backlight bleeding
      </div>
  </div>
</div>

<div v-click=5 v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }" 
  class="absolute right-30 bottom-2">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/backlight_bleeding_boxes_zoom_in.png" 
            alt="sensor" 
            class="h-100 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Zoom in views
      </div>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
However in these displays👆, not every pixel is equal👆 for example 👆 when I display a full black image with the liquid crystal display in our lab, you can see it does not produce an uniform black pattern 👆 if we zoom-in the image 👆 we can see that the light leaks from the edges. This is usually referred as backlight bleeding
-->

---

# Why Do We Need Display Calibration?

<v-click>
Displays also suffer from color inconsistency
</v-click>

<br>
<br>

<div v-click="[2, 4]"
  v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 250 }"
  :click-3="{ x: -1 }"
  class="absolute ">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/discoloration.png" 
            alt="sensor" 
            class="h-80 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Discoloration
      </div>
  </div>
</div>

<div v-click=4
  v-motion
  :initial="{ x: -1}"
  class="absolute">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/discoloration_boxes.png" 
            alt="sensor" 
            class="h-80 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Discoloration
      </div>
  </div>
</div>

<div v-click=4 class="absolute right-30 bottom-2" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
  <div>
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/discoloration_boxes_zoom_in.png" 
            alt="sensor" 
            class="h-100 w-auto object-cover block">
      </div>
      <div class="text-center mt-2">
        Zoom in views
      </div>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Despite the non uniform intensities,👆 displays also suffer from color inconsistency👆 Now, I turn on two displays in our lab👆 showing the identical color pattern on both displays 👆 As you can see the color varies dramatically from display to display.👆
-->

---

# Why Do We Need Display Calibration?

<v-click>
Another common display defects comes with the geometric viewing positions
</v-click>

<br>
<br>

<div class="absolute left-40" v-click="[2,3]" >
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <video controls autoplay muted loop playsinline style="width: 650px;"  >
      <source src="/rotational_display.mp4" type="video/mp4">
    </video>
  </div>
</div>

<div class="absolute left-40" v-click=3 >
  <div class="bg-white p-2 rounded-lg shadow-lg">
  <video controls autoplay muted loop playsinline style="width: 650px;"  >
    <source src="/depth_display.mp4" type="video/mp4">
  </video>
  </div>
</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Another common display defect comes with the geometric viewing positions 👆 This could either due to rotations or 👆 changing position in depth 👆
-->

---

# Why Do We Need Display Calibration?

<v-click>
These defects happen to near-eye display as well
</v-click>

<br>
<br>

<div class="absolute left-60" v-click>
  <div class="bg-white p-2 rounded-lg shadow-lg">
  <video controls autoplay muted loop playsinline style="width: 500px;"  >
    <source src="/ar_display.mp4" type="video/mp4">
  </video>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
These view-dependent distortions happen to near-eye displays as well. 👆Here is a footage captured with my Xreal glasses👆
-->

---

# Motivation


<v-click>
So far we have covered three types of display defects:
</v-click>

<br>

<div class="relative">
  <div v-click="[2,7]">

  - Intensity non-uniformity

  </div>
  <div v-click="7" class="absolute top-0 left-0">

  - **Intensity non-uniformity**

  </div>
</div>

<div class="relative">
  <div v-click="[3,7]">

  - Color inconsistency

  </div>
  <div v-click="7" class="absolute top-0 left-0">

  - **Color inconsistency**
  </div>
</div>


<div v-click="4">


</div>
<div class="relative">
  <div v-click="[4,7]">

  - Viewing-angle dependent distortion


  </div>
  <div v-click="7" class="absolute top-0 left-0">
  
  - <span class="text-gray-800">Viewing-angle dependent distortion</span>

  </div>
</div>

<div class="absolute flex justify-center gap-8 mt-2 left-35" >
  <div v-click="[5,7]" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img src="/Logo_design_sketching.jpg" 
          alt="sensor" 
          class="w-80 h-60 object-cover block">
    </div>
    <div class="text-center mt-2">
      Graphic designer
      <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
        <a href="https://commons.wikimedia.org/wiki/File:Logo_design_sketching.jpg">Claireneon</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons
      </p>
    </div>
  </div>

  <div v-click="[6, ]" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
      <div class="bg-white p-2 rounded-lg shadow-lg">
        <img src="/1280px-CCCamp_2019_by_CountCrapula_034.jpg" 
            alt="sensor" 
            class="w-80 h-60 object-cover block">
      </div>
      <div class="text-center mt-2">
        Video editor
        <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
          <a href="https://commons.wikimedia.org/wiki/File:CCCamp_2019_by_CountCrapula_034.jpg">CountCrapula</a>, <a href="https://creativecommons.org/licenses/by-sa/4.0">CC BY-SA 4.0</a>, via Wikimedia Commons
        </p>
      </div>
  </div>
</div>

<div class=" flex justify-center gap-8 mt-2 " >
  <div v-click="8" v-motion
  :initial="{ x: 50 }"
  :enter="{ x: 0 }"
  :leave="{ x: 50 }">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img src="/Monitor_Calibration_2010-by-RaBoe-20.jpg" 
          alt="sensor" 
          class="w-80 h-60 object-cover block">
    </div>
    <div class="text-center mt-2">
      Colorimeter
      <p class="text-[0.55em] text-gray-500 mt-2" style="margin: 0;">
        <a href="https://commons.wikimedia.org/wiki/File:Monitor_Calibration_2010-by-RaBoe-20.jpg">Ra Boe / Wikipedia</a>, <a href="https://creativecommons.org/licenses/by-sa/3.0/de/deed.en">CC BY-SA 3.0 DE</a>, via Wikimedia Commons
      </p>
    </div>
  </div>
</div>

<div v-click=9 class="absolute right-15 top-10">

<span class="text-red-500 " style="font-size: 30px;">❌ Fixed viewing position only</span>

</div>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!-- 
👆 So far we have covered three types of display defects including: 👆 intensity non-uniformity, 👆 color inconsistency, 👆 and viewing-angle dependent distortion.

For content creators such as graphic designers 👆 and video editors 👆, having a properly calibrated display with accurate color and intensity is essential, as they need to ensure a consistent and reliable visual experience across different devices and viewing environments.

The first two defects 👆 are well resolved by a device called colorimeter 👆 However it only assumed a fixed viewing positions 👆 leading to invalid assessments for other viewing positions.

-->



---

# Motivation


<v-clicks>

<div> 
  <br>
  ISO standard defines procedures to assess the uniformity distribution of Flat Panel Displays (FPD)

</div>

Which requires:

</v-clicks>

<v-clicks depth=2>

- A dark room
- Many captures of the displays with many viewing angles
- Complex setup & alignment

</v-clicks>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
👆 The industrial standard for evaluating the uniformity of flat panel displays requires 👆 measuring their brightness from 👆 many different viewing angles in a 👆 dark room — and that usually involves a 👆 complicated setup and precise alignment.
-->

---
transition: none
---

# Motivation

<br>

<div class="absolute left-40" >
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <video controls autoplay muted loop playsinline style="width: 650px;"  >
      <source src="/Conventional.mp4" type="video/mp4">
    </video>
  </div>
  <div class="text-center mt-2">
    Capturing angle-dependent intensity changes using the <a href="https://www.iso.org/standard/40100.html">ISO standard 9241-305:200</a>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Here’s a time-lapse of me capturing the display’s angular intensity distribution using the ISO standard in our lab, which took about 10 minutes. As you can see I had to constantly move the camera ensuring it is pointing at the center of the display, and I have to account for the camera position using a checkerboard pattern for every capture.
-->

---

# Motivation

<br>

<div class="absolute left-40" >
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <video controls autoplay muted loop playsinline style="width: 650px;"  >
      <source src="/Heatmap.mp4" type="video/mp4">
    </video>
  </div>
  <div class="text-center mt-2">
    Captured angle-dependent intensity heatmap using the <a href="https://www.iso.org/standard/40100.html">ISO standard 9241-305:200</a>
  </div>
</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
And here is the captured display intensity heatmap with varying viewing angles.
-->

---

# Motivation


<br>
<br>
<br>
<br>
<br>
<span v-click class="text-3xl">
  <i>
  An <span class="text-green-500 font-semibold">accessible</span> method with a reasonable amount of captures is needed to measure the image quality of the displays from <span class="text-green-500 font-semibold">arbitrary viewpoints</span>.
  </i>

</span>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
This is a time-consuming and user-unfriendly task hinders daily calibration for average users which means: 👆
 an accessible method with reasonable amount of captures is needed to measure the image quality of the displays from arbitrary viewpoints
-->


---
layout: cover
---

# Implementation

<!--
Now let's talk about the implementation of our prototype
-->

---

# Idea

<br>
<v-clicks>

- **Lensless camera** captures angular information
- **Implicit Neural Representation** learns pixel light fields


<div  style="position: absolute; bottom: 30px" v-motion
  :initial="{ x: -50 }"
  :enter="{ x: 140 }"
  >
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/lenless_lightfield_overview.png"
      class="w-150 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Pixel light fields acquisition with our lensless camera
  </div>
</div>

</v-clicks>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
We propose to use a 👆 lensless camera together with an 👆 implicit neural representation to measure angle-dependent display intensities,👆 with a simpler setup 👆. Before we dive into the setup, I would love to first explain what is lensless camera
-->

---
transition: fade
class: text-white
layout: default
---

# Imaging system

<div v-click=[1,2] style="position: absolute; left: 50%; bottom: 80px; transform: translateX(-50%);" >
  <div class="bg-black border-8 border-white p-2 rounded-lg shadow-lg">
    <img src="/conventional.png" alt="sensor" class="w-130 h-auto object-cover">
  </div>
  <div class="text-center mt-2">
    <span class="text-orange-500">One-to-One</span> mapping
  </div>
</div>

<div v-click=[2,3] style="position: absolute; left: 50%; bottom: 80px; transform: translateX(-50%);">
  <div class="bg-black border-8 border-white p-2 rounded-lg shadow-lg">
    <img src="/no_lens.png" alt="sensor" class="w-130 h-auto object-cover">
  </div>
  <div class="text-center mt-2">
    <span class="text-orange-500">One-to-Many</span> mapping
  </div>

</div>

<div v-click=3 style="position: absolute; left: 50%; bottom: 80px; transform: translateX(-50%);">
  <div class="bg-black border-8 border-white p-2 rounded-lg shadow-lg">
    <img src="/lensless_system.png" alt="sensor" class="w-130 h-auto object-cover">
  </div>
  <div class="text-center mt-2">
    <span class="text-orange-500">One-to-Selected</span> mapping
  </div>

</div>

<p v-click=1 style="position: absolute; bottom: 0px; right: 20%; font-size: 0.6em; color: #888;">
<a href="https://commons.wikimedia.org/wiki/File:Ccd-sensor.jpg">C-M</a>, <a href="http://creativecommons.org/licenses/by-sa/3.0/">CC BY-SA 3.0</a>, via Wikimedia Commons
</p>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
Let's first think of the conventional imaging setup👆, where we have the object on the left, lens at the middle, and sensor on the right. In this case, each point on the object has a one-to-one mapping on the imaging sensor. This one-to-one mapping does not provide any angular diversity for the captured points👆

Without a lens, light rays from every point on the object spread out and hit multiple points on the sensor simultaneously, creating an unfocused image that captures information from wide varity of angles.👆

By adding a specially designed mask, we can control or modulate the light reaching to the sensor. This creates a typical lensless imaging system where the target images are reconstructed with post-processing pipelines
You can see from this plot that only secleted light are able to pass and captured by the sensor.
In our proposal we will be utilizing lensless camera's ability to capture angular information with a single shot. whereas the conventional cameras would require multiple captures
-->

---

# Forward model

<div v-click>

We model the lensless camera as a linear convolution process. 

</div>

<div v-click=[1,2]>
  <div  style="position: absolute; bottom: 90px; left: 100px;">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img 
        src="/lensless_convolution.png"
        class="w-190 h-auto object-cover"
      >
    </div>
    <div class="text-center mt-2">
      Lensless convolution
    </div>
  </div>
</div>

<div v-click=[2,3]>
  <div  style="position: absolute; bottom: 90px; left: 100px;">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img 
        src="/lensless_convolution_1.png"
        class="w-190 h-auto object-cover"
      >
    </div>
    <div class="text-center mt-2">
      Lensless convolution
    </div>
  </div>
</div>

<div v-click=[3,4]>
  <div  style="position: absolute; bottom: 90px; left: 100px;">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img 
        src="/lensless_convolution_2.png"
        class="w-190 h-auto object-cover"
      >
    </div>
    <div class="text-center mt-2">
      Lensless convolution
    </div>
  </div>
</div>

<div v-click=[4,5]>
  <div  style="position: absolute; bottom: 90px; left: 100px;">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img 
        src="/lensless_convolution_3.png"
        class="w-190 h-auto object-cover"
      >
    </div>
    <div class="text-center mt-2">
      Lensless convolution
    </div>
  </div>
</div>

<div v-click=5>
  <div  style="position: absolute; bottom: 90px; left: 100px;">
    <div class="bg-white p-2 rounded-lg shadow-lg">
      <img 
        src="/lensless_convolution_4.png"
        class="w-190 h-auto object-cover"
      >
    </div>
    <div class="text-center mt-2">
      Lensless convolution
    </div>
  </div>
</div>

<div v-click=6 class="absolute right-15 top-10">

<span class="text-green-500 " style="font-size: 30px;">✅ Linear operation</span>

</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!--
We model our lensless camera as a convolutional approximation, 👆 where the 👆sensor measurement 👆is represented as the convolution 👆 between the scene’s radiance 👆 and the precaptured point spread function (PSF) 👆.
This formulation assumes spatial invariance within the local region of interest, allowing us to describe the image formation process as a 👆linear operation.
-->

---

# Hardware

<div v-click>
We need to keep the aperture small to maintain spatial invariance 
</div>

<br>

<div v-click="[1,2]" v-motion
  :initial="{ x: -40 }"
  :enter="{ x: 250 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/incident_angle.png"
      class="w-80 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
</div>

<div v-click="[2,3]" v-motion
  :enter="{ x: 250 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/incident_angle_1.png"
      class="w-80 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
</div>

<div v-click="[3,5]" v-motion
  :enter="{ x: 250 }"
  :leave="{ x: 40 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/incident_angle_2.png"
      class="w-80 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
</div>

<div v-click="[4,5]" class="absolute right-15 top-10">

<span class="text-red-500 " style="font-size: 30px;"> ❌ Limited FoV</span>

</div>

<div v-click="[5,6]" v-motion
  :initial="{ x: -40 }"
  :enter="{ x: 200 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/fov_expansion_3.png"
      class="w-130 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
  
</div> 

<div v-click="[6,7]" v-motion
  :enter="{ x: 200 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/fov_expansion_1.png"
      class="w-130 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
  
</div> 

<div v-click="7" v-motion
  :enter="{ x: 200 }"
  class="absolute">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/fov_expansion_0.png"
      class="w-130 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Incident angle illustration
  </div>
  
</div> 


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
In order to maintain spatial invariance, 👆 we need to keep the aperture small 👆, however the field of view is largely dependent on the aperture size👆 and this samll aperture limits the practical FoV 👆. Therefore, we use an aperture array 👆 to expand the FoV, under the assumption that the adjecent pixels have similar behavior. so as we keep the sensor fixed, we turn on the pixels sequencially 👆👆.
-->

---

# Ours

<br>

<div v-clicks>

- We sample nine positions on the display with our lensless camera
- Computationally recover the angular information of the display

</div>

<v-clicks>

<div  style="position: absolute; bottom: 25px; transform: translateX(85%);">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/lensless_camera.png"
      class="w-70 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Top view of our lensless camera
  </div>
</div>


</v-clicks>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!-- 
Here's a time-lapse showing our proposed workflow, which takes about 2 minutes.
-->

---
transition: none
---
# Ours Video


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
---

<video controls style>
  <source src="/Ours.mp4" type="video/mp4">
</video>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

---

# INR Model


<v-clicks>


<!-- THIS ONE WORKS SO WELL -->
<div  style="position: absolute; bottom: 40px; transform: translateX(25%);">
  <div class="bg-white p-2 rounded-lg shadow-lg inline-block">
    <img src="/model_pipeline.png" alt="sensor" class="w-150 h-auto object-cover">
  </div>
  <div class="text-center mt-2">
    Model overview
  </div>
</div>

</v-clicks>


<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!-- 
Our implicit neural representation uses fully connected layers with 32 neurons and a sinusoidal activation.
For each input coordinate group, we apply positional encoding at multiple frequency levels.
These encoded features are then concatenated and passed through the network to reconstruct the light field.
We convolve this reconstruction with the pre-captured point spread functions to predict the lensless image.
Finally, we compare the predicted image with the captured one to compute the loss.
-->

---

# Results

We compare the simulated display digital twin with the real-world display capture that is captured with a conventional camera

<br>

<v-clicks>

<div  style="position: absolute; bottom: 75px; transform: translateX(25%);">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/real_world_simulation.png"
      class="w-150 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    Comparison between real-world and simulation display
  </div>
</div>
</v-clicks>



<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!-- 
We use the model to simulat the display image at different view point, as shown in the image down below.
-->
---

# Results

We can also simulate the pixels at close viewpoints

<v-clicks>

<div  style="position: absolute; left: 50%; bottom: 80px; transform: translateX(-50%);">
  <div class="bg-white p-2 rounded-lg shadow-lg inline-block">
    <img src="/supplementary_zoomin.png" alt="sensor" class="w-400 h-auto object-cover">
  </div>
  <div class="text-center mt-2">
  The average intensity comparison
  </div>
</div>
</v-clicks>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>
<!-- 
We can also simulate a close up view of the display.
-->
---

# Results

The novel pixels pixels with different incident angles show similar radial pattern with the professional equipment result

<div style="display: flex; justify-content: center; align-items: flex-start; gap: 20px; position: absolute; left: 50%; bottom: 80px; transform: translateX(-50%);">

  <!-- First image -->
  <div class="bg-white p-2 rounded-lg shadow-lg" style="flex: 0 0 auto;">
    <img src="/interpolation_w_heatmap.png" alt="sensor" style="height: 200px; width: auto; object-fit: cover;">
    <div class="text-center mt-2">
      The average intensity comparison
    </div>
  </div>

  <!-- Second image + credit -->
  <figure style="flex: 0 0 auto; text-align: center;">
    <a href="https://example.com/original-image-page" target="_blank" rel="noopener noreferrer">
      <img
        src="https://sensing.konicaminolta.asia/wp-content/uploads/2023/11/Radiant-Conoscope-Lens-system-Cartesian-Coordinates.webp"
        alt="Short, accurate description of the image"
        loading="lazy"
        decoding="async"
        style="height: 250px; width: auto; object-fit: contain; background: white; padding: 4px; border-radius: 8px; box-shadow: 0 2px 6px rgba(0,0,0,0.15);"
      >
    </a>
    <figcaption style="font-size:0.75rem; color:#6b7280; margin-top: 0.25rem;">
      Used for commentary/educational purposes; all rights belong to the copyright holder.
      <a href="https://sensing.konicaminolta.asia/fast-and-accurate-way-to-measure-viewing-angle-performance-of-display/" target="_blank" rel="noopener noreferrer">Konica Minolta</a>.
    </figcaption>
  </figure>

</div>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!-- 
We evaluate pixel consistency by checking how well the reconstructed light fields maintain intensity variations across continuous horizontal and vertical angles.
On the left, you can see that the average pixel intensity changes smoothly, showing that our model can predict new pixel values that depend on the viewing angle.
These predicted pixels also exhibit a similar radial pattern to the results measured with professional equipment on the right.
-->
---

# Results

<v-clicks>

- **PSNR** <span class="text-green-500">19.54 dB</span>
- **SSIM** <span class="text-green-500">0.9165</span>; **MSSIM** <span class="text-green-500">0.9549</span>
- Matches ISO trends without rotation/darkroom

</v-clicks>

<v-clicks>

<div  style="position: absolute; bottom: 30px; transform: translateX(20%);">
  <div class="bg-white p-2 rounded-lg shadow-lg">
    <img 
      src="/capture_illustration.png"
      class="w-150 h-auto object-cover"
    >
  </div>
  <div class="text-center mt-2">
    The average intensity comparison
  </div>
</div>

</v-clicks>

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!-- 
Our method delivers high image quality for novel pixels, and its normalized intensity closely follows the trend defined by the ISO standard.
-->

---

# Thank you for watching!

<div class="absolute bottom-4 right-6 text-sm text-gray-400">
  <SlideCurrentNo /> / <SlidesTotal />
</div>

<!--
-
-->
