+++
title = "Overview"
weight = 5
+++

## Zola at a Glance

Zola is a static site generator (SSG), similar to [Hugo](https://gohugo.io/), [Pelican](https://blog.getpelican.com/), and [Jekyll](https://jekyllrb.com/) (for a comprehensive list of SSGs, please see the [StaticGen](https://www.staticgen.com/) site). It is written in [Rust](https://www.rust-lang.org/) and uses the [Tera](https://tera.netlify.com/) template engine, which is similar to [Jinja2](https://jinja.palletsprojects.com/en/2.10.x/), [Django templates](https://docs.djangoproject.com/en/2.2/topics/templates/), [Liquid](https://shopify.github.io/liquid/), and [Twig](https://twig.symfony.com/). Content is written in [CommonMark](https://commonmark.org/), a strongly defined, highly compatible specification of [Markdown](https://www.markdownguide.org/).

SSGs use dynamic templates to transform content into static HTML pages. Static sites are thus very fast and require no databases, making them easy to host. A comparison between static and dynamic sites, such as WordPress, Drupal, and Django, can be found [here](https://dev.to/ashenmaster/static-vs-dynamic-sites-61f).

To get a taste of Zola, please see the quick overview below.

## First Steps with Zola

Unlike some SSGs, Zola makes no assumptions regarding the structure of your site. In this overview, we'll be making a simple blog site.

### Initialize Site

> This overview is based on Zola 0.9.

```bash
$ zola init myblog
```

You will be asked a few questions.

```
> What is the URL of your site? (https://example.com):
> Do you want to enable Sass compilation? [Y/n]:
> Do you want to enable syntax highlighting? [y/N]:
> Do you want to build a search index of the content? [y/N]:
```

 For our blog, let's accept the default values (i.e., press Enter for each question). We now have a `myblog` directory with the following structure:

```bash
├── config.toml
├── content
├── sass
├── static
├── templates
└── themes
```

Let's start the Zola development server with:

```bash
$ zola serve
Building site...
-> Creating 0 pages (0 orphan), 0 sections, and processing 0 images
```

> This command must be run in the base Zola directory, which contains `config.toml`.

If you point your web browser to <http://127.0.0.1:1111>, you should see a "Welcome to Zola" message.

### Home Page

Let's make a home page. To do this, let's first create a `base.html` file inside the `templates` directory. This step will make more sense as we move through this overview. We'll be using the CSS framework [Bulma](https://bulma.io/).

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <title>MyBlog</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@0.8.0/css/bulma.min.css">
</head>

<body>
  <section class="section">
    <div class="container">
      {% block content %} {% endblock %}
    </div>
  </section>
</body>

</html>
```  

Now, let's create an `index.html` file inside the `templates` directory.

```html
{% extends "base.html" %}

{% block content %}
<h1 class="title">
  This is my blog made with Zola.
</h1>
{% endblock content %}
```