---
layout: page
title: nothing_matters
permalink: /nothing-matters
description: My latest released project — An experimental point & click narrative game inspired by my indie game dev career
image: assets/images/nothing_matters.png
page-banner: assets/images/nothing_matters.png
nav-menu: true

button-url: https://store.steampowered.com/app/2260800?utm_source=portfolio
button-text: Steam Store Page
button-icon: fa-steam

date-text: April 2022 — June 2023
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly"><span class="number">1.</span> Overview</a></li>
    <li><a href="#highlights" class="button small scrolly"><span class="number">2.</span> Highlights</a></li>
    <li><a href="#features" class="button small scrolly"><span class="number">3.</span> Game Features</a></li>
    <li><a href="#reception" class="button small scrolly"><span class="number">4.</span> Reception</a></li>
    <li><a href="#implementation" class="button small scrolly"><span class="number">5.</span> Implementation</a></li>
</ul>
</div>

<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/WrdCmBp1qac?si=mJD0HdX9wxjQm4lj" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>

<b class="alert">NOTE: This game is best experienced with as little knowledge as possible (see store page). If you are interested in this project, I highly recommend playing through the game (available for <a href="https://store.steampowered.com/app/2260800?utm_source=portfolio" target="_blank"  rel="noopener noreferrer">free on Steam</a>, ~1.2 hours in length) before reading the full details below to get the intended experience.</b>

"<i>nothing_matters</i>" is an experimental narrative game inspired by my personal experience as an indie developer. This game features three different sections with escalating complexity, each with distinct visual design and gameplay. The game is primarily a point & click adventure accompanied by minigames; a short experience designed to be played in one session (~1.2 hours, checkpoint saves available). Although not intended to be a horror game, *nothing_matters* features unsettling and disturbing gameplay elements based in realism.

Many aspects of <i>nothing_matters</i> are kept abstract by design. Players are encouraged to make there own interpretations of the experience. However, for the sake of this portfolio page, this is what I had in mind before and during development:

<blockquote style="margin: -1.5em 0 2em 0;">"<i>nothing_matters</i>" is a nihilistic juxtaposition of the games industry (in the perspective of both developers and players) and modern consumer capitalism. This concept is conveyed through satirical gameplay such as patronizing tutorials and overdesigned UI elements. The core theme of hyper production and consumerism is set in an exaggerated dystopian world to explore how/if art fits into a futuristic bureaucratic technocracy. I also wanted to highlight the mundanity of the creative process as it is often glorified as a strictly enjoyable and linear procedure.</blockquote>

My main goal for this project is to stylistically simulate the experience of being an artist, in hopes to resonate with both creative and non-creative audiences. **Ultimately, the game's message is intended to be positive and encourage artists to keep creating despite any inhibitive obstacles outside of their control.**
 
 <!-- TODO: link "overdesigned UI elements" -->
 <!-- TODO: add screenshots above to break paragraphs -->
 
