---
layout: page
title: Bloom Attenuation
description: Tech Demo
image: assets/images/bloomAttenuation.png
nav-menu: true
---

<ul class=nav>
    <li><a href="#video" class="button small scrolly">1.1 Part 1</a></li>
    <li><a href="#code" class="button small scrolly">1.2 Part 2</a></li>
</ul>

<div id="main">

<div id=video style="margin:0 auto; width:640px;">
    <iframe width="640" height="360" src="https://www.youtube.com/embed/u5lX2zunj7g" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
</div>

<div id=code style="display: block; width: 40%; margin:0 auto;">
{% highlight csharp%}
i = 0;

while (!deck.isInOrder()) {
    deck.shuffle();
    i++;
}
{% endhighlight %}
</div>

</div>
