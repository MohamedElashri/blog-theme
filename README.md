# blog-theme
My blog theme that I'm using, modifications and automatic build. 


This theme is a personal modification from the original [caffine](https://github.com/kelyvin/caffeine-theme) theme for ghost CMS

# Caffeine Theme 


## Introduction

**Caffeine Theme** is a Material Design inspired theme for the [Ghost](https://ghost.org?lmref=744)publishing platform. It originally began as a fork of [Uno-Zen](https://github.com/Kikobeats/uno-zen), but has since been drastically changed. Huge thanks to the original creator for the original theme layout and inspiration.

**The theme is super easy to configure,** with almost no code change necessary! Simply follow the customization options [below](#customizations).

You can check out the custom theme in action on my blog [Mohamed Elashri](https://melashri.xyz/blog)


### Table of Contents

- [Installation](#installation)
  - [Option 1](#option-1)
  - [Option 2](#option-2)
  - [Add JQuery and other libraries](#add-jquery-and-other-libraries)
- [Customizations](#customizations)
  - [General Settings](#general-settings)
  - [Number of Posts](#number-of-posts)
  - [Header icon](#header-icon)
  - [Favicons](#favicons)
  - [Tags Overlay](#tags-overlay)
  - [Google Analytics](#google-analytics)
  - [Disqus Comments](#disqus-comments)
  - [Masonry Grid Layout (beta)](#masonry-grid-layout-beta)
  - [Mailchimp](#mailchimp)
  - [Toast Notifications](#toast-notifications)
  - [Cover](#cover)
    - [Cover title](#cover-title)
    - [Cover subtitle](#cover-subtitle)
    - [Disable Cover](#disable-cover)
  - [Links](#links)
  - [Browser Compatibility Page](#browser-compatibility-page)
  - [Custom static pages](#custom-static-pages)
  - [Social Networks](#social-networks)
  - [AMP Support](#amp-support)
 
## Installation

You can install this theme in one of three ways, but the two options require `git`.

### Option 1

Enter the theme folder (`content/themes`) of your Ghost installation and paste the following command:

```bash
$ git clone https://github.com/MohamedElashri/blog-theme
```

### Option 2

If you have your Ghost blog hosted on git and you want to continuously get the latest updates, you can add this repo as a submodule. Create a `.gitmodules` file in your root Ghost installation and add the following like so:

```
[Submodule "content/themes/theme"]
      path = content/themes/theme
      url = https://github.com/MohamedElashri/blog-theme.git
 ```

## Customizations

As mentioned earlier, this theme is very easily configurable to suit your needs. Every feature of the theme that you can easily customize will be listed below.

### General Settings

Make sure to set up some of your default settings within your Ghost Admin panel → `General`. By setting your blog title, description, cover, logo, and posts per page, you will be able to maximize the capabilities of this theme.

### Number of Posts

With ghost migrating to v1, to set the number of posts per page, you'll have to configure a file within the theme directly. The configuration is set within the `package.json`. To adjust it, you'll need to modify the following:

```javascript
"config": {
    "posts_per_page": 6
}
```

### Header icon

On every page there is an icon on the upper-left hand corner that will open the splash screen. If you'd rather set your own icon, overwrite the `icon.png` within `assets/img/icon`. Or, if you rather not use an icon, you can simply open up the `partials/header.hbs` and uncomment the following line:

```html
<img src="{{@blog.logo}}" alt="{{@blog.title}} avatar" class="avatar rounded hvr-buzz-out" />
```
and delete the following line:

```html
 <img src="{{asset "img/icons/icon.png"}}" alt="{{@blog.title}} icon" class="icon rounded hvr-buzz-out" />
```

### Favicons

Create your favicons with [Favicon Generator](http://realfavicongenerator.net/) and place them in in `assets/img/icons` or whatever folder you feel comfortable with.

### Tags Overlay

To purpose of the tags overlay is to display a list of popular tags that you want your users to easily find and navigate to. You can continuously add to this list to create an "infinite" list of tags.

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var tag_names = ['code', 'career'];
</script>
```

*Note: Ghost currently does not have a "production" ready feature to easily find your list of tags, so this is the temporary solution until that feature is more broadly supported.*

### Google Analytics

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var ga_id = 'UA-YOUR_ID_HERE';
</script>
```

### Disqus Comments

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var disqus_shortname = 'YOUR_DISQUS_SHORTCUT_HERE';
</script>
```

### Masonry Grid Layout (beta)

By default this theme will create a two column grid layout if you decided to import the Masonry package as described in the [instructions above](add-jquery-and-other-libraries). If you didn't import the package, the theme will render a single column grid.

You can customize the number of columns you'd like your home page to render by simply specifying the number in the following option.

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var gridOptions = {
    columns: 3
};
</script>
```

This will change the theme to use a 3 column grid. Feel free to experiment the grid columns with the number of posts you want to show on each page to get the experience that you want!

*Note: This feature is still somewhat experimental and you may see some jumpy animations*

### Mailchimp

This theme easily enables you to create a Mailchimp subscription sign-up. We are using [Hello Byte's subbscribe](https://github.com/shlomnissan/subbscribe) library to create an opt-in popup form. Due to its lack of support for a package manager, I have included its assets as part of this project. I will try to keep that updated regularly as needed.

To enable this feature, you'll need to obtain your Mailchimp embed signup form action URL, which is documented [here](http://kb.mailchimp.com/lists/signup-forms/host-your-own-signup-forms). Then inject it into your blog header like the example below.

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var mailchimpOptions = {
    url: "//1bytebeta.us9.list-manage.com/subscribe/post?u=1c261e60d8259c0c636801494&amp;id=7fa99bf359"
};
</script>
```

You **must** set the `url` option for the subscribe button to appear properly. Otherwise, you can modify the contents of the subscribe button by simply adding more options to `mailchimpOptions`. The following list of options are supported and you can edit them to your liking:

```javascript
var mailchimpOptions = {
    url: "//1bytebeta.us9.list-manage.com/subscribe/post?u=1c261e60d8259c0c636801494&amp;id=7fa99bf359",
    title: "Never miss a post!",
    text: "Stay up to the date with the latest posts from Caffeine Coding!",
    name: "<a href='https://www.facebook.com/caffeinecoding' target='_blank'>@caffeinecoding</a>",
    color: "#56817A",
    thumbnail: "http://i.imgur.com/39erIwp.png"
};
```

### Toast Notifications

This theme has support with [toastr](https://github.com/CodeSeven/toastr) to create custom notifications on your blog for your users to see. You can configure the notification through the Ghost admin panel, as seen in the example below:

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var notificationOptions = {
    type: "info",
    message: "I want to show this message",
    isShownOnce: true,
    escapeHtml: false
};
</script>
```

The `type` will define the type of notification to render, the `message` will display the message to render, `escapeHtml` will specify whether to escape the message to render HTML, and `isShownOnce` will set whether to only show our users the notification once.

**Note**: `isShownOnce` will be determined by setting a value in local storage that is set to the `message`. So if your message changes, the local storage value will be set to the new message. We determine whether to show the notification based on whether the current notification message is equal to their last visit.

### Cover

Go to Ghost Admin panel → General → `Blog Cover`

#### Cover title

By default, the title that you see in the cover page of your blog is extracted from your blog settings (Admin panel → Blog Title).

If you want to customize it, you can do it like so:

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var profile_title = 'Caffeine Theme';
</script>
```

#### Cover subtitle

The purpose of the subtitle is to describe your bio in a quick phrase.

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var profile_resume ='Software Engineer';
</script>
```

#### Disable Cover

If you'd like to disable the cover and go directly to the home page, you can simply add the following code to the code injection.

Go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
var disableCover = true;
</script>
```

### Links

Go to Ghost Admin panel → `Navigation` and add/edit items.

The "Home" link is always included by default, so you don't need to add it manually.

### Browser Compatibility Page

This theme includes a special browser compatibility page for users who use IE9 and below. You can enable it by creating a static page with the post url as `browser-compatbility`, as seen in the example below.

![](http://i.imgur.com/unIDJxOl.png)

### Custom static pages

Check out the official [documentation](http://themes.ghost.org/docs/page-context) on Ghost.org.

### Social Networks

To manage your social networks, you'll need to provide a custom config option. 

For Facebook and Twitter links, go to Ghost Admin panel → General → `Social accounts`.
For LinkedIn and Github links, go to Ghost Admin panel → `Code Injection` → `Blog Header` and add:

```html
<script>
    var socialConfig = {
        facebook: {
            title: "Caffeine Coding on Facebook"
        },
        twitter: {
            title: "@KelyvinN on Twitter"
        },
        linkedIn: {
            link: "https://linkedin.com/in/kelyvin",
            title: "Kelyvin on LinkedIn"
        },
        github: {
            link: "https://github.com/kelyvin",
            title: "Kelyvin on Github"
        }
    };
</script>
```

If you don't provide a config for any of these, they will automatically be omitted. If you want other social links besides these four, you'll have to get your hands a little dirty. You can edit the file `partials/social.hbs` with all the social networks you want to show, following the same HTML markup pattern that you see. You can find the right social icon for you by searching through [Font Awesome's icon list](http://fontawesome.io/icons/).


### AMP Support

As of Ghost v0.10.0, Ghost supports and will automatically render AMP (accelerated mobile pages) versions of your posts. You can read more about the [AMP project here](https://www.ampproject.org/).

Included in this theme is an `amp.hbs` file that represents the AMP template. This template is simply a clone of [Ghost's default template](http://themes.ghost.org/v0.10.0/docs/amp) but with some some slight modifications to better fit the style of this theme.

For example, if you'd like to change the default header color to match your theme's default color, simply open up `amp.hbs` and modify the following line with the HEX color of your choice:

```CSS
.main-header {
    ...
    background: #56817A no-repeat center center;
    ...
}
```

To see how the AMP version of a post looks, append `/amp` to the end of the URL of your post. So if you had a blog post with the url: `https://www.melashri.xyz/blog/example/`, it's AMP equivalent would be: `https://www.melashri.xyz/blog/example/amp`.
