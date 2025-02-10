---
layout: splash
title: Rōger Nōden
permalink: /
hidden: true
header:
  overlay_color: #"#FFF" # "#5e616c"
  overlay_image: /assets/images/home-page-image.png
  actions:
    # - label: "<i class='fas fa-download'></i> Install now"
    #   url: "/docs/quick-start-guide/"
excerpt: >
  Vice President of Software Engineering, Aspiring Film Director, Adventurer, Husband.<br/> 
  Software, Movies, Electric Vehicles, Cooking, BBQ, Outdoors, Music.<br/>
  He/him/his &mdash; Gay.<br/>
  Minnesota, USA
feature_row:
  - image_path: assets/images/etienne-girardet-EP6_VZhzXM8-unsplash-2.jpg
    image_caption: Photo by [**Etienne Girardet** on Unsplash](https://unsplash.com/@etiennegirardet?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)
    alt: "writings"
    title: "Writings &amp; Posts"
    excerpt: "Blog posts from your's truely."
    url: "/posts"
    btn_class: "btn--primary"
    btn_label: "Read more"
  - image_path: assets/images/josh-eckstein-VAJEea9u6k8-unsplash.jpg
    image_caption: Photo by [**Josh Eckstein** on Unsplash](https://unsplash.com/@dcejoshe?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)
    alt: "projects"
    title: "Projects"
    excerpt: "Film and software projects I've worked on that might be interesting."
    url: "/projects"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - image_path: assets/images/martin-shreder-5Xwaj9gaR0g-unsplash.jpg
    image_caption: Photo by [**Martin Shreder** on Unsplash](https://unsplash.com/@martinshreder?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash)
    alt: "about"
    title: "About"
    excerpt: "Every good project has an About page, check out what makes this site tick!"
    url: "/about"
    btn_class: "btn--primary"
    btn_label: "Learn more"      
---

## Recent Posts

{{< mdl-disable "<!-- markdownlint-disable MD033 -->" >}}
<div class="feature__wrapper">
{% for post in site.posts limit:3 %}
  {{< mdl-disable "<!-- markdownlint-disable MD033 -->" >}}
  <div class="feature__item">
    {% include archive-single.html type="" %}
  </div>
{% endfor %}
</div>

## Dig Deeper

{% include feature_row %}
