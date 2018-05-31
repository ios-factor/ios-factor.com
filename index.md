---
layout: page
title: iOS-factor
---

iOS-factor was inspired by the famous [twelve-factor app framework](https://www.12factor.net/), a methodology to write high-quality web services. iOS-factor uses the same structure and similar principles, re-written and applied to the iOS app development processes.

## Background

Over the past 10 years, the iOS development process has shifted drastically:

- from supporting a single device to a wide range of available iOS-powered iPhones and iPads and various platforms like tvOS and watchOS
- from manually including git submodules to using dependency managers
- from iOS apps mostly running locally on-device, to iOS apps heavily relying on backend services
- from iOS app review times of more than 2 weeks to less than a day
- from installing an app on your phone using iTunes to distributing apps through the official TestFlight channel
- from uploading 5 screenshots per language to iTunes Connect to 110 per language, as well as app previews
- from plain Objective-C/C++ apps to a mix of languages including JavaScript
- from slow releases whenever something is ready, to shipping every single week
- from full releases to A/B testing, slow rollouts and automatic regression detection

## What's iOS-factor?

iOS-factor is an experimental project started in May 2018. It aims to provide a collection of best practices for building high-end iOS applications. Each topic is covered by a `factor`, which describes an ideal state of how a certain category of the iOS app development process could look like. 

Due to certain limitations (like Xcode running only on macOS) not all requirements can be fulfilled. This project aims to define goals, as well as the best current approaches to solve some of the challenges we're facing.

iOS-factor is all about the bigger-picture iOS app development processes and architecture decisions and will not cover any language specific challenges.

This is a living project, maintained by the iOS developer community. You can find the full source on [GitHub](https://github.com/ios-factor/ios-factor.com) and update existing pages or add new factors.

-----

{% include all_factors_long.html %}