<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>Fully featured narrative game released on <a href="https://store.steampowered.com/app/2260800?utm_source=portfolio" target="_blank"  rel="noopener noreferrer">Steam</a>, developed completely solo on Unity (Built-in Renderer)
        <ul class="highlights-list sub">
            <li>Released for free to reach as many people as possible</li>
            <li>"Very Positive" <a href="#reception" class="scrolly">Steam reviews</a> (159 reviews, 86% positive) as of October 2023</li>
            <li><a href="#end-game" class="scrolly">Steam achievements</a> implemented to guide players to all the game's hidden content (Using <a href="https://github.com/rlabrecque/Steamworks.NET" target="_blank"  rel="noopener noreferrer">Steamworks.NET</a>)</li>
            <li>Total of 40 USD spent for game assets (all for 3D models in the FPS section)</li>
            <li>Communication with users to quickly fix bugs post release</li>
        </ul>
    </li>
    <li>Scripted, storyboarded, edited, and voice acted for <a href="#video" class="scrolly">game reveal trailer</a>
        <ul class="highlights-list sub">
            <li>Reveal trailer was made as an interactive scene in Unity to save time in editing</li>
        </ul>
    </li>
    <li>Extensive writing done to create an original fictional world 
        <ul class="highlights-list sub">
            <li>Set in a near-future hypercapitalistic technocracy, where the world has combined into a single "Unified Earth State"</li>
            <li>Story contains themes of evolution, creativity, choice, and the human condition</li>
            <li>Over 23,500+ words of written content and dialogue (approximate word count only includes Part II)</li>
            <li>Parallel plot written in the form of 136 fictional "MalNews" articles (Part II) in a writing style that mimics sensationalized news media</li>
            <li>41 "Wax" documents written for further world building</li>
        </ul>
    </li>
    <li>Comprehensive <a href="#shaders" class="scrolly">HLSL shader and technical art work</a> done to create contrasting and varied visual styles:
        <ul class="highlights-list sub">
            <li>Graphics design work to create custom icons</li>
        </ul>
    </li>
    <li>Scripted, filmed, and acted in 4 short real life videos as in-universe game content</li>
    <li><a href="#part-I" class="scrolly">Part I: Retro</a>
        <ul class="highlights-list sub">
            <li>An ironic commentary on the societal gamification of life</li>
            <li>Satirical, over the top writing style</li>
            <li>Retro scanline and glow post processing effect with glitch effects</li>
            <li>3 distinct minigames: "<i>Flip the Coin</i>", "<i>Game of Life</i>" and "<i>Ping</i>"</li>
        </ul>
    </li>
    <li><a href="#part-II" class="scrolly">Part II: MalusOS</a>
        <ul class="highlights-list sub">
            <li>Detailed functional OS UI (window management, draggable desktop icons, task bars, etc.)</li>
            <li>A more realistic and subtle writing style in contrast with Part I</li>
            <li>"<i>War Game</i>" minigame - a more complex version of Rock Paper Scissors</li>
            <li>Usable OS Apps for emergent story telling, each with it's own UI design</li>
            <li>Polished UI, with some animations ironically overdesigned with clinical visuals to imitate modern UX/UI tropes</li>
        </ul>
    </li>
    <li><a href="#part-III" class="scrolly">Part III: "9-5" FPS</a>
        <ul class="highlights-list sub">
            <li>Fully featured 3D first person shooter</li>
            <li>PBR graphics with baked and dynamic lighting</li>
            <li>Intended to be a surprise climax to the game, absent from marketing material</li>
            <li>Custom FPS movement controller (improved version from my <a href="{{ site.baseurl }}/bloom-attenuation" target="_blank" rel="noopener noreferrer">Bloom Attenuation project</a>)</li>
            <li>Custom bullet shooting and physics solution (see <a href="#fps-mechanics" class="scrolly" >5.2 FPS Mechanics</a> for full details)</li>
        </ul>
    </li>
</ul>

<div class="box" markdown="1">
*Some Context:*\\
I consider this game experimental because it does not contain the usual gameplay elements most players would expect. I have always thought of video games as an artform and wanted to push the limits of how it can be implemented. Although abstract metacommentary is not uncommon in indie games (some would consider it a trope), I wanted to attempt to make a complete game without an explicit goal, gameplay loop, nor concept of winning and losing (**see my other projects for more conventional game examples**). 

This was partially motivated by the end of a <a href="{{ site.baseurl }}/last-secutor" target="_blank" rel="noopener noreferrer">multiyear project</a> as I wanted to make something a little different. I expected this concept to be polarizing and hard to market so I decided to release the game for free and keep the game time short to ease the barrier of entry.
</div>

 <!-- TODO: link "OS Apps", Part titles, achievements -->

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>  
The multiple parts of the game is designed to keep the localized gameplay elements fresh and diverse. Each part is more complex than the last to create a sense of escalation and unpredictability. These parts are not only intended to build an evolving story, but also serves as variations of the game's themes and concepts.

Once again, I highly encourage anyone interested in this project to experience it firsthand (<a href="https://store.steampowered.com/app/2260800?utm_source=portfolio" target="_blank"  rel="noopener noreferrer">play for free on Steam</a>), however, a full walkthrough is available <a href="https://youtu.be/rh0NU1ry-d4?si=blWfa3repXAIAcCt" target="_blank" rel="noopener noreferrer">here</a> (thanks to Youtuber *AlphaBetaGamer*) if you would like to view footage of the following gameplay sections. *Note: the walkthrough video contains occasional zoomed visuals and music additions not present in the original game.* 

