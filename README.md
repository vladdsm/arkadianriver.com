## Instructions to running this website

Source: arkadianriver.com:
based off the http://html5up.net/spectral design by
[@ajlkn](http://twitter.com/ajlkn).
The site is made for blog and portfolio content. The blog can contain both
personal entries and entries by syndicated authors.
The site uses jekyll, a method of creating and maintaining a web site,
which works by using local templates to generate static files that you upload
and sync with your remote site.
This repo is the same code I use for my site, excluding my posts.

### If you clone or fork this repo to use it:

0. Install [Jekyll](https://jekyllrb.com/) (version 3.1.2 or higher). DONE

0. Tweak the site to make it your own. Jekyll uses [YAML files](http://www.yaml.org/start.html)
   for its site variables:

   a. Edit the `_config.yml` file, replacing the values for each key with your info. DONE (seems to be)

   b. Add a `_data/tokens.yml` file with your IDs & mail program. **Not clear**
      See the `_data/tokens-template.yml.` file for example entries.

   c. Add author info for yourself in `_data/authors.yml` as the first
      author entry in the file.

   d. Provide your own images.
   
   e. Continue tweaking to your heart's desire, or not.

0. Create your posts:

   a. Use the posts in the 31st century as guides for yours. They're built by jekyll only when
      the `--future` option is used.  **Where should I add this option?**

   b. You can run `ruby compose.rb` to create new draft posts. 

0. Test and publish your site:

   If you're building your site on Windows (like me) and you use WinSCP to sync with your
   remote site, you can use the `site.bat` file. Set up a `_site.env` file
   as described in the comments of `site.bat` and change the excludes list for your site.

   `site dev` runs `jekyll serve --future --drafts` in development mode.  
   `site devnof` runs `jekyll serve --drafts` in development mode.  
   `site preview` runs `jekyll serve` in production mode.  
   `site prod` simply builds with `jekyll build` in production mode (no serve).  
   `site publish` uses WinSCP's `synchronize` feature to mirror to a remote site.

## Adding info from Templates - rules to build posts
---
title: Guide for new posts
categories: topics
excerpt: Front-matter guide for site pages and posts
---

## Required

### `categories`

If it's a post, the categories array is required with at least
the first element set to the permalink name of its parent page
(so that breadcrumbs work).

{% highlight yaml %}
categories: topics ...
{% endhighlight %}

The two top-level categories with provided index pages are `topics` and `works`.

If you want back/next navigation within a subcategory:

{:.nobullet}
- Create a first post for the sub-category, but with a permalink.
  The category list can be space-delimited on one line or in a bulleted list.
  Note that the category names must exactly match the permalink.

  {% highlight yaml %}
  categories: topics my-great-vacation
  permalink: /topics/my-great-vacation/
{% endhighlight %}

{:.nobullet}
- The site permalink would be:
  `/topics/my-great-vacation/index.html`

{:.nobullet}
- If your subcategory contains spaces, specify categories as an array

  {% highlight yaml %}
  categories:
    - topics
    - my great vacation
  permalink: /topics/my great vacation/
{% endhighlight %}

{:.nobullet}
- For subsequent topics in the sub-category, add the sub-category and no
  permalink:

  {% highlight yaml %}
  categories: topics my-great-vacation
{% endhighlight %}

{:.nobullet}
- resulting in: `/topics/my-great-vacation/topic-title.html`

{:.nobullet}
- Topics in the sub-category are sorted by date (and time). Therefore, if they
  all fall on the same day, specify the date in the post with a timestamp by
  which to sort.

  {% highlight yaml %}
  date: 3009-09-22 00:00:03
{% endhighlight %}


### `excerpt`

You'll probably wanna provide an excerpt in front-matter, because relying on jekyll to
get the excerpt from the body has too many caveats. The excerpt is truncated
as necessary in references, so it can be as long as you want, except that it's also
displayed, centered, right under the topic title (in all caps).

{% highlight yaml %}
excerpt: yada yada
{% endhighlight %}

### `permalink`

If it's the first page of a sub-category, use a permalink for the categories.
It becomes the index that a breadcrumb link would pop up to, ie:
`/topics/new-category/index.html`. Also see `categories`.

{% highlight yaml %}
permalink: /topics/new-category/
{% endhighlight %}

### `title`

Title for `<title/>` and `<h1/>`. For this and all other fields refer to Yaml
restrictions on when you need to quote the value.

{% highlight yaml %}
title: My interesting topic
{% endhighlight %}


## Presentation options

### `author`

If you want the article to be attributed to an author, specify a name that
corresponds to a key in the `_data\authors.yml` file.

{% highlight yaml %}
author: key_name
{% endhighlight %}

### `background-image`

If you want a larger title block with a background image, specify it here.
If it's in the `/images/` folder, specify just the name;
otherwise specify the folder relative to your jekyll root, starting with `/`.
If it's a remote image, begin the name with `//`.
Use a high resolution image, if possible,
for when viewed full screen. Once displayed, you'll wanna slowly resize your
browser or use its developer tools to see how the image responds for all `@media`
breakpoints and crop it as necessary.

{% highlight yaml %}
background-image: imagefile.png
{% endhighlight %}

### `icon`

For the featured articles on the main page, if you want an icon other than
the heart icon, specify the `font-awesome` icon identifier (just the text after `fa-`).
See the [font-awesome icons]({{ '/topics/icons.html' | prepend: site.baseurl }})
topic for a list of available icons.

{% highlight yaml %}
icon: industry
{% endhighlight %}

### `layout`

For both posts and pages, there's no need to specify the layout.
Specifying the layout is optional because defaults
are set in the `_config.yml` file to set the layout based on the folder it's in
(`_posts` or `_pages`). The layout _is_ useful for pages outside of these folders,
however.

{% highlight yaml %}
layout: {page|post}
{% endhighlight %}

### `options`

The options allow you to customize the page somewhat.

{% highlight yaml %}
options:
  - minihead      # as minimal a title as possible, and no date printed
  - fullwidth     # leaving only a tiny margin on all media sizes
  - nocomment     # disable disqus comments for this post
  - nomenu        # for pages, don't add to the menu
  - nolanding     # for pages and featured posts, don't add to the landing page
{% endhighlight %}

Note that disqus comments are not displayed on `works` posts.

## Ordering and site map options

### `changefreq`

The default change frequency for all pages in the site map is `monthly`.
Depending on how often you think you'll edit a page, you can set the page
change frequency. <a target="_blank"
href="https://www.v9seo.com/blog/2011/12/27/sitemap-xml-why-changefreq-priority-are-important/">Here's
a good guide</a> on when to use the available values.

{% highlight yaml %}
changefreq: weekly
{% endhighlight %}

### `key`

All files in the `_pages` folder are displayed in the nav menu unless you
set the `nomenu` option.
Use `key` to specify the order you want the pages listed in the nav menu.
Values are sorted in ascending order.

{% highlight yaml %}
key: 2
{% endhighlight %}

### `lastmod`, `date`

If you want the site map `lastmod` setting to be updated, you can set one or both of
these to your new modified date as `YYYY-MM-DD HH:MM:SS +/-TTTT` (`lastmod` has priority).
If you use `date`, the date shown on the page is also modified, overriding the
date in the filename. The timestamp is assumed to be UTC unless you specify the
time zone offset afterward.

{% highlight yaml %}
lastmod: 2016-03-13 23:11:00
date: 2016-01-01 00:00:00 -0800
{% endhighlight %}

### `priority`

Use `priority` to specify two things:

- the grouping in the works index
- the site map priority

{% highlight yaml %}
priority: 0.8
{% endhighlight %}

In the works index, the works are grouped by priority, listed by descending priority
and by descending date within each priority.

**Note:** For now, `works` posts _must_ have a priority set for the ordering
          to work. If you get a "`can't compare float with nil`" error in your
          jekyll build, there's a missing priority somewhere.

Because the value is used to set the site map priority,
it must be set to a value between 0 and 1.0.
I have three groups of works, using priorities 0.7, 0.6, and 0.5.
None as high as featured posts, but then, I'm not looking for a job right now. ;-)

Default priorities in the `sitemap.xml` file:

- `1.0` - Landing page
- `0.9` - Featured posts
- `0.7` - Other posts
- `0.5` - Pages

### `sitemap_exclude`

Set to `yes` if you want to exclude a page from the sitemap.

{% highlight yaml %}
sitemap_exclude: yes
{% endhighlight %}

### `tags`

For _topics_ posts, the only tag that has an effect right now is `featured`,
which adds it to the top of the `/topics/` page. The most recent eight
featured posts are also added to the main landing page.

{% highlight yaml %}
tags: featured
{% endhighlight %}

For _works_ posts, the tags become a listing of skills demonstrated. For example:

{% highlight yaml %}
tags:
  - C
  - Windows DLL
  - SGML
{% endhighlight %}

![web page display of the preceding tags]({{ '/images/skills.png' | prepend: site.baseurl }})

You can add the `featured` tag to a work if you want it to appear on the main landing page.
The `featured` tag is excluded from the list of skills on the page and `works` index.
However, its page priority overrides the standard priority of featured posts in the site map.

## CSS and Script support

### `includes`

If your page needs to include stylesheets or scripts, provide 'em as either
local or remote URLs. Prefix remote urls with `//`, not `http`. Stylesheets
are included in the header and scripts at the bottom before the body closes.

{% highlight yaml %}
style-includes:
  - /local/path/to/stylesheet.css
  - //remote.com/url/to/stylesheet.css
{% endhighlight %}

{% highlight yaml %}
script-includes:
  - /local/path/to/script.js
  - //remote.com/url/to/script.js
{% endhighlight %}

### `style, script`

These are useful when you want to embed styles and scripts outside of the
`{% raw %}{{ content }}{% endraw %}` area.
Use the yaml `|` indented block to ensure line breaks are preserved.
The styles are included in the header below stylesheet includes;
scripts are included at the bottom below script includes.

{% highlight yaml %}
style: |
  /* some css block here */
  .some-class {
    somestyle: definition;
  }
{% endhighlight %}

{% highlight yaml %}
script: |
  // some script block here...
  $(document).ready(function(){
    ...
  });
{% endhighlight %}
