---
layout: page
title: Last Secutor
permalink: /last-secutor
description: 2D Turn Based RPG — an unfinished 8 year project where I experimented and honed my skills in game development and programming
image: assets/images/rpgDemo.gif
page-banner: assets/images/rpgDemo.gif
nav-menu: true

button-url: https://github.com/JKHYuen/BloomAttenuationBuild
button-text: Download Playable Demo

team-text: Solo Project, with help on 2D sprite art
date-text: 2014 — 2022
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
*Last Secutor* is a 2D turn based RPG with ARPG mechanics such as an original skill tree system, expansive loot, and complex character progression; inspired by games akin to *Path of Exile* and *Dragon Age: Origins*. The core gameplay loop is similar to the original *Diablo*:

<ul style="list-style: decimal">
    <li>Fight in a designated "dungeon" area</li>
    <li>Gain xp and resources</li>
    <li>Return to town</li>
    <li>Assign available skill points and spend resources</li>
    <li>Repeat</li>
</ul>

<!-- TODO: combat features interaction and positioning, some video -->

<h4>An Unfinished Game</h4>
I worked on this game for 8 years — first 6 years while in university, and 2 years full time. Unfortunately the project was ultimately too ambitious and it was not financially viable to finish the game. I had only been programming for about a year (Python/Java/C#) when I started developing *Last Secutor* and this was the first project I made without following tutorials. This project eventually became an invaluable learning tool I used to teach myself game development. I learned to be autodidactic by always attempting to code things as low-level as possible, rather than using plugins or online solutions. This taught me to build arbitrary game mechanics without outside help (other than documentation). 

<!-- TODO: 2015 phone video -->

I experimented a lot over the years and learned to code common game systems from scratch, many of the implementations in *Last Secutor* have been completely rewritten multiple times. This experience allowed me to quickly develop improved versions for my future projects by avoiding implementation pitfalls (i.e. weighing the pros and cons of different implementations I've tried in the past), improving object-oriented design, and adapting to the unique requirements of each project. 

Several of my projects (including my <a href="{{ site.baseurl }}/nothing-matters" target="_blank" rel="noopener noreferrer">two</a> <a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">games</a> released on Steam) use improved systems that were first developed in this project; such as serialization (user saves), shaders (e.g. procedural texture effects and material manipulation), UI that works on any resolution/aspect ratio, and a tooltip framework that positions tooltips of arbitrary sizes. 

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>8 years of RPG game development experience (6 years part time, 2 years full time)
        <ul class="highlights-list sub">
            <li>Although this game is unfinished, systems used in my <a href="{{ site.baseurl }}/nothing-matters" target="_blank" rel="noopener noreferrer">released</a> <a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">games</a> are based off of implementations developed in this project</li> 
            <li>See <a href="#implementation" class="scrolly">4. Implementation</a> for some code examples of game features that have been implemented</li> 
        </ul>
    </li>
    <li>Created in the Unity engine. All game features, shaders and systems coded and designed <i>by myself</i> with no additional plugins or frameworks with two exceptions:
        <ul class="highlights-list sub">
            <li>Anima2D (<a href="https://forum.unity.com/threads/discontinuing-anima2d-consider-2d-animation-for-skeletal-animation-in-unity.1037605/" target="_blank" rel="noopener noreferrer">now a base feature in Unity</a>) for 2D skinned mesh animations</li>
            <li><a href="https://github.com/Siccity/xNode" target="_blank" rel="noopener noreferrer">xNode</a>: a low level framework to render interactable graphs in the Unity editor (used to easily create skill, dialogue, and quest trees within the Unity GUI)</li>
        </ul>
    </li>
    <li>Game systems implemented in a way that allows for <a href="#rapid-development" class="scrolly">rapid high level development</a>
        <ul class="highlights-list sub">
            <li>Allows developers with no programming experience to easily create and tweak game content through the Unity editor</li>
        </ul>
    </li>
    <li>2D Turn based combat that encourages methodical gameplay
        <ul class="highlights-list sub">
            <li>Tile movement in combat for position management with a variety of skills that can push, pull, and trap characters</li>
            <li>A <a href="#reactions" class="scrolly">reaction</a> system that allows players to queue actions that can trigger during an opponents turn if the reaction skill's conditions are met</li>
            <li>Traditional RPG mechanics such as damage resistance, armor, dodge, status effects, mana/stamina costs, summons, stuns, healing and back hits</li>
        </ul>
    </li>
    <li>Original "build your own" <a href="#skill-tree" class="scrolly">skill tree mechanic</a></li>
    <li>RPG systems coded from scratch with C# including but not limited to:
        <ul class="highlights-list sub">
            <li>Grid based inventory/stash supporting items of any size, with serialization support for player saves</li>
            <li>Equipment slots that alter player sprite's look</li>
            <li>System to manage multi-layered character effects (i.e. freezing, fire, bloody, etc.), custom shaders written from scratch in HLSL</li>
            <li>Character stat system, that interacts with equipped items, buffs/debuffs, and skill trees during gameplay</li>
            <li>AI framework built with Unity coroutines, to create arbitrary enemy behaviors in the game's 2D turn based combat system (example AI with different combat styles is shown in playable demo)</li>
            <li>Custom RPG UI featuring compare tooltips, draggable skill tree windows, character sheets, a game glossary with searchable key words, a quest journal, a combat log, and skill bars</li>
            <li>Quest and dialogue system</li>
            <li>Item rewards with randomized, tiered and categorized stat affixes</li>
            <li>Skill, dialogue and quest tree framework that allows trees (technically mathematical graphs) to be built without code, using the Unity editor</li>
            <li>2D turn based (discrete tile movement) controls in combat and real time point and click continuous movement controls in town</li>
            <li>Modular skill system with custom shader effects using <a href="https://docs.unity3d.com/Manual/class-ScriptableObject.html" target="_blank" rel="noopener noreferrer">Unity scriptable objects</a>, allowing for any skill attribute (e.g. damage ranges, crit chance, projectile style, buff/debuff application, etc.) to be tweaked easily</li>
        </ul>
    </li>
</ul>

<b style="font-size:18pt; color:#ff9587;">NOTE: I could not include every detail for this multi-year project. If you have any questions or want to discuss any other aspects or implementations from this project feel free to <a href="#contact" class="scrolly">contact me!</a></b>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>

<header id="skill-tree" class="page-header"><h2><span class="number">3.1</span> Unique Skill Tree System</h2></header>
The core mechanic of character progression is the unique skill tree system. *Last Secutor*'s skill tree is comprised of 4 swappable subtrees. Subtrees have outer "transition nodes" that allows players to connect to an adjacent subtree. Like other RPGs, players will gain a skill point when leveling to assign to their skill tree. Assigned nodes must have a path to at least one of the subtree's root node.

<!-- TODO: demonstration video with narration -->

The intent of this skill tree design is to encourage players to experiment with subtrees that are compatible with their builds; while also trying to find the optimal path (least amount of skill points) to the desired skill tree nodes. Nodes are generally more powerful/desirable the farther they are from the subtree root nodes. This rewards players for interacting with the transition nodes mechanic to efficiently reach more powerful nodes in adjacent trees.

<!-- TODO: Combat positioning/effects - Combat Log -->
<header id="combat" class="page-header"><h2><span class="number">3.2</span> 2D Turn Based Combat</h2></header>
During a combat turn, Players and NPCs will take turns performing actions until they run out of resources.  

<h4 id="reactions">Reactions</h4>

<h4>Skills</h4>
Although not completely finished, many skills were designed to encourage combinations and deliberate positioning.

<!-- TODO: show knife throw skill -->
<!-- TODO: show marker skill -->

<header id="itemization" class="page-header"><h2><span class="number">3.3</span> RPG Itemization and Stats</h2></header>


<header id="story-plans" class="page-header"><h2><span class="number">3.4</span> Story Plans</h2></header>
The game had extensive plans for a story lead by a mysterious interdimensional cult: *The Unseen Adventists*; a cult comprised of powerful members known to invade and destroy every world they visit. The cultists' motivations remain unknown throughout the game, however they claim to have *seen* something that allowed them to understand the nature of the universe. 

The player will visit the worlds, explore the town/fighting arena with individual questlines, and defeat the invading cult member to progress the story. The story explores themes of nihilism, morality, blind faith, and cosmological philosophy. Many of these concepts are inspired by lore from *Warhammer 40k*.

The cult represents a sci-fi interpretation of *<a href="https://en.wikipedia.org/wiki/Great_Filter" target="_blank" rel="noopener noreferrer">The Great Filter</a>*. Each world features a fatal societal flaw (e.g. overreliance of tradition, corrupt power segregation, etc.), introduced to the player by the invading cult members. The story eventually leads to the discovery of the cult leader — an ancient god-like being that exists between dimensions. Ultimately, the ancient god will show that the player exists in one of an infinite set of parallel universes (in reference to other players), and that the cult's duty is to maintain the careful balance of energies at a cosmological scale.

<!-- TODO: Inventory, Scriptable Objects / database - Use skill as example -->
<header id="implementation" class="major page-header"><h1><span class="number">4.</span> Implementation</h1></header>

<header id="scriptable-objects" class="page-header"><h2><span class="number">4.1</span> Scriptable Objects</h2></header>
<h4 id="rapid-development">Rapid High Level Development</h4>
Early in development, I decided to implement game systems in such a way that people with no programming experience could make content through the Unity GUI. This allows anyone to easily create new skill trees, skills, and enemies (See <a href="#place-holder" class="scrolly">Scriptable Objects</a> for full details). This was originally done as a programming challenge, but it was also motivated by the prospect of hiring/inviting others to work on the project. These implementations also allowed myself to quickly prototype and tweak existing game content.

<header id="content-graphs" class="page-header"><h2><span class="number">4.2</span> Content Graph Building</h2></header>


<header id="shaders" class="page-header"><h2><span class="number">4.3</span> Custom Shader Effects</h2></header>
<!-- TODO: character material stack -->
As a solo programmer with no experience hand drawing 2D illustrations, obtaining art assets are often a road block in game development. At first, I used shaders found online to easily add visual flair at first, but this quickly became a hinderance as I could not make specific effects to my liking.

I soon decided (~2015) the best way to move forward was to learn how to write low-level HLSL shaders myself to create whatever effect I needed. Although daunting at first, this was one of the most valuable skills I learned from this project. This not only allowed me to create countless custom effects in my future projects, but also allowed me to work on my projects without the need to hire other artists. 

I focused on learning to writing shaders in HLSL as opposed to using popular visual programming (i.e. Shader Graph) solutions because I wanted to learn a skill that would be easily transferrable to other engines/frameworks (including other shader graphs).

<header id="inventory" class="page-header"><h2><span class="number">4.4</span> Inventory</h2></header>
The grid based inventory was one of the most tricky game systems to implement. As a challenge, I wanted to replicate *Path of Exile*'s inventory UI functionality exactly. 

After an initial attempt with assumptions of how the UI worked, things felt different and less comfortable. This lead to a realization I never noticed while playing the game — which is that the grid highlighting (when hovering over grid space with an item on cursor) does not update when the cursor crosses a border of a grid square, but rather, when it crosses a **midpoint** of a grid square. To my surprise, this non-trivial difference makes a very noticeable difference to the look and feel of the inventory system.

{% highlight csharp linenos %}
private void UpdateHighlightData() {
    if (isPointerInContainer && inventory.cursorItem) {
        Vector2 pointerLocalPos;
        RectTransformUtility.ScreenPointToLocalPointInRectangle((RectTransform)transform, Input.mousePosition, null, out pointerLocalPos);

        // Index of mouse position in grid of all half squares in inventory
        int[] halfSquareIndex = new int[2];

        // Check if mouse is at the first or second half of container
        if (pointerLocalPos[1] < 0) {
            halfSquareIndex[0] = 2 * position[0] + 1;
        }
        if (pointerLocalPos[1] >= 0) {
            halfSquareIndex[0] = 2 * position[0];
        }

        if (pointerLocalPos[0] > 0) {
            halfSquareIndex[1] = 2 * position[1] + 1;

        }
        if (pointerLocalPos[0] <= 0) {
            halfSquareIndex[1] = 2 * position[1];
        }

        inventory.cursorItem.ResetHighlighted();
        inventory.ResetHighlighted();

        HighlightCalc(halfSquareIndex);
    }
}
{% endhighlight %}


{% highlight csharp linenos %}
private void HighlightCalc(int[] halfSquareIndex) {
    // Change inventory size to 0-index
    int[] inventorySize = new int[] { storage.inventorySize[0] - 1, storage.inventorySize[1] - 1 };

    /// Vertical Calc
    if (itemSize[0] == 1) {
        y = position[0];
    }
    else {
        bool inTopVerticalBorder = halfSquareIndex[0] <= itemSize[0];
        bool inBottomVerticalBorder = halfSquareIndex[0] >= (2 * inventorySize[0] + 1) - itemSize[0];
        // if we are IN the vertical borders
        if (inTopVerticalBorder || inBottomVerticalBorder) {
            if(inTopVerticalBorder) {
                y = 0;
            }
            if (inBottomVerticalBorder) {
                y = inventorySize[0] - itemSize[0] + 1;
            }
        }
        // OUT of vertical border
        else {
            // Vertical index we want moves every 2 half squares: 
            // find nearest multiple of 2 to the half square index (not including top border) to figure out final index
            y = FindNearestMultipleOfTwo(halfSquareIndex[0] - itemSize[0]) / 2;

        }
    }

    /// Horizontal Calc
    if (itemSize[1] == 1) {
        x = position[1];
    }
    else {
        bool inLeftHorizontalBorder = halfSquareIndex[1] <= itemSize[1];
        bool inRightHorizontalBorder = halfSquareIndex[1] >= (2 * inventorySize[1] + 1) - itemSize[1];
        // if we are IN the horizontal borders
        if (inLeftHorizontalBorder || inRightHorizontalBorder) {
            if (inLeftHorizontalBorder) {
                x = 0;
            }
            if (inRightHorizontalBorder) {
                x = inventorySize[1] - itemSize[1] + 1;
            }
        }
        // OUT of vertical border
        else {
            // Horizontal index we want moves every 2 half squares: 
            // find nearest multiple of 2 to the half square index (not including left border) to figure out final index
            x = FindNearestMultipleOfTwo(halfSquareIndex[1] - itemSize[1]) / 2;
        }
    }

    // Highlight item size with upper left corner (x,y) in inventory class
    inventory.Highlight(x, y, storage);
}
{% endhighlight %}

<header id="AI" class="page-header"><h2><span class="number">4.5</span> AI</h2></header>