<div class="box" markdown="1">
*Development Anecdote:*\\
As a fan of the channel and a way to market the game, I contacted <i>AlphaBetaGamer</i> to see if they would be interested in showcasing my game on the channel as *nothing_matters* seemed to fit the kind of games they tend to make videos on. To my surprise, they responded by saying they found my game organically and are already editing their completed playthrough footage.
</div>

<!-- TODO: Add screenshots minigames, showing post processing and glitches -->
<header id="part-I" class="page-header"><h2><span class="number">3.1</span> Part I: Retro</h2></header>
The game starts with a low fidelity aesthetic and aggressive writing style set a tone that contrasts the following parts of the game. The distinctive retro visuals are created with custom post processing involving fake procedural scan lines, uv displacements and bloom based illumination (see <a href="#implementation" class="scrolly">5. Implementation</a> for full details). Each minigame starts as a simple concept and evolves with more gameplay mechanics.

<img class="image center" src="{% link assets/images/nm-quote.jpg %}" alt="Quote Screenshot"/>
<em style="width: 100%;">Introductory quote when player starts the game.</em>

<div class="box" markdown="1">
*Development Anecdote:*\\
Early in development, a quote was chosen to set the tone of the game in the introduction from <a href="https://en.wikipedia.org/wiki/The_Denial_of_Death" target="_blank" rel="noopener noreferrer">The Denial of Death</a> by Ernest Becker (1973), one of the inspirations for this game:
<blockquote style="margin: -1.5em 0 0.5em 0;">"..in order to turn out a piece of work the author has to exaggerate the emphasis of it,<br>to oppose it in a forcefully competitive way to other versions of the truth.."</blockquote>
And completing the quote after the "*Flip the Coin*" section: 
<blockquote style="margin: -1.5em 0 0.5em 0;">"and he gets carried away by his own exaggeration, as his distinctive image is built on it."</blockquote>
Unfortunately, I could not negotiate the rights to use the quote from *Simon & Schuster* as I was informed they "do not license content to individuals". I settled by writing an original diegetic quote.
</div>

<h4>Flip the Coin</h4>
A deconstruction of what a game is, starting with only the bare essentials: a "play" button that indicates whether the player has won or loss.

<h4>Game of Life</h4>
A simple puzzle/guessing game using a real time implementation of <a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life" target="_blank" rel="noopener noreferrer">Conway's Game of Life</a>.

<div class="box" markdown="1">
*Development Anecdote:*\\
A classic and embarrassing case of premature optimization: This minigame was implemented early in the game's development. So with seemingly abundant time and excitement of a new project, I decided to use this opportunity to learn multi-threading in Unity; using the novel Unity <a href="https://docs.unity3d.com/Manual/JobSystemOverview.html" target="_blank" rel="noopener noreferrer">Jobs system</a> and <a href="https://docs.unity3d.com/Packages/com.unity.burst@1.2/manual/index.html" target="_blank" rel="noopener noreferrer">Burst compiler</a>. This was encouraged by slowdowns happening with bigger Game of Life simulation grids.

A day of converting everything into value types later, the multi-threaded simulation seems to be working. However, no performance difference. Turns out the slowdown was primarily caused by redraws in the UI system whenever a grid element is updated (the entirety of Part I and II is implemented in the UI system to easily accommodate for all screen sizes). I ended up simply using slightly smaller grid sizes in the later parts of this section. Lesson once again learned.
</div>

<h4>Ping</h4> 
A detailed clone of the original Pong. Evolves into a pseudo multiplayer game (bots with game and chat AI). Name of the game and creator Al Alcorn slightly altered to avoid copyright issues.

<header id="part-II" class="page-header"><h2><span class="number">3.2</span> Part II: MalusOS</h2></header>
<!-- TODO: "FLIP FLOP", show apps, writing examples, acronym lore list -->
Part II is the largest part of the game, MalusOS is an elaborate implementation of a fictional OS set in the game's universe.

<header id="part-III" class="page-header"><h2><span class="number">3.3</span> Part III: "9-5" FPS</h2></header>
A surprise 3D section of the game. Comprehensive first person shooter featuring movement mechanics (e.g. jump, crouch, sprint with stamina bar), gun mechanics (e.g. recoil, ADS, and reloading) and realistic PBR graphics with baked/dynamic lighting, decals, physics enabled ragdolls and detailed blood effects. This section is designed to be an cathartic and action packed crowd pleaser after going though a largely conceptual experience. 

