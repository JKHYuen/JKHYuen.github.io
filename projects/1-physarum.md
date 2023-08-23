---
layout: page
permalink: /physarum
title: "PHYSARUM: Slime Mold Simulator"
description: Interactive sandbox/visualizer of the real life organism <i>Physarum polycephalum</i>
image: assets/images/physarum.jpg
page-banner: assets/images/physarum-page-banner.jpg
nav-menu: true

button-icon: fa-steam
button-url: https://store.steampowered.com/app/1667120/PHYSARUM_Slime_Mold_Simulator/
button-text: Steam Store Page
team-text: Solo Project, with help from a composer for trailer and gameplay music
date-text: April 2021 - August 2021
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
    <li><a href="#implementation" class="button small scrolly"><span class="number">4.</span> Implementation</a></li>
</ul>
</div>

<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/rW9ZsO6LYdk" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>

<!-- TODO: mention first steam release -->
A project that evolved into a fully featured Steam release while learning how to make compute shaders. *PHYSARUM: Slime Mold Simulator* is an interactive sandbox visualizer of the real life organism *Physarum polycephalum*, all simulated on a single compute shader. The GPU bound AI easily allows for millions of slime agents (i.e. particles) to be simulated in real time.

Users can simulate an arbitrary amount of slime "species" and morph (lerp) between them to discover unique and mesmerizing organic patterns. Although not a traditional "game", *PHYSARUM: Slime Mold Simulator* is designed to encourage users to explore and discover in the sandbox environment for entertainment value. See trailer above for a full feature showcase. 

*Note: UI aesthetic design is not finalized in the trailer, see screenshots on <a href="https://store.steampowered.com/app/1667120/PHYSARUM_Slime_Mold_Simulator/" target="_blank" rel="noopener noreferrer">Steam</a> or below for the final UI look.*

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>

<ul class="highlights-list">
    <li>Simulation and UI implementation done in the Unity game engine, with the built-in renderer
        <ul class="highlights-list sub">
			<li>C# and Cg/HLSL programming</li>
            <li>Compute shaders, game logic and UI implementations coded solo from scratch, without plug-ins or store assets</li>
        </ul>
    </li>
    <li>UX/UI design
        <ul class="highlights-list sub">
			<li>UI designed and implemented with base Unity UI components</li>
            <li>Some icons used from <a href="https://kenney.nl/assets/game-icons" target="_blank" rel="noopener noreferrer">Kenney's game icons</a>, others are custom made</li>
        </ul>
    </li>
    <li>Zero budget marketing
        <ul class="highlights-list sub">
			<li>Live development twitch streams 5+ days a week</li>
			<li><a href="https://youtu.be/rW9ZsO6LYdk" target="_blank" rel="noopener noreferrer">Full game trailer</a>, with <a href="https://youtu.be/sfBsXX5rWfY" target="_blank" rel="noopener noreferrer">several</a> <a href="https://youtu.be/fkV4ea-P8Ic" target="_blank" rel="noopener noreferrer">teasers</a>: storyboarding, scripting, and video editing</li>
			<li>Successful reddit posts: <a href="https://www.reddit.com/r/Simulated/comments/pekgaj/physarum_slime_mold_simulator_is_now_out_on_steam/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(1)</a> <a href="https://www.reddit.com/r/proceduralgeneration/comments/oo6suw/recently_announced_physarum_slime_mold_simulator/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(2)</a> <a href="https://www.reddit.com/r/proceduralgeneration/comments/pekbck/physarum_slime_mold_simulator_is_now_out_on_steam/?utm_source=share&utm_medium=web2x&context=3" target="_blank" rel="noopener noreferrer">(3)</a></li>
			<li>Facebook Ad, funded by a Facebook employee connection</li>
			<li>A marketing post mortem <a href="https://youtu.be/EsHigYW1Qb8" target="_blank" rel="noopener noreferrer">video</a></li>
		</ul>
    </li>
    <li>Customer support
        <ul class="highlights-list sub">
			<li>Discord server: personally responding to bug reports and questions about the product</li>
			<li>Tech support on Steam discussion forums</li>
			<li>Answering questions about the product during live development streams</li>
			<li>Most user reported bugs fixed the day of report</li>
        </ul>
    </li>
    <li>Collaborated with composer to create the <i>PHYSARUM</i> soundtrack and trailer score</li>
