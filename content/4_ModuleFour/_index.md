---
title: "Getting Familiar With Setup"
chapter: true
weight: 4
---

# Getting Familiar With Setup

- Setup Architecture
- Login to the environment
- Post modernization using CloudHedge OmniDeq<sup>TM</sup>

<!-- ### Markdown and Shortcode Resources
{{% notice tip %}}
The following links are your go-to resource for markdown and shortcode reference in building your workshop: <br>
* Markdown cheat sheet https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet <br>
* Learn theme markdown https://learn.netlify.app/en/cont/markdown/ <br>
* Menu extras and shortcuts https://learn.netlify.app/en/cont/menushortcuts/ <br>
* Using Font Awesome Emoji's <i class="fas fa-heart"></i> https://learn.netlify.app/en/cont/icons/ to help your page pop <i class="fas fa-glass-cheers"></i>
{{% /notice %}}

### Adding Images and Static Media
Any images and static media to be included in the workshop need to be placed in the `static/images` folder. The format to display an image is as follows: `![Alternate Text](/images/imagename.jpg)` <br>

For example, the markdown for this dog is `![An adorable puppy](/images/dog.jpg)` and the image is in the `static/images` folder. <br>
![An adorable puppy](/images/dog.jpg)

### Creating Links
The format for creating links is `[Link Display Text](http://example.com)`. For example, this link [Hugo Framework](https://gohugo.io/about/what-is-hugo/) was created using `[Hugo Framework](https://gohugo.io/about/what-is-hugo/)`.

### The "More" Menu Section
This section of the menu on the left is designed to add additional resources that are related to the workshop but not necessarily part of the workshop itself. To modify these links, edit the sections marked `[[menu.shortcuts]]` in the `config.toml` located in the root folder. The "name" portion will be what is displayed in the menu. The "url" should be the address of the link. The "weight" setting will adjust the display order, similar to the other "weight" settings utilized in indexes and modules mentioned previously.

### Ensuring Pages Appear In Both Setup Versions
A shortcut to creating the workshop with different setup versions is utilizing the localization functionality of Hugo. By adding a secondary extension to the filename, this file will be included in the specific version of the workshop. Currently, the base utilizes the format `*.ee.md` to signify that the page is to be used in the AWS EventEngine setup. Much of the time, the files will be the same as the content only differs at specific points. It is necessary to add them, however, to make sure that the common content is duplicated across both versions. If you wish to change the secondary extension or default version, this can be done in the `config.toml` file in the heading and `[Languages]` sections. -->