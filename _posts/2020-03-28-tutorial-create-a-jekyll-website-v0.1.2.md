---
title: "Tutorial: Create a Jekyll-based static website from scratch Part 0.2"
layout: post
date: 2020-03-28 09:45
image: /assets/images/jekyll.jpg
headerImage: true
tag:
- post
- front-end
- programming
# - elements
star: false
category: blog
author: manfredimiraula
description: Tutorial, how to build a website using Jekyll from scratch, pt.2
---

In this new post we will look at our homepage, to start designing it. 

In the first post I will cover the following content: 

1. Design 101... 
1. 

#### I'm not a designer...
Yep, feel free to disagree with what I'm about to say! I'm learning the ropes of everything here, so if you have additional suggestions or better ways to do thingds, please let me know, use this Comment section!

## Design 101

I always find very useful to have a structure in my head for whatever project I'm trying to do. It works for me because having a structure, remove the fear of being blocked and not knowing where to start. What I generally do is scribble down a checklist or diagram about the initial steps I believe are needed to start. 

The initial steps don't need to be the correct ones! 

As you progress in your project, you may realize that the steps you took are not correct or should be modified. This is fine and actually part of the mastering process. Don't be afraid to start, define an MVP (Minimum Viable Product) and stick to it. You are always able to modify your project (... in most cases :) )

If you need some inspiration, you can find a number of jekyll theme templates [here][1].

## Template and fallbacks
Before starting designing all the details of our homepage and website, it's best to generate some default options that we will use throughout the website. 

I imagined this step as when I generate Python functions. The purpose of the functions is to be modular so that you can use them many times in your code while keeping the script clean. We will do the same here by creating the following folders and files: 


1. my_website
    1.  my_website_name
        1. _layouts *create this folder*
            1. ```default.html``` *store default page layouts*
        1. _includes *create this folder*
            1. ```head.html``` *store all the metas*
            1. ```js-link.html``` *store all the JavaScript functions*
        1. assets
            1. css  
                1. ```styles.sass``` 
            1. images
            1. js
                1. functions.js *contains our JavaScript functions*
        1. _sass 
            1. global *store global functions*
                1. ```dir-global.sass``` *store all the files to allow  import*
            1. modules *store small functions*
                1. ```dir-modules.sass```
            1. sections *store layout-section functions*
                1. ```dir-sections.sass```
                1. ```index.sass```
            1. ```main.sass```

Something we are going to use later on is something called [JQuery][2]. Head there and download the latest version (if the download doesn't start automatically, right-click to save as... ). Store the file under ```/assets/js```.

## _layouts
### Defaults.html
Let's edit now the files we created, starting with ```default.html``` so that we don't need to modify all the pages we will create. 

Add some basic html lines: 

``` html
<!--Specify the Doc type as well as some minimal html structure-->  
<!DOCTYPE html>
<html>
    <head>
        <!--Import config from the head.html file-->  
        {% include head.html %}
    </head>
    <body>
        {{ content }}
        <!--Import js functions-->  
        {% include js-link.html %}
    </body>    
</html>
```
## _includes
### head.html
Moving to ```head.html```, let's add the followings: 

```html
<!--The charset attribute specifies the character encoding for the HTML document.-->  
<meta charset="utf-8"> 
<!--Here we specify some compatibility settings for the user browser-->  
<meta content="IE-edge, chrome=1" http-equiv="X-UA-Compatable">
<!--Set the viewable frame for the end user-->  
<meta name="viewport" content="width=device-width, initial-scale=1">
<!--This will allow us to use the variable {{ site.description }} to import the description we added in our config.yaml file-->  
<meta name="description" content="{{ site.description }}">
<!--This will allow us to use the variable {{ site.title }} to import the title we added in our config.yaml file--> 
<title>{{ site.title  }}</title>
<!--Setting the path to the icon file that we will use to label our website--> 
<link rel="icon" type="image/x-icon" href="{{ site.baseurl }}/favicon.ico">
<!--Here we are setting our stylesheet with some css files. --> 
<link rel="stylesheet" type="text/css" href="{{ site.baseurl }}/assets/css/styles.sass">
```

I have stored two images. The icon that I want to use for my avatar and the hero for the Homepage. As a suggestion, if you can use ```.jpg``` files to avoid slowliness due to big images to be loaded. 

![Avatar](/assets/images/face.jpeg)*My face...*

![Hero](/assets/images/palermo_about_header.jpg)*Hero*

### js-link.html
This file will contain a bunch of JavaScript functions that we are going to use. We will exploit JQuery, that should now be stored in the ```asstes/js``` folder. Here, add some lines: 

``` html
<!--here we want to add the file name of the jquery file you downloaded previously. At the time of writing, the jquery version I'm using is jquery-3.4.1.min.js--> 
<script type="tex/javascript" src="{{ site.baseurl }}/assets/js/jquery-3.4.1.min.js"></script>
<!--add the link to the custom js functions--> 
<script type="tex/javascript" src="{{ site.baseurl }}/assets/js/functions.js"></script>

```
## assets
### css
We have only one file here, ```style.sass``` that will contain all our sass functions. Add the followings to import all the functions we will add to the ```main.sass``` file:
``` css
@import 'main'
```
## _sass
### /main.sass
We initially work on the ```_sass/main.sass``` file to import all the main directories from global, modules and sections. In ```main.sass```, add: 

``` scss
@import 'global/dir-global'
@import 'modules/dir-modules'
@import 'sections/dir-sections'
```
### sections/dir-sections.sass
Add the following: 
``` css
@import 'index'
```

### sections/index.sass
``` scss
// header
header.header-main
    position: relative
    z-index: 1
    // the lines below are going to set the layout for the content in the header (Guide: https://sass-lang.com/guide)
    display: flex
    flex-direction: column
    align-items:  center
    justify-content: center
    width: 100%
    height: 500px
    background: 
    // we are going to grab the image directly in the index.html file
        size: cover
        position: center center
        repeat: no-repeat
```

## Index.html
Once we save the changes we added, we want to modify the previous ```index.html``` file we created previously. This will allow all the changes to propagate fully to the wesbite. 

Add the following lines: 
``` html
---
layout: default
--- 
<header class="header-main" style="background-image:url('{{ site.baseurl }}/assets/images/palermo_about_header.jpg')">
    <!--we want to overlay our image for the header--> 
    <div class="overlay-light"></div>
    <div class="home-title">
        <h1>{{ site.title}}</h1>
        <h3>Pythonista!</h3>
    </div>
    <!--here we link the avatar to our bio, so that if someone clicks our avatar it will be redirected to the Bio description--> 
    <a href="#blurb" class="home-avatar"></a>
</header>
```

We can start modifying the Home page now!

[1]: http://jekyllthemes.org/
[2]: https://jquery.com/