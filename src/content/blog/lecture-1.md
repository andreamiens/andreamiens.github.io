---
author: Andréa Miens
pubDatetime: 2023-10-03T15:57:52.737Z
title: Homework 1 - Affordance, Getstalt Law and Darkscheme
postSlug: lecture-1-2-3
featured: true
ogImage:
tags:
  - lecture
description: Affordance, Getstalt Law and Darkscheme around me
---

Astro 2.0 has been released with some cool features, breaking changes, DX improvements, better error overlay and so on. AstroPaper takes advantage of those cool features, especially Content Collections API.

<!-- ![Introducing AstroPaper 2.0](https://user-images.githubusercontent.com/53733092/215683840-dc2502f5-8c5a-44f0-a26c-4e7180455056.png) -->

![Introducing AstroPaper 2.0](https://user-images.githubusercontent.com/53733092/215771435-25408246-2309-4f8b-a781-1f3d93bdf0ec.png)

## Table of contents

## A quick reminder of the concepts

>"An affordance is a relationship between the properties of an object and the capabilities of the agent that determine just how the object could possibly be used." 
- Don Norman

Definition : Affordance is the characteristic of an object or environment that suggests to its user its mode of use or other practice. In other words, the way in which the object suggests its use. The term originated in psychology, and is used in ergonomics by way of a glossary of meanings.

## An exemple of a good affordance

Here's a good example of affordance, this push button. I see this push button on a regular basis. It's located on the doors of public transport trains. What's good about it? First of all, it's well located because it's on the object it sets in motion, i.e. the door. What's more, the luminous green circle highlights the pressable part of the button. So the user knows directly where to press to set the door in motion. The button also provides additional information on door movement. The arrows engraved on it show the user how the doors will move. The fact that the arrows are not just drawn, but embossed, means that they can also be used by blind people. A simple but well thought-out button! 

## An exemple of a terrible affordance 

What's wrong with this cute little lamp? Can't you see? Well, that's normal! This lamp is activated by touch, but there's nothing to indicate it! You immediately want to look for the activation button you'd normally find. The fact of touching the lamp is in no way communicated by the object, so by definition it's a poor affordance of the object. To improve affordance, we could simply engrave a small light bulb to make people want to touch it and activate the lamp.


## Features & Changes

### Type-safe Frontmatters and Redefined Blog Schema

Frontmatter of AstroPaper 2.0 markdown contents are now type-safe thanks to Astro’s Content Collections. Blog schema is defined inside the `src/content/_schemas.ts` file.

### New Home for Blog contents

All the blog posts were moved from `src/contents` to `src/content/blog` directory.

### New Fetch API

Contents are now fetched with `getCollection` function. No relative path to the content needs to be specified anymore.

```ts
// old content fetching method
- const postImportResult = import.meta.glob<MarkdownInstance<Frontmatter>>(
  "../contents/**/**/*.md",);

// new content fetching method
+ const postImportResult = await getCollection("blog");
```

### Modified Search Logic for better Search Result

In the older version of AstroPaper, when someone search some article, the search criteria keys that will be searched are `title`, `description` and `headings` (heading means all the headings h1 ~ h6 of the blog post). In AstroPaper v2, only `title` and `description` will be searched as the user types.

### Renamed Frontmatter Properties

The following frontmatter properties are renamed.

| Old Names | New Names   |
| --------- | ----------- |
| datetime  | pubDatetime |
| slug      | postSlug    |

### Default Tag for blog post

If a blog post doesn't have any tag (in other words, frontmatter property `tags` is not specified), the default tag `others` will be used for that blog post. But you can set the default tag in the `/src/content/_schemas.ts` file.

```ts
// src/contents/_schemas.ts
export const blogSchema = z.object({
  // ---
  // replace "others" with whatever you want
  tags: z.array(z.string()).default(["others"]),
  ogImage: z.string().optional(),
  description: z.string(),
});
```

### New Predefined Dark Color Scheme

AstroPaper v2 has a new dark color scheme (high contrast & low contrast) which is based on Astro's dark logo. Check out [this link](https://astro-paper.pages.dev/posts/predefined-color-schemes#astro-dark) for more info.

![New Predefined Dark Color Scheme](https://user-images.githubusercontent.com/53733092/215680520-59427bb0-f4cb-48c0-bccc-f182a428d72d.svg)

### Automatic Class Sorting

AstroPaper 2.0 includes automatic class sorting with [TailwindCSS Prettier plugin](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)

### Updated Docs & README

All the [#docs](https://astro-paper.pages.dev/tags/docs/) blog posts and [README](https://github.com/satnaing/astro-paper#readme) are updated for this AstroPaper v2.

## Bug Fixes

- fix broken tags in the Blog Post page
- in a tag page, the last part of the breadcrumb is now updated to lower-case for consistency
- exclude draft posts in a tag page
- fix 'onChange value not updating issue' after a page reload
