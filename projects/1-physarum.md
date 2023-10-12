---
layout: page
permalink: /physarum
title: "PHYSARUM: Slime Mold Simulator"
description: Interactive sandbox/visualizer of the real life organism <i>Physarum polycephalum</i>
image: assets/images/physarum.jpg
page-banner: assets/images/physarum-page-banner.jpg
nav-menu: true

button-icon: fa-steam
button-url: https://store.steampowered.com/app/1667120?utm_source=portfolio
button-text: Steam Store Page
team-text: Solo project, with help from a composer for trailer and gameplay music
date-text: April 2021 — August 2021
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly"><span class="number">1.</span> Overview</a></li>
    <li><a href="#highlights" class="button small scrolly"><span class="number">2.</span> Highlights</a></li>
    <li><a href="#features" class="button small scrolly"><span class="number">3.</span> Game Features</a></li>
        <li><a href="#customize" class="button small scrolly sub-section"><span class="number">3.1</span> Fully Customizable Simulation</a></li>
        <li><a href="#game-modes" class="button small scrolly sub-section"><span class="number">3.2</span> Game Modes</a></li>
        <li><a href="#morph" class="button small scrolly sub-section"><span class="number">3.3</span> Morph</a></li>
        <li><a href="#share" class="button small scrolly sub-section"><span class="number">3.4</span> Share</a></li>
        <li><a href="#learn" class="button small scrolly sub-section"><span class="number">3.5</span> Learn</a></li>
    <li><a href="#reception" class="button small scrolly"><span class="number">4.</span> Reception</a></li>
    <li><a href="#implementation" class="button small scrolly"><span class="number">5.</span> Implementation</a></li>
        <li><a href="#compute-shaders" class="button small scrolly sub-section"><span class="number">5.1</span> Compute Shaders</a></li>
        <li><a href="#tooltip" class="button small scrolly sub-section"><span class="number">5.2</span> Tooltip Framework</a></li>
        <li><a href="#color-picker" class="button small scrolly sub-section"><span class="number">5.3</span> Color Picker</a></li>
</ul>
</div>

<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/rW9ZsO6LYdk" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*Note: UI aesthetic design was not finalized in the trailer, see screenshots on <a href="https://store.steampowered.com/app/1667120?utm_source=portfolio" target="_blank" rel="noopener noreferrer">Steam</a> or below for the final UI look.*

A project that evolved into a fully featured product while learning how to make <a href="https://learn.microsoft.com/en-us/windows/win32/direct3d11/direct3d-11-advanced-stages-compute-shader" red="noopner noreferrer">compute shaders</a>. I took the opportunity to release this small game publicly to also learn the process of marketing and shipping a game on Steam.

