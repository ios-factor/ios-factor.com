---
layout: post
permalink: dev-prod-parity
title: Dev/Prod Parity
---

Historically, there has been substantial gaps between development (a developer making live edits to the app on their local machine) and production (an app deployed on the App Store accessed by end users). These gaps manifest in three areas:

- **The time gap:** A developer may work on code that takes days, weeks, or even months to go into production
- **The personnel gap:** All iOS developers write code, just one person knows how to deploy the app
- **The tools gap:** Developers may be using a staging server that runs a different version than the production one. Developers might be using a different Xcode release than the one that was used for deployment

**An iOS-factor app is designed for [continuous deployment](https://avc.com/2011/02/continuous-deployment/) by keeping the gap between development and production small.** Looking at the three gaps described above:

- Make the time gap small: a developer may write code and have it deployed just a few days later
- Make the personnel gap small: developers who wrote code are closely involved in deploying it and watching its behavior in production. This is best possible by completely automating the release process of your iOS app and put the know-how on how to do it in code declarations instead of documentation.
- Make the tools gap small: keep development and production as similar as possible. Follow the principles of the [Dependencies](/dependencies) factor of iOS-factor and make use of a `.xcode-version` file as well as define all other dependencies explicitly.

Summarizing the above into a table:

|          | Traditional iOS app | iOS-factor app |
|----------|---------------------|----------------|
| Time between deploys | Months  | Days           |
| Code authors vs code deployers | One person knows how to deploy | Deployment is automated, ideally on a server |
| Dev vs production environments | Divergent |  As similar as possible |
