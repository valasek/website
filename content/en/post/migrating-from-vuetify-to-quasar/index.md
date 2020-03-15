---
title: 'Migrating from Vuetify to Quasar'
subtitle: ''
summary: 
authors:
- admin
tags:
- Programming
categories:
date: "2019-06-14"
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  placement: 1
  caption: 'Image credit: **Quasar Framework**'
  focal_point: "Center"
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Both [Vuetify](https://vuetifyjs.com/) and [Quasar](https://quasar.dev/) are high quality Material Design frameworks for [VueJS](https://vuejs.org/).

This story began when the decision was made to implement a simple timesheet application. It ended with a stable application that is used daily in production. Quasar is used on the front-end and Golang with PostgreSQL on the back-end.

* * *

# TL / DR

> I was surprised at the ease of migration and the hospitality of the Quasar community. I was able to achieve exactly the same UI and functionality. The visual performance and SEO were improved as well. Hard data is mentioned in the article below.

The migration was from Vuetify 1.5.14 to Quasar 1.0.0-rc.4. [NPM(https://www.npmjs.com/get-npm)] was used as a global and local package manager. There were no changes on the back-end.

* * *

# Back to the story

So when the decision was made I looked around to find the tech stack to help me to reach the goal effectively. I also considered [Ruby on Rails](https://rubyonrails.org/) but the tables were too dynamic.

I was already familiar with [Golang](https://golang.org/) so ultimately the back-end was created in Go. Next I was looking for a framework which would help me to deliver a nice looking UI. I picked VueJS due to its fast learning curve and excellent documentation. At that time I picked Vuetify because a larger community led me to believe it would be better, as I was not experienced in Javascript and was expecting to have to do a lot of research online.

![](./quasar_vuetify.png)

# Why I switched to Quasar?

Once the application was mature and served us well, I played with an idea to improve the UI. I consider [Ant design](https://ant.design/) to be more advanced when compared to Google’s Material Design, but I did not find a suitable VueJS framework at that time. As I had been following the Quasar community for a while already, I decided to give it a go.

- I expected UI speed improvements.
- Quasar looked well-thought out and technically advanced to me.
- I wanted to learn a new framework which would give me an option to create desktop apps and well as mobile apps.
- The [Quasar documentation](https://quasar.dev/introduction-to-quasar) was the last differentiator — the content is just amazing. You should check it out!

* * *

# How I switched

I decided that I would migrate the front-end application as is was and would not add any new features. This would help me to compare the application size and performance characteristics. I generated a new empty application using the [Quasar CLI](https://quasar.dev/start/quasar-cli) (timesheet is the application name):

    $ quasar create timesheet

As a next step I copied all .vue, .js and static files into the target folder structure. I played a bit with the [Vuex](https://vuex.vuejs.org/) store and [Axios](https://github.com/axios/axios) configuration, moved parts from original Apps.vue to new layouts/MyLayout.vue file. Quasar has the concept of [QLayout](https://quasar.dev/layout/layout). Multiple pages can share the same QLayout, so the code is reusable.

> Switching for most components was as easy as replacing v- with q- at the beginning of component names and updating attributes based on Quasar documentation.

A few examples (Vuetify — Quasar)

- v-spacer — q-spacer
- v-icon — q-icon
- v-toolbar — q-toolbar
- v-toolbar-title — q-toolbar-title
- v-card — q-card
- v-expansion-panel-content — q-expansion-item
- v-select — q-select
- v-autocomplete — q-select
- v-text-field — q-input

Most of my obstacles were due to the lack of JavaScript, HTML and VueJS knowledge — but Quasar abstracted a lot of that away.

# Let’s compare the code …

## Toolbar, data table

{{< gist valasek 075d490ad38524a3b05fcc7bb578656f >}}

{{< gist valasek 6de26d2562e65dfb7525546a0679f5a2 >}}

Autocomplete

{{< gist valasek 3497af69483ad8bc0b8bd0ee565e3c47 >}}

{{< gist valasek 4eb7114ba293678f61686e4ff0a65467 >}}

* * *

> Even if the release version number for Quasar is lower when compared to Vuetify, do not worry, it has more UI components and offers similar or better component maturity.

* * *

# And the real gains?

When I look back, I have to say it was a good decision. As a recap, here is a list of benefits for my case:

- Improved performance, see Lighthouse score below.
- Reduced bundle size, compilation time and development server startup time.
- More components out of the box.
- Amazing community. One example is that I struggled with entering decimal numbers (I have to admit it was very basic issue, a missing step attribute …), anyway, I asked on the [Quasar Discord chat](https://chat.quasar.dev/) and got an answer. I created an issue [[Docs] — Reference or copy relevant HTML5 element and attributes relevant for Quasar component](https://github.com/quasarframework/quasar/issues/4321) and the same day PR was prepared by a Quasar community member to be merged into master.

* * *

# Improved performance and SEO

The data mentioned below was taken at the point in time when the back-end and front-end had the same functionality with no additional improvements or optimizations. See the code for [Quasar](https://github.com/valasek/timesheet/tree/master) and [Vuetify](https://github.com/valasek/timesheet/tree/vuetify-deprecated).

## Lighthouse score

As you can see below, the Quasar performance gain is even more relevant for complex pages.

Score on the main page without data

{{< figure src="./lighthouse_quasar_no_data.png" title="Quasar — Lighthouse score without data" >}}

{{< figure src="./lighthouse_vuetify_no_data.png" title="Vuetify — Lighthouse score without data" >}}

Score on the main page with loaded data

{{< figure src="./lighthouse_quasar_data.png" title="Quasar — Lighthouse score with data" >}}

{{< figure src="./lighthouse_vuetify_data.png" title="Vuetify — Lighthouse score with data" >}}

## Bundle size is smaller

- Vuetify — 1080 / 371 KiB
- Quasar —866 / 238 KiB

## Production build time is shorter

- Vuetify — 19 sec
- Quasar — 15 sec

## Development server startup time is shorter

- Vuetify — 24 sec
- Quasar — 14 sec

* * *

# What about you?

Share in the comments which UI framework you are using and why!

* * *

# Links

- https://quasar.dev
- https://vuetifyjs.com/en/
- https://github.com/valasek/timesheet — Quasar app
- https://github.com/valasek/timesheet/tree/vuetify-deprecated — Vuetify app
- [http://timesheet.simplesw.net:8080](http://timesheet.simplesw.net:8080) — Timesheet demo application
