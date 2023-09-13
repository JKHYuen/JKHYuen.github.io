---
layout: page
title: Last Secutor
permalink: /last-secutor
description: 2D Turn Based RPG with ARPG mechanics — an unfinished 7 year project where I experimented and honed my skills in game development and programming
image: assets/images/rpgDemo.gif
page-banner: assets/images/rpgDemo.gif
nav-menu: true

button-url: https://github.com/JKHYuen/BloomAttenuationBuild
button-text: Download Playable Demo

team-text: Solo Project, with help on 2D sprite art
date-text: 2015 — 2022
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly"><span class="number">1.</span> Overview</a></li>
    <li><a href="#highlights" class="button small scrolly"><span class="number">2.</span> Highlights</a></li>
    <li><a href="#features" class="button small scrolly"><span class="number">3.</span> Game Features</a></li>
    <li><a href="#implementation" class="button small scrolly"><span class="number">4.</span> Implementation</a></li>
</ul>
</div>

<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
*Last Secutor* is a 2D turn based RPG with ARPG mechanics such as an unique skill tree system, expansive loot, and complex character progression; inspired by games akin to *Path of Exile* and *Dragon Age: Origins*. The core gameplay loop is similar to the original *Diablo*:

<ul style="list-style: decimal">
    <li>Fight in a designated "dungeon" area</li>
    <li>Gain xp and resources</li>
    <li>Return to town</li>
    <li>Assign available skill points and spend resources</li>
    <li>Repeat</li>
</ul>
<!-- TODO: combat features interaction and positioning -->

<h4>Story Plans</h4>
The game had extensive plans for a story lead by a mysterious interdimensional cult: *The Unseen Adventists*; this powerful cult is known to invade and destroy every world they visit. The cultists' motivations remain unknown throughout the game, however they claim to have *seen* something that made them understand the universe. The player would visit the worlds, explore the town/fighting arena with a questline, and defeat the invading cult member to progress the story. The story explores themes of nihilism, morality, blind faith, and cosmological philosophy. Many of these concepts are inspired by lore from *Warhammer 40k*.

The cult represents a sci-fi interpretation of *<a href="https://en.wikipedia.org/wiki/Great_Filter" target="_blank" rel="noopener noreferrer">The Great Filter</a>*. Each world features a fatal societal flaw (e.g. the reliance on tradition, corrupt power segregation, etc.), introduced to the player by the cult leaders before it is destroyed. The story eventually leads to the discovery of the cult leader — an elder god existing between dimensions. Ultimately, the elder god will show that the player exists in one of an infinite set of parallel universes (in reference to other players), and that the cult followers' duty is to maintain the careful balance of energies at a cosmological scale.

<h4>Rapid High Level Development</h4>
Early in development, I decided to implement game systems in such a way that people with little to no programming experience could make content through the Unity GUI. This allows anyone to easily create new skill trees, skills, and enemies (See <a href="#" class="scrolly">Scriptable Objects</a> for full details). This was originally done as a programming challenge, but it was also motivated by the prospect of hiring/inviting others to work on the project. These implementations also allowed myself to quickly prototype and tweak existing game content.

<h4>An Unfinished Game</h4>
I worked on this game for 7 years — first 5 years while in university, and 2 years full time. Unfortunately the project was ultimately too ambitious and it was not financially viable to finish the game. I had only just started programming (Python, Java) when this project was created and had never made a game nor coded in C#. However, over these years I learned countless skills in game development, programming and design. 

Several of my projects (including my <a href="{{ site.baseurl }}/nothing-matters" target="_blank" rel="noopener noreferrer">two</a> <a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">games</a> released on Steam) use systems adapted from this project; such as serialization (user saves), shaders (e.g. procedural noise effects and material manipulation), UI that work on any resolution/aspect ratio, and a tooltip framework that positions tooltips of arbitrary sizes.