</ul>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>
> Watch the slime mold Physarum polycephalum grow in real time as you tweak and mutate its properties. Learn about the real life organism and discover different ways to manipulate its behavior. Encounter countless unique and organic looking patterns with a seemingly simple multi-agent chemoattractant system.

Discovery is a core theme for this game, there are no intrusive tutorials (see <a href="#learn" class="scrolly">3.5 Learn</a> for more details). The simulation starts immediately after the main menu; users are implicitly motivated by curiosity to discover the possibilities of the game. 

For example, the UI will appear when the cursor is placed in the left or right sections of the screen and clicking anywhere on the screen pushes or pulls (left and right click) the slimes. These kinds of user actions do not need to be explicitly told to the user, this passive design along with a calming soundtrack invites users to explore at their leisure. There is also a "Randomize" button for instant dramatic results.

<!-- TODO: Randomize Gif -->

<header id="customize" class="page-header"><h2><span class="number">3.1</span> Fully Customizable Simulation</h2></header>

Take full control of the simulation with a completely custom UI built in the Unity game engine. The game UI is compatible with any screen resolution/aspect ratio. Users can edit the simulation resolution/aspect ratio separately from the screen UI for a flexible simulation experience.  

<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>

The UI is designed to be as simplistic as possible to condense all the simulation parameters in an easy to read manner. Although possibly daunting at first, every UI element provide tooltips to emergently teach the user the purpose of every button and slider without being overwhelming.

<!-- TODO: tooltip gif -->

<header id="game-modes" class="page-header"><h2><span class="number">3.2</span> Game Modes</h2></header>
Media can be uploaded/created to direct the slime mold into any shape or pattern. The media acts as a permanent chemoattractant in the background layer (i.e. environment) of the simulation. This means slime particles will prefer colors that match the background, allowing for more user experimentation. The different environmental background options are separated into "game modes":

<h4>Draw Mode</h4>
Draw environmental attractant using the mouse. Supports line drawing with arbitrary width and color and erasing.
<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>

<!-- TODO: draw gif -->

<h4>Video/Image Mode</h4>
Upload image and/or video files to the game simply by copying them into a game folder. Images and videos can be rotated. Videos can be loaded into the simulation via URL if it is a direct path to a video file. There is also a basic playback UI with video scrubbing, pause/play, and muting.
<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>

<!-- TODO: video/image gif -->

<h4>Webcam Mode</h4>
Lastly, users can interact with the slime mold simulation with a live video feed via webcam.
<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-ui.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-limits.jpg %}" alt="" /></span></div>
</div>
<!-- TODO: Webcam gif -->

<header id="morph" class="page-header"><h2><span class="number">3.3</span> Morph</h2></header>

<!-- TODO: morph gif -->
<video muted controls poster="{{ site.baseurl }}/assets/images/physarum.jpg">
  <source src="{{ site.baseurl }}/assets/videos/phys-preview.mp4" type="video/mp4">
  morph video
</video>

The morph feature allows users to linearly interpolate between two simulation states. This effectively make slime molds look like they are mutating and evolving into each other in real time.

<header id="share" class="page-header"><h2><span class="number">3.4</span> Share</h2></header>
Simulation sessions can be serialized at anytime with an export feature. Every parameter in the simulation can be encoded into an easily sharable string. These strings can be imported into *PHYSARUM: Slime Mold Simulator* running on another computer to obtain an identical simulation (initial conditions only, individual particle positions are not encoded). A custom encoder was implemented to ensure that these sharable codes are both backward compatible with previous versions of the game and culture-insensitive.

<div class="box" markdown="1">
*Development Anecdote:*\\
The custom encoder was not culture-insensitive on release, this caused import issues when codes were generated and imported in regions that use different decimal separators (i.e. 0.5 vs 0,5). This was promptly fixed after a user bug report was made. Lesson learned.
</div>

<!-- TODO: share gif -->

<header id="learn" class="page-header"><h2><span class="number">3.5</span> Learn</h2></header>
For users who are curious about the inner workings of the simulation or want to understand the slime particle parameters better, a detailed description is provided with an interactive slime particle visualizer.

<div class="row">
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-learn-1.jpg %}" alt="" /></span></div>
<div class="6u"><span class="image fit"><img src="{% link assets/images/phys-learn-2.jpg %}" alt="" /></span></div> 
</div>

<header id="implementation" class="major page-header"><h1><span class="number">4.</span> Implementation</h1></header>

<!-- color picker, tooltip for all resolutions, compute shader - slime + drawing,  https://uwe-repository.worktribe.com/output/980579 -->