*PHYSARUM: Slime Mold Simulator* is an interactive sandbox visualizer of the real life organism *Physarum polycephalum*; all simulated on a single compute shader (simulation model of the slime mold is based on <a href="https://uwe-repository.worktribe.com/output/980579" target="_blank" rel="noopener noreferrer">this paper</a>). The GPU bound AI easily allows for millions of slime agents to be simulated in real time. Although not a traditional "game", *PHYSARUM: Slime Mold Simulator* is designed to encourage users to explore and discover in the sandbox environment for entertainment value. See trailer above for a full feature showcase.

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>Simulation and UI implementation done in the Unity game engine, with the built-in renderer
        <ul class="highlights-list sub">
			<li>C# and Cg/HLSL programming</li>
			<li>Experience dispatching GPU processes with compute shaders</li>
            <li>All shaders, game logic and UI implementations coded solo from scratch, without plug-ins or store assets (See <a href="#implementation" class="scrolly">5. Implementation</a> for examples)</li>
        </ul>
    </li>
    <li>UI/UX design
        <ul class="highlights-list sub">
			<li>UI designed and implemented with base Unity UI components</li>
            <li>Some icons used from <a href="https://kenney.nl/assets/game-icons" target="_blank" rel="noopener noreferrer">Kenney's game icons</a>, others are custom made</li>
        </ul>
    </li>
    <li>Full product launch on Steam
        <ul class="highlights-list sub">
			<li>Free Demo for users to test hardware requirements</li>
			<li>Steam store page set up with custom marketing assets</li>
			<li>Experience with the Steamworks SDK to create and deliver builds</li>
			<li>Positive Steam reviews (See <a href="#reception" class="scrolly">4. Reception</a> for details)</li>
        </ul>
    </li>
    <li>Zero budget marketing
        <ul class="highlights-list sub">
			<li>Live development twitch streams 5+ days a week</li>
			<li><a href="https://youtu.be/rW9ZsO6LYdk" target="_blank" rel="noopener noreferrer">Full game trailer</a>, with <a href="https://youtu.be/sfBsXX5rWfY" target="_blank" rel="noopener noreferrer">several</a> <a href="https://youtu.be/fkV4ea-P8Ic" target="_blank" rel="noopener noreferrer">teasers</a>: storyboarding, scripting, and video editing</li>
			<li>High engagement reddit posts: <a href="https://www.reddit.com/r/Simulated/comments/pekgaj/physarum_slime_mold_simulator_is_now_out_on_steam/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(1)</a> <a href="https://www.reddit.com/r/proceduralgeneration/comments/oo6suw/recently_announced_physarum_slime_mold_simulator/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(2)</a> <a href="https://www.reddit.com/r/proceduralgeneration/comments/pekbck/physarum_slime_mold_simulator_is_now_out_on_steam/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(3)</a></li>
			<li>Facebook ad, pro bono via a Facebook employee connection</li>
			<li>A marketing post mortem <a href="https://youtu.be/EsHigYW1Qb8" target="_blank" rel="noopener noreferrer">video</a></li>
		</ul>
    </li>
    <li>Customer support
        <ul class="highlights-list sub">
			<li>Personally responding to bug reports and questions about the product on Discord server, Steam Discussion forums, and live development streams</li>
			<li>Most user reported bugs fixed the day of report</li>
        </ul>
    </li>
    <li>Collaborated with a composer to create the <i>PHYSARUM</i> soundtrack and trailer score</li>
</ul>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>
> Watch the slime mold Physarum polycephalum grow in real time as you tweak and mutate its properties. Learn about the real life organism and discover different ways to manipulate its behavior. Encounter countless unique and organic looking patterns with a seemingly simple multi-agent chemoattractant system.

Discovery is a core theme for this game, there are no intrusive tutorials (see <a href="#learn" class="scrolly">3.5 Learn</a> for more details). The simulation starts immediately after the main menu; users are implicitly motivated by curiosity to discover the possibilities of the game. 

For example, the UI will appear when the cursor is placed in the left or right sections of the screen and clicking anywhere on the screen pushes or pulls (left and right click) the slimes. These kinds of user actions do not need to be explicitly told to the user, this passive design along with a calming soundtrack invites users to explore at their leisure.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-randomize.mp4" type="video/mp4">
  Randomize Video
</video>
*There is also a "Randomize" feature for instant dramatic results.*

<header id="customize" class="page-header"><h2><span class="number">3.1</span> Fully Customizable Simulation</h2></header>

Take full control of the simulation with a completely custom UI built in the Unity game engine. The game UI is compatible with any screen resolution/aspect ratio. Users can edit the simulation resolution/aspect ratio separately from the screen UI for a flexible simulation experience.  

<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>

The UI is designed to be as simplistic as possible to condense all the simulation parameters in an easy to read manner. Although possibly daunting at first, every UI element provide tooltips to emergently teach the user the purpose of every button and slider without being overwhelming.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-tooltip.mp4" type="video/mp4">
  Tooltip Video
</video>

