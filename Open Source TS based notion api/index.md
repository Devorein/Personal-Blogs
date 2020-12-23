---
title: Open source ts based notion API
cover_image: https://miro.medium.com/max/4500/1*nfybRXVNYHben8gL4IQMiQ.png
tags: typescript,notion-api,notion,axios
---

# Nishan

Nishan is an open-source notion API built with typescript, axios, and node to automate almost all the CRUD functionalities the notion client provides by itself.

## Reasons

As an avid notion user and a front end developer, I’ve always wanted to automate a lot of my workflow using Notion’s native API. I have a pretty complex setup that requires a lot of manual steps, which me being a developer just could not consider as an option.

## Motivation

When I started looking for the API I was a bit surprised to find that there is none, at least by the official notion team, but plenty of open-source ones, and very few for javascript where I am most comfortable. Unfortunately, most of them supported only reading data but lacked other CRUD features. So, I decided to build one from scratch using Axios as the HTTP client and javascript.

## Stack

Writing it in plain JS seemed like a good idea initially, (as I never could have imagined I would be working on this library for over a month). But soon enough it got really out of hand and I ran into errors here and there. The most frustrating was the manual testing. i had to manually test whether all of the API methods worked properly or not, which was really not that fun. Finally, I believe after 2 weeks into it I decided to convert the whole project into typescript and never looked back since.

## Process

The first few days were incredibly rough. I had no idea what to do as I’ve never done something like this ever before. But after dabbling with the notion client for a bit, seeing each request that happens when I do something in the client and analyzing the headers, I began to grasp it little by little, and after a month of work, I am proud to say that while it’s definitely not gonna have all the features of the native API, it does provide a lot.

## Features

1. Optimal caching to reduce unnecessary requests
2. CRUD features for all types of data eg Space, User, Page, Block etc etc
3. Easy to use API providing methods for almost everything
4. Minimal setup (you only require your notion token)
5. Types to represent almost everything within notion
6. Ability to batch multiple operations and execute them later together

## Usage

Please note that this library has not been published as an npm package yet as I feel the API is still constantly evolving. So you have to clone the repo to use it.

```js
const Nishan = require("./dist");
(async(){
  const nishan = new Nishan({
    token: /* Paste your copied token here, you can obtain it from devtools > Application > Cookies > notion.so > token_v2 */,
    timeout: 500 /* Timeout between each request */
  });
  const user = await nishan.getNotionUser((user)=>user.given_name === "Safwan");
  const space = await user.getSpace((space) => space.name === `Developer`);
  const troot_pages = await space.getTRootPages((troot_page)=>troot_page.type === "page" && troot_page.properties.title[0][0] === "My Page");
  await troot_pages.page[0].delete();
})()
```

## Disclaimer

This is still a project in progress and the docs do require a lot of love. Although the API is pretty much fixed it might change drastically in the future. Please use this library with caution as you might end up manipulating your notion data in irreversible ways. Also, be on the lookout for the official API as that will definitely be a lot better than what I’ve managed myself.

## Conclusion

I know my work will become invalidated within a couple of months when the official API comes out, but this journey was a lot of fun plus I learned a ton from it. It would be wonderful if you could check it out. Any sort of feedback and suggestions is more than welcome. Thank you, cheers.

[Repo](https://github.com/Nishan-Open-Source/Nishan)

[Doc](https://nishan-docs.netlify.app/)