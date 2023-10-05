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
        <li><a href="#combat" class="button small scrolly sub-section"><span class="number">3.1</span> Time Reverse Combat</a></li>
        <li><a href="#gameplay-loop" class="button small scrolly sub-section"><span class="number">3.2</span> Gameplay Loop</a></li>
    <li><a href="#implementation" class="button small scrolly"><span class="number">4.</span> Implementation</a></li>
        <li><a href="#time-reversal" class="button small scrolly sub-section"><span class="number">4.1</span> Time Reversal</a></li>
        <li><a href="#bullets" class="button small scrolly sub-section"><span class="number">4.2</span> Bullets</a></li>
        <li><a href="#grenades" class="button small scrolly sub-section"><span class="number">4.3</span> Grenades</a></li>
</ul>
</div>

<!-- TODO: github readme, known bug if player dies during revive -->
<header id="overview" class="major page-header"><h1><span class="number">1.</span> Overview</h1></header>
<div id="video" class="embedded-video">
<div class=container>
    <iframe src="https://www.youtube.com/embed/aL_vSCgVSbU?si=vrLpo9PW1l9XXnxM" title="YouTube video player" allowfullscreen></iframe>
</div>
</div>

*Palindrome* was a project I started immediately after watching <a href="https://youtu.be/4xj0KRqzo-0?si=C0E3o7mncO0CjlLk" target="_blank" rel="noopener noreferrer">Tenet</a>. I spent 6 days to make a proof of concept game demo that features similar time rewind combat mechanics from the movie. The game is a 2D local multiplayer arena shooter where two players can rewind time for their character at any time. Each player has their own timeline that is separate from the world timeline. This means a player in normal time can actively fight an opponent who is going backwards in time. 

Players can shoot, throw grenades, jump, climb walls, crouch, and dive. All actions, audio, and visual effects will reverse during time rewind as expected. This includes blood particles, bullet impacts particles, bullet trails, and damage taken. Unique combat situations arise with time reversal combat, such as not needing to reload when the bullets reenter the player's gun, damaging your opponent with bullets going backwards, and watching blood go back into your character after rewinding a bullet wound.

*Note: The proof of concept demo unfortunately only supports one player on keyboard and one player on controller*

<header id="highlights" class="major page-header"><h1><span class="number">2.</span> Highlights</h1></header>
<ul class="highlights-list">
    <li>Unique multiplayer time reversal combat
    <ul class="highlights-list sub">
        <li>Inspired by <a href="https://youtu.be/4xj0KRqzo-0?si=C0E3o7mncO0CjlLk" target="_blank" rel="noopener noreferrer">Tenet</a>, started project after walking out of the movie theatre</li>
        <li>Reversible player actions, audio, and visual effects</li>
        <li>Management of 3 independent timelines</li>
    </ul>
    </li>
    <li>Rapid 6 day development for playable proof of concept build
        <ul class="highlights-list sub">
            <li>Some shader effects are modified from previous projects (mainly from <a href="{{ site.baseurl }}/last-secutor" target="_blank" rel="noopener noreferrer">Last Secutor</a>)</li>
            <li><a href="#time-reversal" class="scrolly">Chronos</a> (framework) used to speed up development</li>
        </ul>
    </li>
    <li>Full local multiplayer <a href="#gameplay-loop" class="scrolly">gameplay loop</a>, with round logic and scoring</li>
    <li>Polished combat controls with keyboard and controller</li>
    <li>Customizable game mode through main menu UI</li>
</ul>

<header id="features" class="major page-header"><h1><span class="number">3.</span> Game Features</h1></header>

<!-- TODO: bunch of combat videos, time controls/bar mechanic -->
<header id="combat" class="page-header"><h2><span class="number">3.1</span> Time Reverse Combat</h2></header>
Each player has two buttons to control time. Pressing ```Q``` (```LT``` for controller) at any time will begin reversing the individual player's timeline and pressing ```E``` (```RT``` for controller) resumes normal forward time. Once a player begins reversing their timeline, all their previous actions will begin to playback until the beginning of the round **or** the last time the player resumed to normal time. 

