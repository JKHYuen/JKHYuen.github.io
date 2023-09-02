---
layout: page
permalink: /other-projects
title: Other Projects
description: 
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

<!-- TODO: Upload Build, video -->
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
After seeing a widely used effect in some Darkest Dungeon II gameplay, I challenged myself to recreate the effect as close as possible in a day. The effect is created completely procedurally in an HLSL shader, with no pre-made textures.

<h4>Fragment Shader</h4>
The "flaming" edges are implemented with a noise alpha cutoff, with a ```step``` function to get the hard edges. Voronoi noise was used as an alpha mask to create the familiar circular holes. These holes was the most recognizable feature that prompted me to attempt to recreate the effect. UVs can be stretched via variables in the shader to get the more uneven look.

<!-- TODO: talk about angle mask, gradient mask -->

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
*Note: Voronoi implmentation (```Unity_Voronoi_float``` in line 14) is taken from the Voronoi Node in <a href="https://docs.unity3d.com/Packages/com.unity.shadergraph@6.9/manual/Voronoi-Node.html" target="_blank" rel="noopener noreferrer">Unity's Shader Graph documentation.</a>*



<!-- TODO: Upload Build, video -->
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
A recreation of the mobile game *<a href="https://www.youtube.com/watch?v=Wk5JupHelAg" target="_blank" rel="noopener noreferrer">Alto's Adventure</a>* in Unity; made in a 2 day weekend as a challenge. Recreation features similar visuals, backflip boost mechanic and faux slide physics.

<header id="website" class="major page-header"><h1><span class="number">3.</span> This Website</h1></header>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>August 2023</span>
    </div>
</div>
My first website.\\
**Web technologies used:** Jekyll, Liquid, Kramdown, Bundler, jQuery, SASS (in Ruby, Javascript, HTML, and CSS/SCSS).\\
**Theme:** A heavily modified version of the <a href="https://html5up.net/forty" target="_blank" rel="noopener noreferrer">"Forty" theme by HTML5 UP</a>, adapted to Jekyll by <a href="https://github.com/andrewbanchich/forty-jekyll-theme" target="_blank" rel="noopener noreferrer">Andrew Banchich</a>.

<header id="tutoring" class="major page-header"><h1><span class="number">4.</span> Twitch/Discord Programming Tutoring</h1></header>
<div class="project-icon-info other-projects">
    <div>
        <span class="icon fa-calendar-days"></span>
        <span>2020 — Present</span>
    </div>
</div>