<div class="box" markdown="1">
*Development Anecdote:*\\
As a developer who has primarily made 2D projects, I took this opportunity to challenge myself and learn to create a FPS for the first time. Although a large part of the implementation is easily transferrable from 2D as expected (general work with quaternions and position vectors); dynamic decals, first person bullet visuals, and lighting took some time to figure out, see <a href="#fps-mechanics" class="scrolly">5.2 FPS Mechanics</a> for details.

*Bonus trivia: a subtle upward <a href="https://en.wikipedia.org/wiki/Shepard_tone" target="_blank" rel="noopener noreferrer">Shepard tone</a> (inspired by Hans Zimmer) loops throughout the FPS section to represent the theme of survival and capitalistic growth.*
</div>

<header id="end-game" class="page-header"><h2><span class="number">3.4</span> End Game / Achievements</h2></header>
Although this game is designed to be completed in one sitting, bonus features and secrets are added for players who want to explore the world further. After the game is completed, a sandbox version of Part II and Part III will be unlocked, accessible from the main menu. Players can take as long as they need to read all the written content in *MalusOS* and play a survival version of the FPS.

<!-- TODO: Show end game main menu -->

I decided early in development that this game would be a good opportunity for me to learn how to implement Steam achievements, as well as using it as a game mechanic to guide and encourage users to find all the secret/bonus content I spent time making. This worked very well as players are seen discussing achievement hunting in the game's Discord channel and in the Steam discussion page. This effect is reinforced by an <a href="https://steamcommunity.com/sharedfiles/filedetails/?id=2998648664" target="_blank" rel="noopener noreferrer">achievement guide</a> that a player spent time making.

<!-- TODO: show achievements -->

The end game features are designed to provide players with additional content and a method to obtain all the achievements without playing through the whole game again (2 missable achievements in Part I can be obtained by starting a new game and playing a few minutes).

<header id="reception" class="major page-header"><h1><span class="number">4.</span> Reception</h1></header>
<img class="image center" src="{% link assets/images/nm-reviews.jpg %}" alt="Reviews Screenshot"/>

<!-- TODO: youtube videos, horrors, reviews -->

<header id="implementation" class="major page-header"><h1><span class="number">5.</span> Implementation</h1></header>

<header id="shaders" class="page-header"><h2><span class="number">5.1</span> Shader Effects</h2></header>

<!-- TODO: glitch effect -->

<h4>Custom Post Processing Fragment Shader</h4>
{% highlight hlsl linenos %}
fixed4 frag (v2f i) : SV_Target {
    // for screen scroll as another "glitched" effect
    i.uv.y += _UV_Y_Offset;

    // Scanlines
    fixed4 scanLine1 = frac((i.uv.y + _Time.x * _ScanlineSpeed) * _ScanlineCount);
    fixed4 scanLine2 = frac((i.wPos.y + _Time.x * 0.5 * _ScanlineSpeed) * _ScanlineCount2);

    fixed4 scanLines = scanLine1 * scanLine2 * _ScanLineTint;

    // uv distortion by scanlines
    i.uv += 0.01 * scanLines * _ScanLineUVStrength; 

    // Chromatic Aberration
    fixed s = 0.001 * (_ChromaticAberrationAmount + scanLines * 2);
    fixed r = tex2D(_MainTex, i.uv + fixed2(+s, +s)).r;
    fixed g = tex2D(_MainTex, i.uv + fixed2(+s, -s)).g;
    fixed b = tex2D(_MainTex, i.uv + fixed2(-s, -s)).b;
    fixed4 col = tex2D(_MainTex, i.uv);
    fixed4 aberratedColor = fixed4(r, g, b, col.a);

    // Luminance threshold for scanline visibility
    fixed4 originalColor = tex2D(_MainTex, i.uv);
    float luminance = (0.2126f * originalColor.r + 0.7152f * originalColor.g + 0.0722f * originalColor.b);

    fixed4 finalColor = aberratedColor + (scanLines * luminance * _ScanLineVisibility * (1 - aberratedColor.a));
    return finalColor;
}
{% endhighlight %}

<header id="fps-mechanics" class="page-header"><h2><span class="number">5.2</span> FPS Mechanics</h2></header>

<header id="ui-framework" class="page-header"><h2><span class="number">5.3</span> UI Framework</h2></header>