Players can't input controls other than resuming to normal time while reversing. Time reversing players can still be hurt and all reversing bullets and explosions still do damage. The amount of time left for a player to reverse is represented by a draining bar in the UI when they are reversing time.
<!-- TODO: short video of time bar going down -->

Since actions and positions are always being recorded, it is possible for the computer to run out of memory if a player never rewinds time (See <a href="#time-reversal" class="scrolly">4.1 Time Reversal</a> for more implementation details). Making time reversal automatically end when a player reaches the point where they last resumed to normal time (previous timeline cache is flushed) alleviates this problem completely for most rounds. This problem can also be solved by making a maximum amount of time the player can reverse (not implemented in proof of concept demo).


<header id="gameplay-loop" class="page-header"><h2><span class="number">3.2</span> Gameplay Loop</h2></header>
The proof of concept demo has all the features for two local players to play competitively. When a player dies, world time is slowed down for dramatic effect, then time for the dead player will be rewound for 5 seconds to revive them (the other player can't move during this time for fairness). This is called a *Timeline Inversion Revive*, and each player gets one per game, indicated by a glowing red orb in the UI. Players have unlimited ammo, but limited grenades. Health, revive, and grenade pickups are spawned in random locations on the stage at random times during gameplay.

Once a player is dead with no revives, the opposing players get a point, and the next round starts when both players press ready. First to 3 points win the game. Player names (shown in score screen), number of points needed to win, and number of starting revives can all be tweaked in the main menu.

<header id="implementation" class="major page-header"><h1><span class="number">4.</span> Implementation</h1></header>
Below are a few code examples of how the time reversal effects are implemented. Since this was a proof of concept, code is not optimized and encapsulation was not prioritized.

<!-- TODO: Assigning timelines -->
<header id="time-reversal" class="page-header"><h2><span class="number">4.1</span> Time Reversal</h2></header>
To save time, I used <a href="https://ludiq.io/chronos/features" target="_blank" rel="noopener noreferrer">Chronos</a> (a deprecated framework) to keep track of time events in individual timelines. Although it works great for this proof of concept, the implementation is relatively crude, with little to no space optimization (a non-trivial problem to solve unless you are <a href="https://www.youtube.com/watch?v=8dinUbg2h70" target="_blank" rel="noopener noreferrer">Jonathan Blow </a>). The plugin comes with accurate-enough position tracking, however other time reverse effects require additional code. 

Chronos allows for time events to be scheduled into timelines, a delegate is given for the forward passage of the event, and a different delegate for the backwards passage. For example, the following is the scheduling of events for a bullet impact on a wall using the ```Do(...)``` function from Chronos, with ```time``` as one of the player's timeline:

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
*Note: ```Do``` function signature: ```Do<T>(bool repeatable, ForwardFunc<T> forward, BackwardFunc<T> backward)```*

An additional ```Plan(...)``` function is nested in the ```forward``` delegate in ```line 17```. ```Plan(...)``` is the same as ```Do(...)```, except it has an additional delay parameter to schedule it forward in time. This is useful for managing rewindable audio clips, since we can line up the backwards audio clip in the future with the length of the audio clip (```line 18```). Setting pitch to -1 in the Unity audio component plays audio backwards (```line 23```) , so we don't need to create new audio clips. All audio effects in the game are added to a timeline and reversed using this method.

<header id="bullets" class="page-header"><h2><span class="number">4.2</span> Bullets</h2></header>
<!-- TODO: short video showing bullet shooting and reversing -->
<h4>The Problem</h4>
Reversible bullets pose a unique problem since they have trails effects. Traditionally, trails are created by procedurally adding and removing vertices to generate a 2D mesh (usually as a billboard) behind a moving object; the length of the trail is determined by the speed of the projectile. 

Since I opted for a trail with a tapered end (it just doesn't look right without the tapering), simply reversing the direction of the shot projectile will not work. The procedural trail mesh will not be rendered when time reversing first starts because the initial velocity of the bullet is zero. The tapered tail will also be on the wrong side of the trail because it is dependent on the projectile's direction of travel.

<h4>The Solution</h4>
{% highlight csharp linenos %}
public IEnumerator LaunchProjectile(Vector3 bulletSpawnPosition, Vector3 direction) {
    // Launch bullet (trail head)
    bulletTimeLine.rigidbody2D.velocity = direction * weapon.launchForce;

    // cache bullet velocity for when bullet is set to normal time after rewinding
    bullet.GetComponent<BulletController>().cachedVelocity = bulletTimeLine.rigidbody2D.velocity;

    bullet.GetComponent<BulletController>().bulletForce = weapon.hitForce;

    // Trail delay
    yield return bulletTimeLine.WaitForSeconds(trailDelay);
    trail.GetComponent<TrailController>().followBullet = true;
}
{% endhighlight %}

To fix this problem, **two** invisible projectiles are launched when a player shoots. The second projectile is launched with a delay (```line 11```) and a tapered line is rendered with the two projectiles as fixed end points. Mesh vertices are generated and removed procedurally as the distance between the two projectiles change (e.g. when first projectile hits wall and stops).

This method creates the desired reversible trails by recording and reversing the positions of the two projectiles and leaving the line renderer on. There is no need to keep track of anything with the line itself, and the taper will face the right way since it only depends on the initial bullet velocity rather than the real time velocity.

<header id="grenades" class="page-header"><h2><span class="number">4.3</span> Grenades</h2></header>
<!-- TODO: Grenade reversing video -->
Reversible grenades are implemented by combining methods shown above. Grenades shoots the same bullet projectiles in random directions (to simulate shrapnel) with a reversible audio effect and sprite animation. 

To make grenades more threatening, players will take additional damage if they are within a certain radius during the explosion. If implemented naively, players can be hit through walls with this damage. To check for obstacle blocking, we first check if there are colliders within a radius using the Unity physics engine (```Physics2D.OverlapCircleAll(...)```), then we do a raycast from the centre of the explosion to the centre of each object in the radius to see if there is any stage geometry in between. This single raycast check is crude, but it suffices for most situations in this demo. 

{% highlight csharp linenos %}
public void ExplosionRadiusCheck(bool isInversed) {
    // Check for colliders in explosion radius and apply appropriate force if not blocked by stage geometry
    Collider2D[] colliders = Physics2D.OverlapCircleAll(transform.position, explosionRadius);
    foreach (Collider2D hit in colliders) {
        Rigidbody2D rb = hit.GetComponent<Rigidbody2D>();

        if (rb != null) {
            // ignore stage and this grenade in radius check
            if (rb.CompareTag("Stage") || rb == GetComponent<Rigidbody2D>()) {
                continue;
            }

            Vector2 direction = rb.transform.position - transform.position;
            float distance = direction.magnitude;
            RaycastHit2D[] rayHit = Physics2D.RaycastAll(transform.position, direction, distance);

            // Check if there is stage geometry between explosion and victim
            // Note: not a perfect check, just a single raycast
            bool blocked = false;
            for (int i = 0; i < rayHit.Length; i++) {
                if (rayHit[i].collider.CompareTag("Stage")) {
                    blocked = true;
                    break;
                }
            }

            // if not blocked by stage, apply force and damage if this is a character
            if (!blocked) {
                // if this is an inverse explosion, reverse force direction
                if (isInversed) {
                    explosionForce *= -1;
                }
                rb.AddForce(direction * explosionForce * Mathf.Lerp(1, 0, distance / explosionRadius), ForceMode2D.Impulse);

                if (rb.CompareTag("Character")) {
                    rb.GetComponent<PlayerController>().Bleed(direction, -2);
                }
            }
        }
    }
}
{% endhighlight %}
*Note: the stage raycast check loop (```line 15 — 25```) can be simplified to an if statement with a ```LayerMask``` <a href="https://docs.unity3d.com/ScriptReference/Physics2D.Raycast.html" target="_blank" rel="noopener noreferrer">raycast</a>*

Finding every collider in the radius with ```Physics2D.OverlapCircleAll(...)``` is relatively slow. It would be much faster to just raycast each player to check for distance and stage geometry at the same time. However, this was done so other physics enabled objects can also react to the explosion; such as pushing away other grenades, bullets and dropped weapons (when a player dies). Ultimately, this method performs with no issues in the limited scenarios created by two players.