<header id="game-modes" class="page-header"><h2><span class="number">3.2</span> Game Modes</h2></header>
Media can be uploaded/created to direct the slime mold into any shape or pattern. The media acts as a permanent chemoattractant in the background layer (i.e. environment) of the simulation. This means slime particles will prefer colors that match the background, allowing for more user experimentation. The different environmental background options are separated into "game modes":

<h4>Draw Mode</h4>
Draw environmental attractant using the mouse. Supports line drawing with arbitrary width and color and erasing.
<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-draw.mp4" type="video/mp4">
  Draw Video
</video>

<h4>Video/Image Mode</h4>
Upload image and/or video files to the game simply by copying them into a game folder. Images and videos can be rotated. Videos can be loaded into the simulation via URL if it is a direct path to a video file. There is also a basic playback UI with video scrubbing, pause/play, and muting.
<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-image-video.mp4" type="video/mp4">
  Video/Image Video
</video>

<h4>Webcam Mode</h4>
Lastly, users can interact with the slime mold simulation with a live video feed via webcam.
<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>
<!-- TODO: Webcam gif -->

<header id="morph" class="page-header"><h2><span class="number">3.3</span> Morph</h2></header>
The morph feature allows users to linearly interpolate between two user defined simulation states. This effectively make slime molds look like they are mutating and evolving into each other in real time.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-morph.mp4" type="video/mp4">
  Morph Video
</video>

<header id="share" class="page-header"><h2><span class="number">3.4</span> Share</h2></header>
Simulation sessions can be serialized at anytime with an export feature. Every parameter in the simulation can be encoded into an easily sharable string. These strings can be imported into *PHYSARUM: Slime Mold Simulator* running on another computer to obtain an identical simulation (initial conditions only, individual particle positions are not encoded). A custom encoder was implemented to ensure that these sharable codes are both backward compatible with previous versions of the game and culture-insensitive.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-share.mp4" type="video/mp4">
  Share Video
</video>

<div class="box" markdown="1">
*Development Anecdote:*\\
The custom encoder was not culture-insensitive on release, this caused import issues when codes were generated and imported in regions that use different decimal separators (i.e. 0.5 vs 0,5). This was promptly fixed after a user bug report was made. Lesson learned.
</div>

<header id="learn" class="page-header"><h2><span class="number">3.5</span> Learn</h2></header>
For users who are curious about the inner workings of the simulation or want to understand the slime particle parameters better, a detailed description is provided with an interactive slime particle visualizer.

<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-learn-1.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-learn-2.jpg %}" alt="" /></span></div> 
</div>

<header id="reception" class="major page-header"><h1><span class="number">4.</span> Reception</h1></header>
*PHYSARUM: Slime Mold Simulator* has sold 450+ units, with 13 Steam reviews (84% positive) as of August 2023. Although a very niche and small game, reception has been very positive. Master's students in AI, biology and engineering as well as fashion and graphic designers have reached out with questions about the software and permission to use it in their works (explicit permission is not needed!).

<header id="implementation" class="major page-header"><h1><span class="number">5.</span> Implementation</h1></header>
See below for some code examples and implementation details from the project. The slime agent algorithm was taken from <a href="https://uwe-repository.worktribe.com/output/980579" target="_blank" rel="noopener noreferrer">this paper</a> by Dr. Jeff Jones and the compute shader implementation is based on <a href="https://youtu.be/X-iSQQgOd1A?si=7pIOyvsba7aWwk_6" target="_blank" rel="noopener noreferrer">Sebastian Lague's video</a> and <a href="https://catlikecoding.com/unity/tutorials/basics/compute-shaders/" target="_blank" rel="noopener noreferrer">Catlike Coding's tutorial</a>.

<div class="box" markdown="1">
*Development Anecdote:*\\
An early alpha of *PHYSARUM: Slime Mold Simulator* was sent to Sebastian Lague and Dr. Jones before release. Both were very gracious and enjoyed the game. Dr. Jones was responsible for suggesting a periodic boundary feature and a scalable UI.
</div>

