---
layout: page
title: Last Secutor
permalink: /last-secutor
description: 2D Turn Based RPG — an unfinished 8 year project where I experimented and honed my skills in game development and programming
image: assets/images/last-secutor.jpg
page-banner: assets/images/ls-banner.jpg
nav-menu: true

button-url: https://github.com/JKHYuen/LastSecutorBuild
button-text: Download Playable Tech Demo

team-text: Solo Project, with help on placeholder 2D sprite art
date-text: 2014 — 2022
---

<div class=nav>
<h4>Contents</h4>
<ul>
    <li><a href="#overview" class="button small scrolly"><span class="number">1.</span> Overview</a></li>
    <li><a href="#highlights" class="button small scrolly"><span class="number">2.</span> Highlights</a></li>
    <li><a href="#features" class="button small scrolly"><span class="number">3.</span> Game Features</a></li>
        <li><a href="#skill-tree" class="button small scrolly sub-section"><span class="number">3.1</span> Unique Skill Tree System</a></li>
        <li><a href="#combat" class="button small scrolly sub-section"><span class="number">3.2</span> 2D Turn Based Combat</a></li>
        <li><a href="#story-plans" class="button small scrolly sub-section"><span class="number">3.3</span> Story Plans</a></li>
    <li><a href="#implementation" class="button small scrolly"><span class="number">4.</span> Implementation</a></li>
        <li><a href="#rapid-development" class="button small scrolly sub-section"><span class="number">4.1</span> Rapid High-Level Development</a></li>
        <li><a href="#shaders" class="button small scrolly sub-section"><span class="number">4.2</span> Custom Shader Effects</a></li>
        <li><a href="#inventory" class="button small scrolly sub-section"><span class="number">4.3</span> Inventory</a></li>
        <li><a href="#ai" class="button small scrolly sub-section"><span class="number">4.4</span> AI</a></li>
        <li><a href="#hit-splash" class="button small scrolly sub-section"><span class="number">4.5</span> Hit Splash Display (Damage Numbers)</a></li>

</ul>
</div>

<header id="overview" class="major page-header mini"><h1><span class="number">1.</span> Overview</h1></header>
*Last Secutor* is a 2D turn based RPG with ARPG mechanics such as an original skill tree system, expansive loot, and complex character progression; inspired by games like *Path of Exile* and *Dragon Age: Origins*. The core gameplay loop is similar to the original *Diablo*:

<ul style="list-style: decimal">
    <li>Fight in a designated "dungeon" area</li>
    <li>Gain xp and resources</li>
    <li>Return to town</li>
    <li>Assign available skill points and spend resources</li>
    <li>Repeat</li>
</ul>

<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/0d0FjkqnoqU?si=j8Lnz5TknrzNyf3C" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*Footage of the <a href="https://github.com/JKHYuen/LastSecutorBuild" target="_blank" rel="noopener noreferrer">playable tech demo</a>. Note: skill costs and cooldowns are disabled by default, only some skills have sound effects.*

