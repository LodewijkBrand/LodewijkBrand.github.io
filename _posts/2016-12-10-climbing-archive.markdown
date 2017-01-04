---
layout: post
title:  "Climbing Pictures from the Archives"
date:   2016-12-10 22:04:31 -0800
categories: jekyll update
images:
  - image_path: /images/climbing/castaway.jpg
    title: Castaway Dyno - Chattanooga, Tennessee
    caption: Trying a finicky dyno in Little Rock City outside of Chattanooga, Tennessee
  - image_path: /images/climbing/atari.jpg
    title: The Atari Boulder - Bishop, California
    caption: On a spring break trip in Bishop with a few friends from college climbing something that looks a lot like the Atari logo...
  - image_path: /images/climbing/black_mountain.jpg
    title: Black Mountain - Idyllwild, California
    caption: My first trip outside in Southern California after moving to San Diego from Colorado
  - image_path: /images/climbing/topout_lrc.jpg
    title: Little Rock City - Chattanooga, Tennessee
    caption: Great photo of an unnamed topout in Tennessee
  - image_path: /images/climbing/the_ladder.jpg
    title: The Ladder - Mount Evans, Colorado
    caption: One of my all time favorites in the picturesque valley of Mount Evans, Colorado
---

<ul class="photo-gallery">
  {% for image in page.images %}
    <div style="display:block; margin-left: auto; margin-right: auto; text-align:center;">
      <img src="{{ image.image_path }}" alt="{{ image.title }}"/>
      <p>{{ image.caption }}</p>
    </div>
  {% endfor %}
</ul>
