# Simple Video Posts for Jekyll Sites

## Introduction

The code in this repository enables you to create video posts by adding the ID of a Vimeo or Youtube video to the post's front matter.

## Getting started

To do this, you need to add a variable to your post's front matter. Depending on site it has to be called `vimeo-id` or `youtube-id` followed by the video's ID. You also need to insert a few lines of liquid code in both `/index.html` and `/_layouts/post.html` which will read the variable and insert the videos' embed code. The same needs to be done for any other layout you are using. If for example you want to use videos with pages too, you also have to add it to `/layouts/page.html`.

### YAML frontmatter

Your YAML frontmatter should look like this for Youtube videos:

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

SCNR.

### Template and layout files

For the loop in `/index.html`, you need to fill in the following lines. The snippet checks whether a video ID is present in the post's front matter and, if yes, inserts the corresponding embed code (which you can tweak to your liking).

    {% if post.vimeo-id %}
      <div class="video-container">
        <iframe src="//player.vimeo.com/video/{{ post.vimeo-id }}?byline=0&amp;portrait=0" width="560" height="315" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
      </div>
    {% elsif post.youtube-id %}
      <div class="video-container">
        <iframe width="560" height="315" src="//www.youtube.com/embed/{{ post.youtube-id }}" frameborder="0" allowfullscreen></iframe>
      </div>
    {% endif %}

For `/layouts/post.html` or any other layout file, you need to change `post.` to `page.`:

    {% if page.vimeo-id %}
      <div class="video-container">
        <iframe src="//player.vimeo.com/video/{{ page.vimeo-id }}?byline=0&amp;portrait=0" width="560" height="315" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
      </div>
    {% elsif page.youtube-id %}
      <div class="video-container">
        <iframe width="560" height="315" src="//www.youtube.com/embed/{{ page.youtube-id }}" frameborder="0" allowfullscreen></iframe>
      </div>
    {% endif %}

I have added two complete example files to the repository.

## Advantages compared to regular embeds

Compared to using the embed codes in the posts itself, this method has two main advantages:

* If you decide to change the embed code (or if the video hoster requires you to do so), you will not have to change every single post, but only the template/layout files.
* Your posts will look cleaner.

## Disadvantages compared to regular embeds

The major disadvantage is that you can only have the video at a predefined location within your post. In the example files, the videos are inserted between the headline and the content. For most use cases, this should be an acceptable solution.You can, however, still use regular video embeds if you need it at a different place.