<h4>An Unfinished Game</h4>
I worked on this game for 8 years — first 5 years while in university, and 3 years full time. Unfortunately the project was ultimately too ambitious and it was not financially viable to finish the game. I had only been programming for about a year (Python/Java/C#) when I started developing *Last Secutor* and this was the first project I made without following tutorials. However, this project became an invaluable learning tool I used to teach myself game development. I learned to be autodidactic by always attempting to code things as low-level as possible, rather than using plugins or online solutions. I will usually compare what I come up with existing solutions afterwards to find advantages and disadvantages of different implementations. This learning process allowed me to build arbitrary game mechanics without outside help (other than documentation). 

<video class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/ls-old.mp4" type="video/mp4">
  Old Footage
</video>
*Oldest footage of this project I could find, from October 25 2015.*

I experimented a lot over the years and learned to code common game systems from scratch, many of the implementations in *Last Secutor* have been completely rewritten multiple times. This experience allowed me to efficiently develop future projects by avoiding implementation pitfalls, improving object-oriented design, and adapting to the unique design and technical requirements of each project. 

Several of my projects (including my <a href="{{ site.baseurl }}/nothing-matters" target="_blank" rel="noopener noreferrer">two</a> <a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">games</a> released on Steam) directly benefitted from the experience gained from this project; particularly in the implementation of user saves (serialization), shaders (<a href="#shaders" class="scrolly">e.g. procedural noise effects and general HLSL experience)</a>, aspect ratio/resolution agnostic UI, and frameworks for arbitrary tooltips. 

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>8 years of RPG game development experience (5 years part time, 3 years full time)
        <ul class="highlights-list sub">
            <li>Although this game is unfinished, systems used in my <a href="{{ site.baseurl }}/nothing-matters" target="_blank" rel="noopener noreferrer">released</a> <a href="{{ site.baseurl }}/physarum" target="_blank" rel="noopener noreferrer">games</a> are based off of implementations developed in this project</li> 
            <li>See <a href="#implementation" class="scrolly">4. Implementation</a> for some code examples of game features that have been implemented</li> 
        </ul>
    </li>
    <li>Created in the Unity engine (Built-in Render Pipeline). All game features, shaders and systems coded (C#/HLSL) and designed <i>by myself</i> with no additional plugins or frameworks with two exceptions:
        <ul class="highlights-list sub">
            <li>Anima2D (<a href="https://forum.unity.com/threads/discontinuing-anima2d-consider-2d-animation-for-skeletal-animation-in-unity.1037605/" target="_blank" rel="noopener noreferrer">now a base feature in Unity</a>) for 2D animation rigging</li>
            <li><a href="https://github.com/Siccity/xNode" target="_blank" rel="noopener noreferrer">xNode</a>: a low-level framework to render interactable graphs in the Unity editor (adapted to easily create skill, dialogue, and quest trees within the Unity GUI)</li>
        </ul>
    </li>
    <li>Experience animating and rigging multi-part sprite characters/ragdolls</li>
    <li>Game systems implementation designed for <i>rapid high-level development</i> (<a href="#rapid-development" class="scrolly">See video for full details</a>)
        <ul class="highlights-list sub">
            <li>Allows developers with no programming experience to easily create and tweak game content through the Unity editor</li>
            <li>Core RPG elements are implemented with <a href="https://docs.unity3d.com/Manual/class-ScriptableObject.html" target="_blank" rel="noopener noreferrer">Unity scriptable objects</a> (object oriented design) for seamless integration between modular game systems</li>
        </ul>
    </li>
    <li><a href="#shaders" class="scrolly">Experimentation with various custom HLSL shaders</a> to create interesting visual effects without the need of other artists</li>
    <li>2D Turn based combat that encourages methodical gameplay
        <ul class="highlights-list sub">
            <li>Tile movement in combat for position management with a variety of skills that can push, pull, and trap characters</li>
            <li>A <a href="#reactions" class="scrolly">reaction</a> system that allows players to queue actions that can trigger during an opponents turn if the reaction skill's conditions are met</li>
            <li>Implemented traditional RPG mechanics such as damage resistance, armor, dodge, status effects, mana/stamina costs, summons, stuns, healing and back hits</li>
        </ul>
    </li>
    <li>Original "build your own" <a href="#skill-tree" class="scrolly">modular skill tree mechanic</a></li>
    <li>Additional RPG systems coded from scratch with C# including but not limited to:
        <ul class="highlights-list sub">
            <li>Robust skill implementation allowing for skill attributes (e.g. damage ranges, crit chance, projectile style, buff/debuff application, etc.) to be tweaked and new archetypal skills to be created without the need to add or alter code</li>
            <li>Skill, dialogue and quest tree framework/toolset that allows trees (graphs) to be built within the Unity editor (<a href="#so-video" class="scrolly">video demo</a>)</li>
            <li>Character stat system, that interacts with equipped items, buffs/debuffs, and skill trees during gameplay</li>
            <li>2D turn based (discrete tile movement) controls in combat and point and click continuous movement controls in town</li>
            <li>Grid based inventory/stash supporting items of any size (behavior identical to <i>Path of Exile</i>), all serialized for player saves (<a href="#inventory-video" class="scrolly">video demo</a>)</li>
            <li>Equipment slots that alter different parts of character sprites</li>
            <li><a href="#material-stack" class="scrolly">System to manage multi-layered character effects</a> (i.e. freezing, fire, bloody, etc.), to render an arbitrary amount of custom shaders effects on the same object</li>
            <li><a href="#ai" class="scrolly">AI framework</a> built with Unity coroutines, to create a variety of enemy behaviors in the game's 2D turn based combat system (example AI with different combat styles is shown in the <a href="https://github.com/JKHYuen/LastSecutorBuild" target="_blank" rel="noopener noreferrer">playable tech demo</a>)</li>
            <li>Custom RPG UI featuring draggable skill tree windows, character sheets, a game glossary with searchable key words, a quest journal, and skill bars that support any aspect ratio and resolutions</li>
            <li>Robust tooltip system (for items, skills, skill trees, etc.) with item compare feature (See  <a href="{{ site.baseurl }}/physarum#tooltip" target="_blank" rel="noopener noreferrer"><i>5.2 Tooltip Framework</i> in PHYSARUM</a> for implementation details, it is mostly the same.)</li>
            <li>A detailed "Battle Log" to keep track of all gameplay interactions during combat in real time (<a href="#battlelog-video" class="scrolly">video demo</a>)</li>
            <li>Randomizable items with, tiered affix groups for rewards and enemy equipment</li>
        </ul>
    </li>
</ul>

<b class="alert">NOTE: I did not include every detail for this multi-year project. If you have any questions, feel free to <a href="#contact" class="scrolly">contact me!</a> Be sure to check out the <a href="#implementation" class="scrolly">two commentated videos</a> for a detailed technical overview on most of the game features.</b>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>
The majority of development time was spent building core systems and frameworks (see <a href="#implementation" class="scrolly">4. Implementation</a>), so most of the visual design, game balance and content (e.g. skills, equipment, skill trees) is work in progress. However, the following are examples of features and content that are fully designed and implemented.

<header id="skill-tree" class="page-header"><h2><span class="number">3.1</span> Unique Skill Tree System</h2></header>
The core mechanic of character progression is the unique skill tree system. *Last Secutor*'s skill tree is comprised of 4 swappable subtrees. Subtrees have outer "transition nodes" that allows players to connect to an adjacent subtree. Like other RPGs, players will gain a skill point when leveling to assign to their skill tree. Assigned nodes must have a path to at least one of the subtree's root node.

<div id="video" class="embedded-video mini">
<div class=container>
    <iframe src="https://www.youtube.com/embed/Sb1z9gkpm68?si=qaBHLehC29rBYMZ7" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*Demo with commentary of skill tree system.*

The intent of this skill tree design is to encourage players to experiment with subtrees that are compatible with their builds; while also trying to find the optimal path (least amount of skill points) to the desired skill tree nodes. Nodes are generally more powerful/desirable the farther they are from the subtree root nodes. This rewards players for interacting with the transition nodes mechanic to efficiently reach more powerful nodes in adjacent trees.

<header id="combat" class="page-header"><h2><span class="number">3.2</span> 2D Turn Based Combat</h2></header>
During a combat turn, Players and NPCs will take turns performing actions until they run out of resources. Skills costs can use any consumable resource, including health, armor, stamina and *adrenaline*. Adrenaline is a resource that is gained only if dealing and taking damage. There is also a stun bar for each character. Certain skills will deal "stun" damage, adding to this bar. Once the bar is filled, the character is forced to skip a turn and the stun bar is reset. The combat stage is divided into discrete tiles (internally called "cells" or "grid cells"). Character positioning and skill ranges are all quantized into these tiles.

<h4>Damage</h4>
Like other RPGs, *Last Secutor* provides various ways to attack and defend with character stats. The damage formula involves dodge chance, critical hit chance and accuracy. See below for a visualization of how it works. [Note: all internal nodes represents a percent chance]

<span class="image"><img src="{% link assets/images/ls-damage.png %}" alt="Damage Formula Figure"/></span>

Once damage is taken, damage mitigation is then calculated from character stats. Each damage type (e.g. ice, fire, physical, etc.) has a corresponding percent mitigation and flat mitigation stat. Skills have "tags" system similar to *Path of Exile*. Any damage mitigation stat that matches these tags will be used to reduce the damage taken. In the implementation, tags and damage types are all the same stat objects (see <a href="#so-video" class="scrolly">this video</a> for full implementation details), this means every tag has corresponding damage mitigation stats in this game (e.g. "Projectile", "AOE", "Buff", etc.).

<!-- TODO: show messy damage calc code -->

<img class="image center" src="{% link assets/images/ls-tooltip-1.jpg %}" alt="Tooltip Example"/>
<em style="width:30%;">Skill tooltip: tags highlighted in red<br>(not highlighted in game).</em>

After damage mitigation is calculated, it is finally time to apply the damage. In this game, armor and blocking acts as an additional layer of health. Armor simply acts as health that can't be healed (certain skills can add armor). Block is a little different, block success is calculated based on a character's block chance stat and damage is taken from the block bar as expected, however a character's block bar fully replenishes at the start of their turn. This creates a powerful block mechanic but character must invest in both block chance and block bar for it to be effective. Damage is first taken from block, then armor, then health (unless stated otherwise).

<img class="image center" src="{% link assets/images/ls-healthbars.jpg %}" alt="Tooltip Example"/>
<em style="width:50%;">HUD display for character hit points. Health is red, block is yellow, and armor is represented by a grey overlay on top of health. Aesthetics are not polished, but this is the intended UI design.</em>

<h4 id="reactions">Reactions</h4>
*Last Secutor*'s turn based combat features "reactions" — a special kind of skill that queues up actions that will trigger if certain conditions are met. This creates a way for players to try and gain an advantage during the enemy turn, at he cost of turn resources. NPCs combatant will use these skills as well. Players will be able to see how many queued up reactions the AI has, but will not be able to see what they are. See the <a href="#ai-vs-ai-video" class="scrolly">AI vs AI video below</a> for a demonstration.

<h4>Skills</h4>
Although not completely finished, many skills were designed to encourage combinations and deliberate positioning. All hit detection is done in real time with accurate colliders. This effects how certain skills behave depending on range, particularly with projectile skills. Some skills also rotate between different versions when used (internally called "multi skills"), encouraging resource management and future planning. See video below for examples.

<h5>Notable Timestamps:</h5>
0:57 and 5:28 — skill combos\\
2:57 and 6:50 — projectile hit detection\\
5:01 — multi skill example

<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/_lz07iOkC6w?si=5mDLqFqTDOpHpWRu" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*Demonstration of most skills in the game.*

<h4>Battle Log</h4>
The "battle log" is a feature that records all relevant combat events in an resizable window (press ```B``` in the demo to toggle). It is designed mostly for player curiosity, akin to combat logs in CRPGs, but it is also helpful when debugging.

<video id="battlelog-video" class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/ls-battlelog.mp4" type="video/mp4">
  Battle Log Demo
</video>
*Battle log demo.*

<h4 id="ai-combat">AI Combat</h4>
All turn based combat in this game is against NPCs with various AI combat styles. The UI gives information on the limitations of AI actions. AI's don't use skill resources like players, instead, they have a set amount of skills and movement (in grid cell units) every turn. This design decision was made so it is more convenient for the player to gauge the number of moves the AI can do and react accordingly. Players can also press ```P``` in combat to view revealed NPC skills and stats.

<img class="image center" src="{% link assets/images/ls-ai-ui.jpg %}" alt="AI UI Example"/>
<em>AI actions displayed in UI.</em>

There are two rows of icons (chess image placeholder) next to a number. The icons represent number of skills the AI will use and the number is the amount of movement. The top row shows the current turn's values and the bottom row shows values in the next AI turn. This system also gives a convenient way to control AI difficulty. Each AI preset contains a max value for skill count and movement, these values are randomized from 1 to the max value each turn for gameplay variety.

*Note: some AIs in the tech demo, including the ones in the video below ignores this system due to unfinished development. See <a href="#ai" class="scrolly">4.4 AI</a> for full technical details.*

<div id="ai-vs-ai-video" class="embedded-video mini">
<div class=container>
    <iframe src="https://www.youtube.com/embed/74qN1IjO4rM?si=nngOmPKwU0de1cAE" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*AI vs AI combat demo (available in <a href="https://github.com/JKHYuen/LastSecutorBuild" target="_blank" rel="noopener noreferrer">playable tech demo</a>). Made for debugging only, "AI intention" UI only works for right side.*

<header id="story-plans" class="page-header"><h2><span class="number">3.3</span> Story Plans</h2></header>
The game had extensive plans for a story lead by a mysterious interdimensional cult: *The Unseen Adventists*; a cult comprised of powerful members known to invade and destroy every world they visit. The cultists' motivations remain unknown throughout the game, however they claim to have *seen* something that allowed them to understand the nature of the universe. 

The player will visit the worlds, explore the town/fighting arena with individual questlines, and defeat the invading cult member to progress the story. The story explores themes of nihilism, morality, blind faith, and cosmological philosophy. Many of these concepts are inspired by lore from *Warhammer 40k*.

The cult represents a sci-fi interpretation of *<a href="https://en.wikipedia.org/wiki/Great_Filter" target="_blank" rel="noopener noreferrer">The Great Filter</a>*. Each world features a fatal societal flaw (e.g. overreliance of tradition, corrupt power segregation, etc.), introduced to the player by the invading cult members. The story eventually leads to the discovery of the cult leader — an ancient god-like being that exists between dimensions. Ultimately, the ancient god will show that the player exists in one of an infinite set of parallel universes (in reference to other players), and that the cult's duty is to maintain the careful balance of energies at a cosmological scale.

<header id="implementation" class="major page-header"><h1><span class="number">4.</span> Implementation</h1></header>
<header id="rapid-development" class="page-header"><h2><span class="number">4.1</span> Rapid High-Level Development</h2></header>
Early in development, I decided to implement game systems in such a way that people with no programming experience could make content through the Unity GUI. This allows anyone to easily create new skill trees, skills, and enemies. This was originally done as a programming challenge, but it was also motivated by the prospect of hiring/inviting others to work on the project. These implementations also allowed myself to quickly prototype and tweak existing game content. All this was done with Unity scriptable objects, which are just object instances that can be conveniently edited in the Unity GUI. See the video below for a detailed explanation of this development feature.

<div id="so-video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/UHkDUjA1NUs?si=Hu0gWQxxis3oodEj" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*In-depth overview of most of the RPG system implementations, with code examples and commentary.*

<header id="shaders" class="page-header"><h2><span class="number">4.2</span> Custom Shader Effects</h2></header>
As a solo programmer with no experience hand drawing 2D illustrations, obtaining art assets is often a road block in game development. At first, I used shaders found online to easily add visual flair, but this quickly became a hinderance as I could not make specific effects to my liking.

I soon decided (~2015) the best way to move forward was to learn how to write low-level HLSL shaders myself to create whatever effect I needed. Although daunting at first, this was one of the most valuable skills I learned from this project. This not only allowed me to create countless custom effects in my future projects, but also allowed me to work on my projects without the need to hire other artists. See video below for a summary of my early shader experiments as well as some more complex effects developed in this project.

<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/Xq6KeXNt6ZQ?si=oL-ueUNuYdhKT7fX" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>
*Quick run through of my HLSL shaders, with code examples and commentary.*

I focused on learning to writing shaders in HLSL as opposed to using popular visual programming tools (i.e. Shader Graph) because I wanted to learn a skill that would be easily transferrable to other engines/frameworks (including other shader graphs). This experience inspired me to pursue technical art further, by researching graphics rendering techniques and experimenting with my own implementations (e.g. <a href="{{ site.baseurl }}/bloom-attenuation" target="_blank" rel="noopener noreferrer">my bloom attenuation project</a> ).

<h4 id="material-stack">The Character Material Stack</h4>
Every status effect in the game has an optional accompanying shader effect. Each time a status effect applies a new shader effect, a material instance is created for each body part (characters are comprised of multiple sprite objects for animation/ragdolls) and stored into a dictionary for the character. This is to ensure we don't create a new instance every time we're changing an existing effect (a Unity quirk if material is not cached), and only load the materials that are being used in the current battle. Particle effects specified by the status effect scriptable object are implemented similarly, the particles are randomly spawned on the sprite vertices.

<video class="embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/ls-char-mats.mp4" type="video/mp4">
  Character material stack video
</video>
*Demonstration of multiple shader effects rendered on the same sprite.*

I call this system the "character material stack", however it is implemented as a queue, scheduled by a coroutine. This is required because the effects are quickly interpolated by a universal shader variable to ease in the effect. The queue ensures that the last interpolation of the same effect has completed, this is done only as a aesthetic choice. The status effect shaders are all alpha blended, allowing for an arbitrary amount of character effects to be visible at once. This combined with the flexible development of status effects creates a scalable system for any character effects added in the future.

The code for this system is straight forward and uninteresting, but I wanted to show the use of *material property blocks*. This function eases the visibility of the given shader effect (given by index) on the given renderer (character sprite part).

{% highlight csharp linenos %}
private IEnumerator ChangeFloatPropertyValue(Renderer renderer, int materialIndex, float newValue, bool isInstant = false) {
    // Get the material in materialIndex's current effect value
    MaterialPropertyBlock propBlock = new MaterialPropertyBlock();
    renderer.GetPropertyBlock(propBlock, materialIndex);
    float currentValue = propBlock.GetFloat(PROP_MAG_VAR);

    // Alter material block
    renderer.GetPropertyBlock(propBlock);
    if(!isInstant) {
        float timer = 0f;
        float duration = 0.3f;
        while(timer < duration) {
            propBlock.SetFloat(PROP_MAG_VAR, lerp(currentValue, newValue, timer / duration));
            renderer.SetPropertyBlock(propBlock, materialIndex);
            timer += Time.deltaTime;
            yield return null;
        }
    }
    
    propBlock.SetFloat(PROP_MAG_VAR, newValue);
    renderer.SetPropertyBlock(propBlock, materialIndex);
}
{% endhighlight %}

The drawback of having multiple materials is that there will be multiple draw calls. I decided to use <a href="https://docs.unity3d.com/ScriptReference/MaterialPropertyBlock.html" target="_blank" rel="noopener noreferrer">Unity material property blocks</a>, which batches all of the same materials in one call while changing a shader property. This was ultimately unnecessary premature optimization since there are very few characters using the same material in the 2D combat scenes (lesson learned once again). It's possible that using a monolithic shader with shader keywords to conditionally calculate needed effects would be more time efficient. However, it would be significantly less convenient to add new status effects; which is a much more important feature.

<header id="inventory" class="page-header"><h2><span class="number">4.3</span> Inventory</h2></header>
The grid based inventory was one of the more tricky game systems I implemented. As a challenge, I wanted to replicate *Path of Exile*'s inventory UI functionality exactly. 

<video id="inventory-video" class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/ls-inventory.mp4" type="video/mp4">
  Inventory Demo
</video>
*Side by side Comparison with Path of Exile's Inventory System*

After an initial attempt with assumptions of how the UI worked, I found that my UI felt different and less comfortable than <i>Path of Exile</i>'s. This lead to a realization I never noticed while playing the game — which is that the grid highlighting (when hovering over grid space with an item on cursor) does not update when the cursor crosses a border of a grid square, but rather, when it crosses a **midpoint** of a grid square. To my surprise, this non-trivial difference changes the look and feel of the inventory system completely.

<h5>Find Half Square Index From Mouse Pointer Location</h5>
{% highlight csharp linenos %}
private void UpdateHighlightData() {
    if (isPointerInContainer && inventory.cursorItem) {
        Vector2 pointerLocalPos;
        RectTransformUtility.ScreenPointToLocalPointInRectangle(
            (RectTransform)transform,
            Input.mousePosition,
            null,
            out pointerLocalPos
        );

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
*Note: ```position[]``` is an array with two elements representing the grid position in the inventory (this function is a member of the grid element class). This function calculates ```halfSquareIndex[]``` — a two element array representing the index on the inventory grid with 2x the resolution (i.e. each grid square is split into 4 quadrants)*

<div class="box" markdown="1">
*Development Note:*\\
This code was written in 2018, the implementation is not very optimized and readability could be improved. I remember this algorithm being very difficult to figure out at the time, so I decided to share the original code here for posterity.

For example, ```UpdateHighlightData(...)``` creates a new array every frame, causing unnecessary strain on the GC (<a href="https://ericlippert.com/2010/09/30/the-truth-about-value-types/" target="_blank" rel="nooperner noreferrer">theoretically</a>). Unity's ```Vector2``` type is a much better fit since it is a value type and it improves readability significantly. Regardless, I'm satisfied with this solution since I know it works and optimizing this early in development with no performance issues would almost definitely be a mistake.
</div>

<h5>Finding Which Inventory Squares to Highlight</h5>
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
*Note: indices are rounded to match Path of Exile's inventory UI behavior*

<header id="ai" class="page-header"><h2><span class="number">4.4</span> AI</h2></header>
<h4>AI Framework</h4>
A comprehensive AI framework was developed to allow combat NPCs to perform any action players can, while abiding to the rules of the 2D combat system. This can be challenging, since animations must be interrupted properly and mechanics like knockback can happen during any given action. Spin locks within coroutines are often used to solve these issues, however a proper state machine would probably be more robust and reliable.

Below is the code for moving within a given range, this is usually called before using a chosen skill to hit something. Some movement skills can ignore obstacles (e.g. teleport and jump), these skills have a ```b_canMoveThroughEntities``` member that will adjust this algorithm accordingly. ```MoveInRange(...)``` is usually used to move within a queued skill's range before triggering the skill. For other movement behavior such as moving behind the player, ```MoveTrigger(...)``` can be called directly within the individual AI algorithms.

{% highlight csharp linenos %}
protected IEnumerator MoveInRange(int cellRange, Skill moveSkill, bool stayWithinRange = true, bool moveIntoEntities = false) {
    // Wait for previous AI action
    while (AIPause) {
        yield return null;
    }

    /// Sanity Checks
    // if cell range ends up being 0, default it to 1 so we don't have to worry about going behind the target
    if(cellRange == 0) {
        cellRange = 1;
    }

    if(!targetController) {
        if(defaultTarget) {
            targetController = defaultTarget;
        }
        else {
            Debug.Log("AI Movement: AI tried to move in range without target.");
            yield break;
        }
    }

    if(!(moveSkill is Movement)) {
        Debug.LogError("AI Movement: MOVEMENT skill must be used for \"MoveInRange()\".");
        yield break;
    }
    ///

    // cell index we are trying to move to
    int goalIndex = targetCellIndex;

    // Find closest entity in the way and make it the new target if this AI can not move through entities
    if (!(moveSkill as Movement).b_canMoveThroughEntities && !moveIntoEntities) {
        // scan for intermediate objects
        List<UserController> scannedObjects = CellObjectScan(CellIndex, targetCellIndex, targetTeamID, out UserController closest);
        // if there are more than one, select the one closest to this AI
        if (closest) {
            // target is now the intermediate object
            targetController = closest;
            // update goal index
            goalIndex = targetCellIndex;
        }
    }

    int direction = 1;
    if (goalIndex > cellIndex) {
        direction = -1;
    }

    if (stayWithinRange) {
        // if already within range,
        // do nothing
        if (CheckInRange(cellIndex, goalIndex, cellRange)) {
            //Debug.Log($"AI Movement: Already in Range ({cellRange})");
            yield break;
        }
    }

    // clamp cell range within stage
    int clampedIndex = GridSystem.ClampGridIndex(goalIndex + (cellRange * direction));

    // Check if clamped cell range is vacant, keep trying cells within range
    // do not check for obstacles if this AI can move into entities
    int i = clampedIndex;
    if(!moveIntoEntities) {
        Cell currentTargetCell = GridSystem.manager.GetCellFromIndex(i);
        while (currentTargetCell.cellObjectUserControllers.Count > 0 && !currentTargetCell.CellTraversableCheck(userController.cellObjectType)) {
            // no possible position, give up
            if (GridSystem.manager.GetCellFromIndex(i).cellObjectUserControllers.Contains(targetController) || i == cellIndex) {
                Debug.Log("AI Movement: " + userController.gameObject.name + ": No valid cell found for movement.");
                yield break;
            }

            if (goalIndex > i) {
                i--;
            }
            else {
                i++;
            }

            // out of grid, give up
            if (!GridSystem.IndexIsInGrid(i)) {
                Debug.Log("AI Movement: " + userController.gameObject.name + ": No valid cell found for movement.");
                yield break;
            }
        }
    }

    cellRange = Mathf.Abs(i - goalIndex) * (int)Mathf.Sign(cellRange);

    // Do move to closest vacant cell within range without range check
    yield return MoveTrigger(cellRange, moveSkill);
}
{% endhighlight %}
*Note: ```targetController``` is the entity AI is currently trying to attack, ```targetCellIndex``` is the cell the AI is currently trying to move to*

A lot of (mostly uninteresting) logistical helper functions were written to make sure AI actions abide to all the game's rules and mechanics. Below are some examples:

<h5 markdown="1">Function to finds all character entities in a cell range (used in ```line 35``` above):</h5>
{% highlight csharp linenos %}
// Checks for all UserController GameObjects in cells between two cell positions on the stage (exclusive of start and end positions)
// that have the same teamID as "teamIDLookUp", if "teamIDLookUp" is -1, scan all UserControllers
// "closest" parameter: gameobject to cellPosition, null if none
// returns: list of all found GameObjects
protected List<UserController> CellObjectScan(int originIndex, int targetIndex, int teamIDLookUp, out UserController closest, int teamIDIgnore = -1, bool bIncludeOriginCell = false) {
    closest = null;
    List<UserController> ret = new List<UserController>();

    // find start and end index for the for loop
    int startIndex = GridSystem.ClampGridIndex(Mathf.Min(originIndex, targetIndex));
    int endIndex = GridSystem.ClampGridIndex(Mathf.Max(originIndex, targetIndex));

    // start in front of lower index for exclusive bound check
    for (int i = startIndex; i <= endIndex; i++) {
        // Check whether to include origin cell or not
        if (!bIncludeOriginCell && i == originIndex) {
            continue;
        }

        // if there is a cell object in these cells, add it to the return list
        Cell checkCell = GridSystem.manager.GetCellFromIndex(i);
        if (checkCell.cellObjectUserControllers.Count > 0) {
            foreach(UserController targetController in checkCell.cellObjectUserControllers) {
                // ignore self and unhittable users
                if (!targetController.isIgnoreHits && targetController != userController) {
                    // add found object if teamID requirements are met
                    if ((teamIDLookUp == -1 || targetController.teamID == teamIDLookUp) && (teamIDIgnore == -1 || teamIDIgnore != targetController.teamID)) {
                        ret.Add(targetController);
                    }
                }
            }

        }
    }

    // Get closest entity based on scan direction
    if(ret.Count > 0) {
        closest = (originIndex < targetIndex) ? ret[0] : ret[ret.Count - 1];
    }

    return ret;
}
{% endhighlight %}

<h5>Helper function to find closest character entity, with an alliance (team) filter:</h5>
{% highlight csharp linenos %}
// if "teamIDLookUp" is -1, scan all characters
protected UserController FindClosestEntity(int originIndex, int range, int teamIDLookUp, int teamIDIgnore = -1, bool bIncludeOriginCell = false) {
    // Check to the left and right of origin within range
    CellObjectScan(originIndex, originIndex - range, teamIDLookUp, out UserController closest_2, teamIDIgnore, bIncludeOriginCell);
    CellObjectScan(originIndex, originIndex + range, teamIDLookUp, out UserController closest_1, teamIDIgnore, bIncludeOriginCell);

    UserController ret = null;

    if(closest_1 && closest_2) {
        ret = Mathf.Abs(closest_1.CellIndex - CellIndex) < Mathf.Abs(closest_2.CellIndex - CellIndex) ? closest_1 : closest_2;
    }
    else {
        if(!closest_1 ^ !closest_2) {
            ret = closest_1 == null ? closest_2 : closest_1;
        }
    }

    return ret;
}
{% endhighlight %}

<h4>AI Behavior Scripting</h4>
*Technical Note: I use the term "script" loosely here. Although the following code is compiled rather than interpreted, the term "scripting" here just implies "high level code using my AI framework". Unity also refers to all ```MonoBehaviour```s as scripts.*

Using this framework, individual AI behavior can be scripted conveniently by inheriting the ```AI``` base class (all code samples above are from this ```AI``` class). These AI scripts generally just consists of a series of game state condition checks (e.g. character health values) to pick the next skill to perform. This method is inspired by the <a href="https://dragonage.fandom.com/wiki/Tactics_(Origins)" target="_blank" rel="noopener noreferrer"><i>Dragon Age: Origin</i> "tactics" mechanic</a>, because of the believable AI behavior that was possible using that simplistic system. 

<h4>Finite State Machines (FSM)</h4>
I opted to not use a FSM solution at the time (~2019) because while researching and experimenting, I decided FSMs may be overkill for the limitations of my game's combat. In practice, I also preferred my lower level approach since it was easier to iterate new ideas quickly and see what was going on at a glance of the code. Admittedly, I don't have too much experience with FSMs, but it seemed harder to see what's going on without seeing a visual graph of all the AI states — that could possibly span multiple classes. I didn't end up implementing a full FSM workflow, but my <a href="#so-video" class="scrolly">scriptable object based graph visualizer (see timestamp 17:22)</a> could have alleviated some of these concerns. This is something I intend to revisit in future projects because the high level abstraction can definitely build complex behaviors much more conveniently than my implementation. I would wager that the aforementioned *Dragon Age: Origins* "tactics" system was implemented by integrating it into a larger FSM AI framework.

<h4>New and Legacy AI System</h4>
Unfortunately, showing the working AI behavior scripts will be a little messy since it was still under development. The <a href="#ai-combat" class="scrolly">current AI action system</a> was a relatively late addition to this game's design so I had to convert some older working code. The old system used character resources (stamina, mana, etc.) just as the player would. I eventually decided that this made it too hard for the player to predict and react to the AI behavior, so I opted for the current more streamlined version. This conversion was never completely finished, but both workflows work in the latest build (the tech demo uses both types of AIs). For completeness I will show an example of both.

<h5>Legacy AI that summons wall obstacles  in (featured in <a href="#ai-vs-ai-video" class="scrolly" style="border-bottom: dotted 1px;">AI vs AI video</a>)</h5>
{% highlight csharp linenos %}
protected override IEnumerator StartAICoroutine() {
    targetController = defaultTarget;

    // if I am BELOW half health
    if (!CurrentLifePercent_GreaterThan(50)) {
        // 100 - current precent of life chance to do self preservation (e.g. 30% life => 70% chance to heal)
        if (RNG.PercentChanceRoll(100 - GetCurrentStatPercent(ResourceType.Life))) {
            yield return RetreatAndHeal();
        }
        else {
            if (RNG.PercentChanceRoll(50)) {
                yield return LightningCombo();
            }
            else {
                yield return KeepDistant();
            }
        }
    }
    // if I am ABOVE half health
    else {
        // if target's health is BELOW 50%
        if (currentTargetHealth < currentTargetMaxHealth * 0.5f) {

            if (RNG.PercentChanceRoll(50)) {
                yield return RandomCombo();
            }
            else {
                yield return LightningCombo();
            }

        }
        // target health ABOVE 50%
        else {
            yield return RandomCoroutine(RandomCombo(), KeepDistant(), DebuffTarget());
        }
    }

    yield return EndTurn();
}

private IEnumerator RetreatAndHeal() {

    // if there aren't already obstacles between target and AI, create icewall
    if(!ObstacleCheck()) {
        // summon icewall between me and target
        yield return TriggerSkill(summonIcewall, -1, true);
    }

    // make some space from target
    yield return MoveInRange(3, defaultWalk, false);

    // heal
    yield return TriggerSkill(rest);

}

public IEnumerator KeepDistant() {
    // Move to side of target that has more room
    if (CheckEmptySpaceFromTarget() > 0) {
        yield return MoveInRange(3, phase, false);
    }
    else {
        yield return MoveInRange(-3, phase, false);
    }

    // if there is an obstacle, set up traps
    if(ObstacleCheck()) {
        yield return TriggerSkill(fireBlast);
        yield return TriggerSkill(fireBlast);
        yield return TriggerSkill(RandomSkill(dodgeBack, elementalFocus, invigorate, dodgeForward));
    }
    else {
        // random range attacks
        yield return TriggerSkill(RandomSkill(iceGale, fireball));
        Skill randomSkill = RandomSkill(iceGale, elementalFocus, fireball);
        yield return MoveInRange(randomSkill.range, defaultWalk);
        yield return TriggerSkill(randomSkill);
    }

}

public IEnumerator RandomCombo() {
    Skill randomSkill;

    // 50/50 chance to keep buff going
    if(RNG.PercentChanceRoll(50)) {
        yield return TriggerSkill(elementalFocus);
    }

    // if there is an obstacle in front of target
    if (ObstacleCheck()) {
        if(RNG.PercentChanceRoll(50)) {
            yield return MoveInRange(-2, phase);
        }
        else {
            yield return TriggerSkill(elementalFocus);
        }
    }

    // if there is still an obstacle, set up traps
    if (ObstacleCheck()) {
        yield return TriggerSkill(fireBlast);
        yield return TriggerSkill(fireBlast);
        yield return TriggerSkill(RandomSkill(dodgeBack, elementalFocus, invigorate, dodgeForward, elementalConfusion));
    }
    else {
        // 50/50 to set up traps
        if (RNG.PercentChanceRoll(50)) {
            yield return MoveInRange(2, defaultWalk, false);
            yield return TriggerSkill(fireBlast);
        }
        else {
            randomSkill = RandomSkill(iceGale, fireball);
            yield return MoveInRange(randomSkill.range, defaultWalk);
            yield return TriggerSkill(randomSkill);
        }

        randomSkill = RandomSkill(iceGale, dodgeBack, dodgeForward, fireball, elementalConfusion);
        yield return MoveInRange(randomSkill.range, defaultWalk);
        yield return TriggerSkill(randomSkill);

        // 50/50 chance to move away
        if (RNG.PercentChanceRoll(50)) {
            yield return MoveInRange(2, defaultWalk, false);
        }
    }

}

public IEnumerator DebuffTarget() {
    // if there is an obstacle, phase behind target
    if (ObstacleCheck()) {
        yield return MoveInRange(-2, phase);
    }

    yield return MoveInRange(3, defaultWalk, false);

    yield return TriggerSkill(elementalFocus);
    yield return TriggerSkill(summonIcewall, -1);
    yield return TriggerSkill(RandomSkill(lowerFireRes, elementalConfusion));
}

public IEnumerator LightningCombo() {
    yield return TriggerSkill(elementalFocus);

    yield return MoveInRange(2, defaultWalk, false);
    yield return TriggerSkill(lightningStrike);
}
{% endhighlight %}
*Note: "TriggerSkill" function signature: ```IEnumerator TriggerSkill(Skill skill, int cellOffset = 0, bool targetSelf = false, bool targetIntermediateObject = false)```*

<h4>Current AI System</h4>
Some of the boilerplate parts of the algorithm is extracted to the base class for the updated system. New AI scripts only determine the next skill to use and potential bonus action. Repositioning can still be done by choosing a movement skill.

<h5>New base StartAICoroutine() function:</h5>
{% highlight csharp linenos %}
protected virtual IEnumerator StartAICoroutine() {
    targetController = defaultTarget;
    aiMoveDisplayController.UpdateAIToNextTurn(this);

    while(currentActionCount > 0) {
        if(GameManager.isEndOfGame) {
            yield break;
        }

        ChosenSkillData chosenSkillData = ChooseNextSkillInAILoop();
        Skill chosenSkill = chosenSkillData.skill;
        if(chosenSkill) {
            // Move into skill range
            if(chosenSkill.range > 0) {
                int targetRange = chosenSkill.range;

                // if chosen skill is a teleport skill, assume we are going behind the target
                if(chosenSkill is Movement movementSkill && movementSkill.isTeleport) {
                    targetRange = -1;
                    yield return MoveInRange(targetRange, chosenSkill, false);
                }
                // if chosen skill is not a movement skill, and there are remaining movement points,
                // walk into range
                else if(currentMovementCount > 0) {
                    // if target cell is more than current movement count, move as close as possible
                    if(GetTargetDistance() - targetRange > currentMovementCount) {
                        targetRange = GetTargetDistance() - currentMovementCount;
                    }

                    yield return MoveInRange(targetRange, defaultWalk, !chosenSkill.b_AlwaysMoveToExactRange);
                }
            }

            // Use non-movement skill
            if(!(chosenSkill is Movement)) {
                // only use skill if in range, otherwise action is wasted (think of something else?)
                // if a multi skill, use it anyway to not mess up sequence index
                if(CheckIfTargetInRange(chosenSkill.range + chosenSkill.radius) || chosenSkill.range == 0 || chosenSkill.nextSkill != null) {
                    yield return TriggerSkill(chosenSkill, cellOffset: chosenSkillData.offset);
                }
                else {
                    yield return ShowOutOfRangeMessage(chosenSkill.displayName);
                }
            }
        }
        else {
            Debug.LogWarning("AI: no skill chosen in loop", userController);
        }

        // End turn if skill choosing functions says so
        if(chosenSkillData.b_endTurn) {
            break;
        }

        currentActionCount--;
        aiMoveDisplayController.RemoveCurrentActionIcon();

        while(AIPause) {
            yield return null;
        }
    }

    // Bonus Action(s)
    yield return BonusActionAfterAILoop();

    yield return EndTurn();
}
{% endhighlight %}

<h5 markdown="1">AI script of a basic melee NPC using new system (used in ```line 10``` above):</h5>
{% highlight csharp linenos %}
protected override ChosenSkillData ChooseNextSkillInAILoop() {
    Skill chosenSkill = default;

    // Teleport to the side with more room
    if(RNG.PercentChanceRoll(65) && CheckIfMoreRoomBehindTarget()) {
        chosenSkill = teleportStrike;
    }
    // to pocket sand if target is adjacent
    else if(CheckIfTargetInRange(1) && RNG.PercentChanceRoll(50)) {
        chosenSkill = RandomSkill(pocketSand, spearStab);
    }
    else {
        // if currently healthy
        if(CurrentLifePercent_GreaterThan(60)) {
            // offensive combos
            if(RNG.PercentChanceRoll(80)) {
                chosenSkill = RandomSkill(spearStab, kick, grapple, groundSpike);
            }
            // defensive combos
            else {
                chosenSkill = RandomSkill(rest, dodgeBack, dodgeForward, invigorate);
            }
        }
        // not healthy
        else {
            // if target healthy
            if(TargetCurrentLifePercent_GreaterThan(80)) {
                chosenSkill = RandomSkill(spearStab, rest, dodgeBack, dodgeForward, invigorate, groundSpike);
            }
            // if target not healthy
            else {
                if(RNG.PercentChanceRoll(80)) {
                    chosenSkill = RandomSkill(spearStab, kick, grapple);
                }
                else {
                    chosenSkill = RandomSkill(rest, dodgeBack, dodgeForward, invigorate);
                }
            }
        }
    }

    return new ChosenSkillData(chosenSkill, 0);
}

protected override IEnumerator BonusActionAfterAILoop() {
    yield return TriggerBonusAction(RandomSkill(dodgeBack, dodgeForward, invigorate), 5);
}
{% endhighlight %}


<header id="hit-splash" class="page-header"><h2><span class="number">4.5</span> Hit Splash Display (Damage Numbers)</h2></header>
A design goal I had early in development is to keep damage values and modifiers as low as possible. In my opinion, smaller numbers give a more satisfying sense of progression than very large ones. For example, upgrading a skill from 8 damage to 11 damage is much easier to parse than upgrading damage from 1,165,236 to 1,602,199 (same percentage increase). This is not always easy to control in a large game with long term support (i.e. power creep), but I believe it was obtainable for my relatively small single player game.

Since keeping track of the low numbers is very important for the sense of accomplishment in this game, **it is mandatory that the damage numbers do not overlap**. The aesthetic is inspired by *Old School Runescape*'s <a href="https://secure.runescape.com/m=news/maximum-hitsplats--clan-hall-changes?oldschool=1" target="_blank" rel="noopener noreferrer">hitsplats</a>, since it has similar design requirements with damage numbers. I call my UI elements "hit splashes".

<video id="hit-splash-video" class="scroll-auto embedded-video mini" muted controls playsinline loop>
  <source src="{{ site.baseurl }}/assets/videos/ls-hit-splash.mp4" type="video/mp4">
  Hit splash Demo
</video>
*Many hit splashes occurring at once.*

To avoid number overlaps, my algorithm starts from the center of the character, then searches for a vacant position by radially checking positions in a growing radius. This is done with the parametrized circle equation so the radius and angle steps can be controlled easily. I could have used randomization and collision checks with the built in Unity physics system, but I opted for this low-level implementation for more control and predictability.

<h5>Hit Splash Placement Without Overlap</h5>
{% highlight csharp linenos %}
    private IEnumerator CreateHitSplash(string text, Color color, int fontSize, Sprite spriteIcon = null) {
        // New hit splash is instantiated
        GameObject hitSplashInstance = Instantiate(HUDManager.manager.hitSplashPrefab, HitSplashParent.transform);
        RectTransform hitSplashInstanceTransform = hitSplashInstance.GetComponent<RectTransform>();
        HitSplashController hitSplashInstanceController = hitSplashInstance.GetComponent<HitSplashController>();
        RectTransform hitSplashTextTransform = hitSplashInstanceController.displayText.GetComponent<RectTransform>();

        hitSplashInstance.name = text;

        Text hitSplashText = hitSplashInstanceController.displayText;
        hitSplashText.text = text;
        hitSplashText.fontSize = fontSize;
        hitSplashText.color = color;

        if(spriteIcon) {
            hitSplashInstanceController.icon.gameObject.SetActive(true);
            hitSplashInstanceController.icon.sprite = spriteIcon;
        }

        // Add this hit splash to list of all active hit splashes
        activeHitSplashTextTransforms.Add(hitSplashTextTransform);

        // Calculate preferred width to update content size fitter
        LayoutRebuilder.ForceRebuildLayoutImmediate(hitSplashTextTransform);
        yield return new WaitForEndOfFrame();

        // increment for radius
        // Pick random increment to add some variability
        float radiusSearchIncrement = Random.Range(5f, 15f);

        // increment for parameter i.e. perimeter spacing
        int parameterSearchIncrement = 5;
        bool collision = false;

        // Search for a vacant position (no overlap) for new hit splash by parametrically looking through circles with increasing radius
        // max radius: 10
        for (float r = 0f; r <= 2000; r += radiusSearchIncrement) {
            for (int t = 0; t <= 360; t++) {
                // reset collision flag
                collision = false;

                // check every n parameters
                if (t % parameterSearchIncrement == 0) {
                    // Move hit splash 
                    hitSplashInstanceTransform.localPosition = new Vector2(r * Mathf.Cos(t * Mathf.Deg2Rad), r * Mathf.Sin(t * Mathf.Deg2Rad));

                    // check if there are no collisions for all active hit splashes, if there is one, break for loop and continue while loop
                    foreach (RectTransform existingHitSplashTextTransform in activeHitSplashTextTransforms) {
                        // do not check if instance is colliding with itself
                        if (existingHitSplashTextTransform == hitSplashTextTransform) {
                            continue;
                        }
                        if (RectOverlapCheck(hitSplashTextTransform, existingHitSplashTextTransform)) {
                            collision = true;
                            break;
                        }
                    }

                    // No collisions with any other active hit splashes, vacant position found
                    if (!collision) {
                        break;
                    }
                }

                // only check first position for r = 0 (origin)
                if (r == 0) {
                    break;
                }
            }

            // Position found, break radius loop
            if (!collision) {
                break;
            }

            // Contingency
            if(r > 2000) {
                Debug.Log("ERROR: vacant space for hit splash not found");
            }
        }

        // Start process of fading hit splash away
        StartCoroutine(FadeOutAndDestroy(hitSplashInstanceController));

        yield return null;
    }
{% endhighlight %}

I used a naive O(n^2) approach for overlap detection; each hit splash checks every other hit splash for collisions. This is possibly slower than using an out-of-the-box physics engine (with Dynamic AABB trees, etc.), but the Unity physics engine does not work well with it's UI renderer (very slow, possibly from frequent canvas updates). Although my method is brute force, the algorithm can be constant time depending on hit frequency and the fade delay. Constant time can also be guaranteed by limiting the number of hit splashes on the screen (i.e. remove the oldest hit splashes when limit is reached).

The <a href="#hit-splash-video" class="scrolly">video above</a> shows the intended upper limit of hit frequency. Based on anecdotal tests, it is clear that the algorithm runs *well enough* for this game. Run time performance is also aided by the tweakable fade timer (hit splashes are destroyed after delay) and radius/angle step size. Additionally, the hit splash objects are not object pooled in this implementation, a feature that can be trivially added if needed. *Object instantiation and destruction is probably the most time costly part of the algorithm.*

<h4>Removed Bonus Feature</h4>
With the code above, the first hit splash will be perfectly centered with a character model. A second immediate hit splash will always be placed directly to the right of the first one. I had the idea that it would be more aesthetically pleasing if the first 3 hit splashes are always centered by averaged position. This is done by shifting the whole canvas after finding a vacant spot with the method above. I ultimately scrapped this idea because it made keeping track of the hit splashes a little more difficult since the hit splashes would jump around instead of always being in the same spot.

<h5>Calculate Average Position and Shift Canvas</h5>
{% highlight csharp linenos %}
// If 3 or less active splashes (do nothing if there is just 1),
// Calculate avg position of all hit splashes to center parent transform
if(activeHitSplashTextTransforms.Count <= 3 && activeHitSplashTextTransforms.Count > 1) {
    Vector3 avgPos = Vector3.zero;
    foreach(RectTransform hitSplashTransform in activeHitSplashTextTransforms) {
        avgPos += hitSplashTransform.parent.GetComponent<RectTransform>().localPosition;
        Debug.Log(hitSplashTransform.parent.GetComponent<RectTransform>().localPosition, hitSplashTransform);
    }
    avgPos /= activeHitSplashTextTransforms.Count;
    // Move origin to avg position of all hit splashes
    HitSplashParent.GetComponent<RectTransform>().localPosition = -avgPos;
}
else {
    HitSplashParent.GetComponent<RectTransform>().localPosition = Vector3.zero;
}
{% endhighlight %}
*Note: This code would be inserted in ```line 80``` in the ```CreateHitSplash(...)``` function above.*