<header id="compute-shaders" class="page-header"><h2><span class="number">5.1</span> Compute Shaders</h2></header>
<!-- TODO: Show early sims, early compute shader stuff -->
<!-- TODO: drawing + slimes -->

<header id="tooltip" class="page-header"><h2><span class="number">5.2</span> Tooltip Framework</h2></header>
Text tooltips can be challenging because they must stay within a screen of any resolution/aspect ratio, while having an arbitrary width and height to fit text content. Additionally, we must account for scale of the UI element we are creating the tooltip from, this is because the game features a scalable UI. 

I used a solution I developed in a previous Unity project: use a reference UI resolution of 1920 x 1080 and fit arbitrary resolutions by height. The Unity <a href="https://docs.unity3d.com/Packages/com.unity.ugui@1.0/manual/script-CanvasScaler.html" target="_blank" rel="noopener noreferrer">canvas scaler</a> component does this by altering the scale of all UI objects. Which is why the "lossy scale" (i.e. the global scale: this includes the canvas scaler multiplier AND the scale multiplier from my scalable UI feature) is used to get a coefficient representing the aspect ratio difference between the run time screen and the reference resolution (line 13 of code snippet below). Using this method with the appropriate position anchors also allows the UI as a whole to work predictably with any screen size and aspect ratio.

<h4>Function used to position text tooltips of arbitrary size:</h4>
{% highlight csharp linenos %}
private IEnumerator CalculateTooltipPosition(RectTransform targetObjectRect, Vector2 customOffset) {
    LayoutRebuilder.ForceRebuildLayoutImmediate(tooltipRectTransform);
    yield return new WaitForEndOfFrame();

    float tooltipWidth = tooltipRectTransform.rect.size.x;
    float tooltipHeight = tooltipRectTransform.rect.size.y;

    float targetObjectWidth = targetObjectRect.rect.width * targetObjectRect.lossyScale.x;
    float targetObjectHeight = targetObjectRect.rect.height * targetObjectRect.lossyScale.y;

    // Scale positions and screen measurements with canvas scaler ratio
    // Note: make sure we use tooltip parent for UI scaling
    float aspectRatioScaling = 1 / tooltipRectTransform.parent.lossyScale.y;

    float scaledScreenHeight = Screen.height * aspectRatioScaling;
    float scaledScreenWidth = Screen.width * aspectRatioScaling;

    Vector3 scaledTargetObjectPosition = targetObjectRect.position * aspectRatioScaling;

    // above target object with padding
    float verticalAdjustOffset = (targetObjectHeight / 2f) + (tooltipHeight / 2f) + pixelPadding;
    // to the right of target object with padding
    float horizontalAdjustOffset = (tooltipWidth / 2f) + pixelPadding;

    // top edge of tooltip when it is above hovered object with padding
    float topTooltipY = scaledTargetObjectPosition.y + verticalAdjustOffset + tooltipHeight / 2f;

    // left and right edge of tooltip where middle of tooltip is centered on hoveredObject
    float leftTooltipX = scaledTargetObjectPosition.x - horizontalAdjustOffset;
    float rightTooltipX = scaledTargetObjectPosition.x + horizontalAdjustOffset;

    if (topTooltipY > scaledScreenHeight) {
        // flip tooltip to bottom
        verticalAdjustOffset = -verticalAdjustOffset;
    }

    if(leftTooltipX < 0f) {
        // if left side of tooltip goes past left side of screen,
        // nudge it to the right with padding
        horizontalAdjustOffset = -leftTooltipX + pixelPadding;
    }
    else if(rightTooltipX > scaledScreenWidth) {
        // flip tooltip to left side
        horizontalAdjustOffset = -horizontalAdjustOffset;
    }
    // no horizontal adjust needed
    else {
        horizontalAdjustOffset = 0f;
    }

    // Final tooltip position
    tooltipRectTransform.anchoredPosition = scaledTargetObjectPosition + new Vector3(horizontalAdjustOffset + customOffset.x, verticalAdjustOffset + customOffset.y);

    tooltipCanvasGroup.alpha = 1f;
}
{% endhighlight %}

