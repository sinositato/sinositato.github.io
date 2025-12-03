---
layout: post
title: "My Brief Journey Setting Up GitHub Pages"
date: 2025-12-03 +0800
categories: blog
---

# How I Finally Set Up My GitHub Page (and the Weird Little Problems Along the Way)

So… I finally stood up my GitHub Page.  
It’s funny because it’s supposed to be *the easiest way to host a static site*, and yet I still managed to trip over half the usual landmines—Jekyll versions, Gemfiles, layouts, posts not showing up, and figuring out where things actually go.

This post is basically the behind-the-scenes of that whole scramble.
<!--more-->
---

## Why I Even Wanted a GitHub Page

I just wanted a simple, clean place to host my blog—nothing heavy, nothing overly-designed, and definitely nothing I’d have to babysit. GitHub Pages made sense:

- Free hosting  
- Automatic builds  
- Custom domain support  
- Jekyll built-in  

Perfect… theoretically.

---

## The Ruby Problem (aka: “I Don’t Know This Language at All”)

Let me be straight:  
**I’m not familiar with Ruby. At all.**

I know just enough to recognize a Gemfile when I see one… but not enough to know why it sometimes behaves like it has a personality disorder.

So when the Gemfile threw errors?  
Or when Bundler yelled at me about locked versions?  
Or when `bundle exec jekyll serve` refused to behave?

Yeah — that definitely added friction.

Once I realized GitHub Pages locks you into its own Ruby/Jekyll ecosystem, things clicked into place. The fix wasn’t “debug the Gemfile” — it was “stop overthinking and stick to the supported versions.”

Simplifying to this finally worked:

```ruby
source "https://rubygems.org"

gem "minima", "~> 2.0"
gem "github-pages", "~> 232", group: :jekyll_plugins
````

Basically:
Don’t fight Ruby. Let it win.

---

## The “Where Do I Put My Posts?” Moment

Yes, I technically *knew* posts belong in `_posts`.
But the real confusion was why nothing appeared.

Turns out:

1. The file goes inside `_posts/`
2. It must be named `YYYY-MM-DD-title.md`
3. It needs proper frontmatter

Once that clicked, the posts finally showed up on the site.

---

## Listing the Posts on the Homepage

This one made me pause. Where exactly does the Liquid loop go?
Answer: your homepage file (`index.md` or `index.html`).

```liquid
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>
```

Simple, but not obvious when you’re staring at a blank repo.

---

## Adding an About Page

This part was surprisingly painless:

Create `about.md`:

```yaml
---
layout: page
title: About
permalink: /about/
---
```

Drop your content under it.
Done.

---

## The “Publish on Root” Episode

There was a moment where GitHub Pages kept serving the default placeholder instead of my real site.
Fixing it meant changing the Pages config:

**Settings → Pages → Build and deployment → Source**

* Branch: `main`
* Folder: `/ (root)`

Instantly solved.

---

## The Meta Part: Debugging the Blog While Building the Blog

The entire experience became unintentionally meta.
Half the time I was building the blog, I was also asking questions about how to fix the blog:

* “How do I list my posts?”
* “Where do I paste this code?”
* “Why isn’t GitHub detecting my posts?”
* “Why isn’t the theme loading?”
* “Where do I place layouts and loops?”

It felt like playing an instrument you don’t fully know yet:
you hit the chord wrong, adjust a finger, hit it again — suddenly it works.

---

## Final Thoughts

GitHub Pages is easy **after** you know the rules:

* Don’t fight Ruby if you’re not a Ruby dev
* Let GitHub Pages dictate the Jekyll versions
* Keep your folder structure clean
* Name your posts correctly
* Add frontmatter properly
* Use Liquid where the theme expects it
* Make sure you’re deploying from root if you want a root site

Once the puzzle pieces locked in, everything became smooth.
Now the site is live, and I finally get to focus on writing instead of wrestling with Bundler.