---
layout: page
title: Palindrome
permalink: /palindrome
description: 2D arena shooter proof of concept demo inspired by Christopher Nolan's <i>Tenet</i>
image: assets/images/palindrome.jpg
# TODO: get a different page-banner
page-banner: assets/images/palindrome.jpg
nav-menu: true

button-url: https://github.com/JKHYuen/PalindromeBuild
button-text: Download Proof of Concept Demo

date-text: Oct 6 2020 — Oct 12 2020
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

<!-- TODO: github readme -->
<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
*Palindrome* was a project I started immediately after watching <a href="https://www.imdb.com/title/tt6723592/" target="_blank" rel="noopener noreferrer">Tenet</a>. I spent 6 days to make a proof of concept game demo that features similar time rewind combat mechanics from the movie. The game is a 2D local multiplayer arena shooter where two players can rewind time for their character at any time. Each player has their own timeline that is separate from the world timeline. This means a player in normal time can actively fight an opponent who is going backwards in time. 

Players can shoot, throw grenades, jump, climb walls, crouch, and dive. All actions, audio, and visual effects will reverse during time rewind as expected. This includes blood particles, bullet impacts particles, bullet trails, and damage taken. Unique combat situations arise with time reversal combat, such as not needing to reload when the bullets reenter the player's gun, damaging your opponent with bullets going backwards, and watching blood go back into your character after rewinding a bullet wound.

*Note: The demo unfortunately only supports one player on keyboard and one player on controller*

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>

<header id="time-reversal" class="page-header"><h2><span class="number">3.1</span> Combat</h2></header>
<!-- TODO: bunch of combat videos, time controls/bar mechanic -->

<header id="gameplay-loop" class="page-header"><h2><span class="number">3.2</span> Gameplay Loop</h2></header>
The proof of concept demo has all the features for two local players to play competitively. When a player dies, world time is slowed down for dramatic effect, then time for the dead player will be rewound for 5 seconds to revive them (the other player can't move during this time for fairness). This is called a *Timeline Inversion Revive*, and each player gets one per game, indicated by a glowing red orb in the UI. Players have unlimited ammo, but limited grenades. Health, revive, and grenade pickups are spawned in random locations on the stage at random times during gameplay.

Once a player is dead with no revives, the opposing players get a point, and the next round starts when both players press ready. First to 3 points win the game. Player names (shown in score screen), number of points needed to win, and number of starting revives can all be tweaked in the main menu.

<header id="implementation" class="major page-header"><h1><span class="number">4.</span> Implementation</h1></header>
<header id="time-reversal" class="page-header"><h2><span class="number">4.1</span> Time Reversal</h2></header>
To save time, I used <a href="https://ludiq.io/chronos/features" target="_blank" rel="noopener noreferrer">Chronos</a> (a deprecated framework) to keep track of time events for the time reversal mechanic. Although it works great for this proof of concept, the implementation is relatively crude, with little to no space optimization (a non-trivial problem to solve unless you are <a href="https://www.youtube.com/watch?v=8dinUbg2h70" target="_blank" rel="noopener noreferrer">Jonathan Blow </a>). The plugin comes with accurate-enough position tracking, however other time reverse effects require additional code. 

Chronos allows for time events to be scheduled into timelines, a delegate is given for the forward passage of the event, and a different delegate for the backwards passage. For example, the following is the scheduling of events for a bullet impact on a wall using the ```Do()``` function from Chronos, with ```time``` as one of the player's timeline:

{% highlight csharp linenos %}
time.Do(
    true,
    delegate() {
        // find rotation to opposite direction of bullet velocity and rotate impact to that direction
        Quaternion rotation = Quaternion.Euler(new Vector3(0, 0, Mathf.Atan2(-time.rigidbody2D.velocity.y, -time.rigidbody2D.velocity.x) * Mathf.Rad2Deg));
        GameObject bulletImpactInstance = Instantiate(GameManager.manager.bulletImpactPrefab, transform.position, rotation);
        bulletImpactInstance.transform.SetParent(transform, false);

        Timeline bulletImpactTimeline = bulletImpactInstance.GetComponent<Timeline>();
        bulletImpactTimeline.globalClockKey = time.globalClockKey;
        bulletImpactTimeline.particleSystem.Play();

        AudioSource impactAudioSource = bulletImpactInstance.GetComponent<AudioSource>();
        impactAudioSource.pitch = 1;
        impactAudioSource.PlayOneShot(stageHit);

        bulletImpactTimeline.Plan(
            stageHit.length,
            true,
            delegate () { },
            delegate () {
                impactAudioSource.clip = stageHit;
                impactAudioSource.pitch = -1;
                impactAudioSource.time = stageHit.length - 0.01f;
                impactAudioSource.Play();
            }
        );

        return bulletImpactInstance;
    },
    delegate(GameObject bulletImpactInstance) {
        Destroy(bulletImpactInstance);
    }
);
{% endhighlight %}
*Note: function signature: ```Do<T>(bool repeatable, ForwardFunc<T> forward, BackwardFunc<T> backward)```

An additional ```Plan()``` function is nested in the ```forward``` delegate in ```line 17```. ```Plan()``` is the same as ```Do()```, except it has an additional delay parameter to schedule it forward in time. This is useful for managing rewindable audio clips, since we can line up the backwards audio clip in the future with the length of the audio clip (```line 18```). Setting pitch to -1 in the Unity audio component plays audio backwards (```line 23```) , so we don't need to create new audio clips.

<!-- TODO: Time, Grenade, Bullet Trails -->

