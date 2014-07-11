# Simple Video Posts for Jekyll Sites

## What it is

If you want to quickly post videos, it can be done with Jekyll and liquid. The code in this repository enables you to post a video just by adding the ID of a Vimeo or Youtube video to post's YAML frontmatter.

## How to use it

To do this, you need to add a variable called either `vimeo-id` or `youtube-id` to your video post's frontmatter. You also need to insert some liquid code in both `/index.html` and `/_layouts/post.html`[^1].

### YAML frontmatter

This is simple. Your YAML frontmatter should look like this for Youtube videos:

---
title: Something to dance to
layout: post
youtube-id: vctPOz4RL9g
---

Or like this for Vimeo videos:

---
title: Something to dance to
layout: post
vimeo-id: 77091919
---

### .html files

For the loop in `/index.html`, you need to fill in the following lines which check whether a variable for a video ID is present in a post's frontmatter and, if yes, inserts the corresponding embed code.

    {% if post.vimeo-id %}
      <div class="video-container">
        <iframe src="//player.vimeo.com/video/{{ post.vimeo-id }}?byline=0&amp;portrait=0" width="560" height="315" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
      </div>
    {% elsif post.youtube-id %}
      <div class="video-container">
        <iframe width="560" height="315" src="//www.youtube.com/embed/{{ post.youtube-id }}" frameborder="0" allowfullscreen></iframe>
      </div>
    {% endif %}

For `/layouts/post.html` or any other layout file, you need to change ´post.´ to ´page.´:

    {% if page.vimeo-id %}
      <div class="video-container">
        <iframe src="//player.vimeo.com/video/{{ page.vimeo-id }}?byline=0&amp;portrait=0" width="560" height="315" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
      </div>
    {% elsif page.youtube-id %}
      <div class="video-container">
        <iframe width="560" height="315" src="//www.youtube.com/embed/{{ page.youtube-id }}" frameborder="0" allowfullscreen></iframe>
      </div>
    {% endif %}

## Advantages

Compared to using the embed codes in the posts itself, this method has two main advantages:

* If you decide to change the embed code options (or if the video hoster requires you to do so), you will not have to change every single code, but only the layout files.
* Your posts also look cleaner.

## Disadvantage

The major disadvantage is that you can only have the video at a predefined location within your post. In my example files, I chose to put it between the headline / post meta data and the post content. You can, however, still use the regular way of embedding a video if you need it at a different place.

[^1]:	The same needs to be done for any other layout you created. For example, if you want to use it with pages too, you also have to add it to `/layouts/page.html`
