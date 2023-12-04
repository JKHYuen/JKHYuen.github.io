---
layout: page
permalink: /other-projects
title: Other Projects
description: Darkest Dungeon II Shader, Mobile game clone, and more
image: assets/images/other-projects.jpg
page-banner: assets/images/other-projects.jpg
nav-menu: true

disable-team-info: I can write anything here to disable header icons
---

<!-- TODO: School stuff: Enigma AI, SIFT -->

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#dd-shader" class="button small scrolly"><span class="number">1.</span> Darkest Dungeon II Shader</a></li>
    <li><a href="#alto" class="button small scrolly"><span class="number">2.</span> Alto Clone</a></li>
    <li><a href="#website" class="button small scrolly"><span class="number">3.</span> This Website</a></li>
    <li><a href="#tutoring" class="button small scrolly"><span class="number">4.</span> Twitch/Discord Programming Tutoring</a></li>
</ul>
</div>

<!-- TODO: write readme for build -->
<header id="dd-shader" class="major page-header"><h1><span class="number">1.</span> Darkest Dungeon II Shader</h1></header>
<a href="https://github.com/JKHYuen/DarkestDungeonII-ShaderDemo" target="_blank" rel="noopener noreferrer" class="button icon fa-download">Download Interactive Demo</a>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-users"></span>
        <span>Solo Project</span>
    </div>
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>January 3 2022</span>
    </div>
</div>

<video class="scroll-auto embedded-video" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/dd-demo.mp4" type="video/mp4">
  Shader Demo Video
</video>

After seeing a widely used black dissolve effect in some Darkest Dungeon II gameplay, I challenged myself to recreate the shader as close as possible in a day. Although it is possible the original effect used scrolling textures, my version is created exclusively with procedural noise in an HLSL shader. Try the downloadable demo to see an interactive sample UI and environment that mimics the game (press ```space``` to toggle environment and ```tab``` to toggle UI with animation). 

The "flaming" edges are created with a noise alpha cutoff, with a ```step(...)``` function to get the hard edges. Voronoi noise was used as an additional alpha mask to create the familiar circular holes. UVs can be stretched via variables in the shader to make the circles look irregular. The scenes in the demo were created with material instances on quads of various sizes. I am satisfied with the final result, however additional particles and animation edits need to be made for a more accurate replication. Also, upon further inspection, the original effect contains one more layer of subtle scrolling noise to "wiggle" the hard edges on certain environmental elements.

<h4>The Fragment Shader</h4>
{% highlight hlsl linenos %}
fixed4 frag(v2f i) : SV_Target {
    float2 unscaledUV = i.uv;
    i.uv *= float2(1 + _UvStretch_X, 1 + _UvStretch_Y);

    float gradient = (1 - saturate(i.uv.y + _GradientHeight)) * (1 - saturate(i.uv.x + _GradientWidth));

    float mask = (unscaledUV.x + 0.1) / (1 - unscaledUV.y);
    mask = smoothstep(_AngleMask - 0.9, _AngleMask, mask);

    float noise = Unity_SimpleNoise_float(i.uv + _UVShift - _NoiseScrollVector * _Time.x, _NoiseScale);

    float vOut;
    float vCells;
    Unity_Voronoi_float(
        ((i.uv + _UVShift) * float2(_VoronoiStretch_X, _VoronoiStretch_Y)) - _VoronoiScrollVector * _Time.x,
        _VoronoiAngleSpeed * _Time.x + 2,
        _VoronoiCellDensity, vOut, vCells
    );

    _VoronoiThreshold *= 1 - gradient;

    vOut = saturate(
        Unity_Remap_float(vOut, float2(0, 1), float2(-_VoronoiThreshold, _VoronoiThreshold) * mask)
    );

    noise = step(noise * mask, _NoiseStep * gradient);
    vOut = step(vOut, _VoronoiStep);

    return _Color * noise * vOut;
}
{% endhighlight %}
*Note: Functions ```Unity_Voronoi_float(...)```, ```Unity_Remap_float(...)```, and ```Unity_SimpleNoise_float(...)``` are adapted from <a href="https://docs.unity3d.com/Packages/com.unity.shadergraph@6.9/manual/Voronoi-Node.html" target="_blank" rel="noopener noreferrer">Unity's Shader Graph documentation</a>.*

All variables that start with an underscore can be controlled in gameplay code. For example, ```_GradientHeight``` and ```_GradientWidth``` are the primary variables used to "dissolve in" sprite elements vertically or horizontally (this is used for the UI panel toggle animation). The two parameters are consolidated into the ```gradient``` variable to control both noise alpha thresholds at the same time. The ```_NoiseStep``` and ```_VoronoiStep```variables can be used to roughly control the length of the "dissolved" end (see video below for demonstration). 

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/dd-params.mp4" type="video/mp4">
  Shader Parameter Video
