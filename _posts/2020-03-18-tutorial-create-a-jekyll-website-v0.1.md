---
title: "Tutorial: Create a Jekyll-based static website from scratch"
layout: post
date: 2020-03-16 09:45
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
description: Tutorial, how to build a website using Jekyll from scratch
---

In this tutorial I will share my experience in building a static website based on Jekyll. I'm imagined this tutorial as a series of posts, to help me getting practice with content creation and Markdown. 

In the first post I will cover the following content: 

1. What is Jekyll and what are the advantages of using it
1. Create the folder structure and requirements
1. Preliminary configuration of the config.yml file
1. Summary and next post

Mainly, this tutorial represent a note to my future self, in the case that I will have to generate another website for myself (or a friend/client) in the future. As such, I hope this will represent a useful how-to guide for anyone interested in the reading. 

#### Disclaimer and requirements
The guide assumes you are using a MacOS environment, as Ruby (Jekyll's language) is pre-installed in every Mac. If you are using a different OS, you will need to find specific guides for your systems as the command we will use might change. 

## What is Jekyll and what are the advantages of using it

[Jekyll][jekyll] is  a useful way to generate static websites that can then be served by webservers such as GitHub Pages. 

Jekyll allow to generate beautiful websites without any prior coding knowledge. However, if someone is so inclined it is possible to extend its functionality with front-end frameworks and additional plugins to track, for instance, web views. 

## Requirements and  folder structure
Ok, here we go!

We need to first open our terminal and position ourselves in the directory we want to use to create our base folder. 

You can use the following command to to move around folders, create a folder and generate a file:

``` shell
$ cd [directory/folder]
$ mkdir [folder_name]
$ touch [file_name.ext]
```

We will need [Ruby gems][gems] and [Git][git]. To test wether we have them installed we can run the following commands from Terminal: 

``` shell
$ git
``` 
and
``` shell
$ gem
```

 If everything works as expected, you should see the following responses from Terminal 
 
 ![Git installed response](/assets/images/2020-03-18-tutorial/git-response.png)*This is part of the response when git is installed*

  ![Gem installed response](/assets/images/2020-03-18-tutorial/gem-response.png)*This is part of the response when git is installed*

Once the requirements are in place, we can start creating our folder. We want to run the following commands: 

``` shell
$ gem install jekyll bundler
$ bundle install 
$ jekyll new 'website_name'
```

For the last command, you want to change the name to the folder that will contain the files to build the website. I recommend having the following strucure: 

1. User/
    1. website_name
        1. website_name (this will be our working_folder)

Once the command has finished to run, we can see how the website looks like by running the following command: 

``` shell
$ bundle exec jekyll serve
```

This will create a local environment in your browser that allow us to see the changes we make to our website! Open a page in Chrome (or your favourite browser) at the address http://localhost:4000/ to see the starting version of the website. 

I know, it looks pretty bare bone and hugly but don't worry! Will make it much more appealing and pretty!

## Let's start playing around with our config.yml!

For context, the config.yml file that you find in the newly created folder is a very important file and it handles the configurations of our websites. For example, the file specifies which plugins we want to have in order to add additional functionalities to our website. 

The first tweaks we are going to make will allow us to start from scratch and create the layout the way we want it. I would recommend to use a text editor from now on. My preferred editor is [Visual Studio Code][vsc], but you can also use [Atom][atom] or any editor you like. Ok, let's dive into our config file. 

Open the file ```config.yml``` and modify the following lines:

``` yml
title: 'name of your website'
email: 'add your personal/work email'
description: 'Add the description for your website'
baseurl: '/your_website_folder'
url: 'add the future url of your website'
```
For some context, the url can be populated with a temporary place holder, if you don't have your url hosted yet, as we won't need the website live to design it!

Now, to remove the current theme, delete the line 
``` yml
theme: minima
``` 
This is the default minimal them that comes with jekyll installation. We will use our own theme. 

In the ```gems``` section add jekyll plugin [autoprefixer][apfixer]: 
``` yml
- jekyll-autoprefixer
```

We are going to use [Sass][sass] to add CSS functionalities to our website. Let's add a section at the end of the ```config.yml``` 

``` yml
sass:
  sass_dir: _sass
```

At this point, is also useful to add some prettification for future use. Have you ever notice that professional website show structured url like ```https://my_website/about``` ? We are going to prettify our website as well by hiding the file extension on the website page. 

In the section "Build settings" add the following line: 
``` yml
permalink: pretty
```

Before moving to the next step, we want to start creating some custom variables, that will be useful while building the website. We can add the following variables before the "Build settings" section:

``` yml
# these variable can be accessed using the format {{ site.myvariable }} 
twitter_path: https://twitter.com/my_twitter
facebook_path: https://facebook.com/my_facebook
instagram_path: https://instagram.com/my_instagram
youtube_path: https://youtube.com/channel/my_youtube
github_path: https://github.com/my_github
```

## Modify the Gemfile to reflect our config.yml modifications

Now that we  modified the ```config.yml``` file extensively, we want to make sure that these modifications can work properly. We need to modify our ```Gemfile``` to match the modifications we just made. 

Remove the line

``` yml
gem "minima", "~> #.#"
```

Add the line 

``` yml
gem "jekyll-autoprefixer"
```

Save the ```Gemfile```.

## Last thing before having our balnk canvas...

If we now try to reload the website in our local host you may notice that nothing has changed. This is because every time we change the ```config.yml```, we need to restart the local service to see the changes rendered. 

Before doing so, we want to delete the file in the ```_posts``` folder ```today's date-welcome-to-jekyll.markdown```. If we don't do that and try to restart the local host, we will get an error caused by the fact that we deleted the theme and thus, we won't be able to render the page. 

Let's change the ```index.md``` to ```index.html``` and add the following lines to the file: 

``` html
<h1> My Website Title <h1/>
```

Let's restart the local server and Congrats! You already have your static Home that is ready to be designed!

![Our Home MVP!](/assets/images/2020-03-18-tutorial/home.png)*Congrats! This is your first website Home page!*




[jekyll]: https://jekyllrb.com/
[gems]: https://guides.rubygems.org/what-is-a-gem/
[git]: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
[vsc]: https://code.visualstudio.com/
[atom]: https://atom.io/
[apfixer]: https://github.com/postcss/autoprefixer#other-build-tools
[sass]: https://sass-lang.com/