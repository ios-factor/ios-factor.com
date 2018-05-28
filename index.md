---
layout: page
title: iOS-factor
---

iOS-factor was inspired by the famous [twelve-factor app framework](https://www.12factor.net/), a methodology to write high-quality web services. iOS-factor uses the same structure and similar principals, re-written and applied to iOS apps.

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

This project describes the ideal state of how the iOS app development process should look like. Due to certain limitations (like Xcode requiring macOS) not all requirements can be fulfilled. This project aims to define a goal, as well as the best current approaches to solve some of the challenges.

iOS-factor covers the bigger-picture iOS app development processes and architecture decisions and will not cover any language specific challenges.

-----

{% include all_factors_long.html %}