</video>
*Note: For a real project I would probably limit all shader variables in the inspector with sliders with normalized values.*

Since the scene uses many elements with the same shader, the noise generation will noticeable synchronize and look unnatural. To alleviate this, I added the ```_UVShift``` variable in ```line 10``` so a random noise offset can be generated in gameplay code when the scene loads. A more elegant solution would be to generate a hash value based on object position within the shader.

Lastly, a ```mask``` value is calculated in the shader based on UV to create an optional diagonal alpha mask (```line 7 — 8```). The angle of this mask is controlled by only one variable for convenience; not very flexible but it is good enough for the demo. This mask is used to make the angled dissolved UI bars on the top of the screen.

<header id="alto" class="major page-header"><h1><span class="number">2.</span> Alto Clone</h1></header>
<a href="https://github.com/JKHYuen/AltoCloneBuild" target="_blank" rel="noopener noreferrer" class="button icon fa-download">Download Playable Build</a>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-users"></span>
        <span>Solo Project</span>
    </div>
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>July 25 2020 — July 27 2020</span>
    </div>
</div>

A clone of the mobile game *<a href="https://www.youtube.com/watch?v=Wk5JupHelAg" target="_blank" rel="noopener noreferrer">Alto's Adventure</a>* in Unity; made in a 2 day weekend as a challenge. The main appeal to the original game is the relaxing and satisfying gameplay, which is exemplified by the one button controls and what I believe to be customized physics.

<video class="scroll-auto embedded-video" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/alto.mp4" type="video/mp4">
  Alto Video
</video>
*Note: Recreation features similar visuals, backflip boost mechanic and slide physics. Mouse cursor unfortunately not hidden in build.*

I opted for a mix of the built in Unity physics engine and application of some manual forces to make the movement more smooth. For example, a light constant downward force is applied every physics update whenever the player object is touching the ground. Additionally, whenever the player is not touching the ground, a raycast is cast directly below to get the normal of the ground. The player will automatically be gradually rotated to match the angle of the ground below. All these tweaks make it so the player does not need to worry about sliding with the ground unless interacting with the jump/spin mechanic. 

In my implementation, the player object will still occasionally launch over smooth hills. The original game is quite strict in keeping the character in contact with the smooth ground curves. This leads me to believe the original may lean more heavily in manually calculated movement rather than relying on a physics engine. I also added a couple of personal touches in my build not present in the original; such as additional particle effects and a "glide" mechanic that lets the player briefly float mid air based on number of backflips performed (indicated by UI bar element). 

<header id="website" class="major page-header"><h1><span class="number">3.</span> This Website</h1></header>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-users"></span>
        <span>Solo Project</span>
    </div>
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>August 2023, Ongoing</span>
    </div>
</div>
My first website.\\
**Web technologies used:** Jekyll, Liquid, Kramdown, Bundler, jQuery, SASS (Ruby, Javascript, HTML, and CSS/SCSS).\\
**Theme:** A heavily modified version of the <a href="https://html5up.net/forty" target="_blank" rel="noopener noreferrer">"Forty" theme by HTML5 UP</a>, adapted to Jekyll by <a href="https://github.com/andrewbanchich/forty-jekyll-theme" target="_blank" rel="noopener noreferrer">Andrew Banchich</a>.

<header id="tutoring" class="major page-header"><h1><span class="number">4.</span> Twitch/Discord Programming Tutoring</h1></header>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>2020 — Present</span>
    </div>
</div>
I streamed the development of *<a href="{{ site.baseurl }}/last-secutor" target="_blank" rel="noopener noreferrer">Last Secutor</a>* full time (5+ streams a week) from 2020 - 2022 on Twitch. My streams primarily consisted of C#/HLSL programming. I also developed almost the entirety of *<a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">PHYSARUM</a>* live on stream. Other streams activities include shader experiments, game rendering/programming research, game design discussion, and C++ practice. I still do occasional programming streams currently, but much less often.

 Despite being a very small stream I always encourage aspiring game devs and programmers in chat to ask any technical questions that they may have. This has lead to impromptu lessons on beginner-friendly fundamental programming topics such as memory management, value vs. reference types, classes vs. structs and hash functions. As well as frequent explanations on how my game code/shaders work and pros and cons of different implementations. I have tutored many viewers in game development and programming over the years and gained a small following on my Twitch and Discord channel, where I answer questions off stream and personally handle all bug reports for my released projects.