<header class="page-header"><h3>Non-Text Tooltips</h3></header>
Menus like the color picker and "randomize settings" menu have a similar placement requirement of fitting within any screen size, but I used more ad hoc solutions. This reduced the need to make a overly robust (i.e. buggy) solution when simpler solutions work fine for the scope of this project.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-other-tooltip.mp4" type="video/mp4">
  Non-text Tooltips Video
</video>

For example, it is an invariant in the UI design that the color picker menu will always show on the right side of the color picker buttons. By default, color picker menus are always placed with the same horizontal offset from the button, with the top of the button flush with the top of the menu. Therefore, we only need to check if the bottom of the color picker goes lower than the bottom of the screen and adjust accordingly since color picker buttons are never above the screen.

<header id="color-picker" class="page-header"><h2><span class="number">5.3</span> Color Picker</h2></header>
Many UI elements are custom solutions built from scratch in Unity. One of the more complex elements is the color picker. My interface uses HSL color representation for intuitive color picking. Saturation and lightness is represented by the horizontal and vertical (respectively) 2D texture coordinates in the main color picking square; hue can be chosen in a vertical gradient on the side. RGB sliders with input boxes can also be used as an alternative. When one color representation value (i.e. HSL or RGB) is changed, the other color representation values and UI elements are updated in real time. 

The hue gradient and saturation/lightness square are rendered via uv coordinate interpolation and mouse coordinates are normalized, this means the color picker will work with any width and height without changing any code.

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/phys-color-picker.mp4" type="video/mp4">
  Color Picker Video
</video>

<h4>Saturation/Lightness Square Fragment Shader:</h4>
To render the color picker square, we use the uv values on the UI texture to calculate color values. This is done by linearly interpolating between the vertical uv value (Figure 1) and the vertical uv multiplied with the selected hue color (Figure 2, with red as selected hue), using the horizontal uv value. This results in a dynamic texture that is equivalent to showing all the saturation and lightness values, that can be colored with any hue (Figure 3).

<span class="image fit"><img src="{% link assets/images/color-picker-figures.png %}" alt="Color Picker Figures" /></span>

{% highlight hlsl linenos %}
fixed4 frag (v2f i) : SV_Target {
    fixed4 col = lerp(
        fixed4(i.uv.y, i.uv.y, i.uv.y, 1),
        fixed4(i.uv.y * i.color.x, i.uv.y * i.color.y, i.uv.y * i.color.z, 1),
        i.uv.x
    );
    col.a = i.color.a;
    return col;
}
{% endhighlight %}

*Note: i.color is the hue of the square, which is updated externally*

<h4>Hue Gradient Fragment Shader:</h4>
For the vertical hue selector, the vertical uv coordinates [0, 1] are scaled to hue values [0, 360]. The final HSL color is calculated using a formula found on <a href="https://en.wikipedia.org/wiki/HSL_and_HSV#HSL_to_RGB_alternative" target="_blank" rel="noopener noreferrer">wikipedia</a>, with locked S and L values.

{% highlight hlsl linenos %}
float HSL2RGB(float n, float H, float a, float L) {
    float k = fmod(n + (H / 30), 12);
    return L - a * max(-1, min(k - 3, min(9 - k, 1)));
}

fixed4 frag (v2f i) : SV_Target
{
    float H = i.uv.y * 360;
    float S = 1;
    float L = 0.5;

    float a = S * min(L, 1 - L);

    fixed4 col = fixed4(
        HSL2RGB(0, H, a, L),
        HSL2RGB(8, H, a, L),
        HSL2RGB(4, H, a, L),
        i.color.a
    );

    return col;
}
{% endhighlight %}

