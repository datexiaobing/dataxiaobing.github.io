---
layout: post
title:  实验代码（二）
author: wb zhang
tags:
- jekyll theme
- jekyll
date: 2023-05-28 13:56 +0800
---

# codes two

## scroll.html
````html
   <script>
    function strip(str, remove) {
        while (str.length > 0 && remove.indexOf(str.charAt(0)) != -1) {
        str = str.substr(1);
        }
        while (str.length > 0 && remove.indexOf(str.charAt(str.length - 1)) != -1) {
        str = str.substr(0, str.length - 1);
        }
        return str;
    }

    function scroll() {
        console.log('scroll');
        window.scrollTo({
        left: 0, 
        top: window.innerHeight,
        behavior: 'smooth'
        });
        sessionStorage.removeItem('forceCheckScroll');
    }

    const forceCheckScroll = sessionStorage.getItem('forceCheckScroll') === 'true';
    const checkScroll = strip(window.location.pathname, '/') !== strip('{{ site.baseurl }}', '/');

    if (forceCheckScroll || checkScroll) {
        const maxWidth = "(max-width: 48rem)";
        const result = window.matchMedia(maxWidth);
        if (result.matches) {
        scroll();
        } else {
        result.addListener((match) => {
            if (match.media == maxWidth) {
            if (match.matches) {
                scroll();
            }
            }
        });
        }
    }
    </script>

````

##  home-header.html
    ````html
        <div class="home-header pure-menu pure-menu-horizontal">
    <div class="home-header-bar">
        {% if site.data.archive %}
        <ul class="home-header-menu pure-menu-list">
        {% for item in site.data.archive %}
            <li class="pure-menu-item">
            <a href="{{ item.url | relative_url }}" class="pure-menu-link {% if page.url == item.url %}current-item{% endif %}"">{{ item.title }}</a>
            </li>
        {% endfor %}
        </ul>
        {% endif %}
    </div>
    </div>
    ````
