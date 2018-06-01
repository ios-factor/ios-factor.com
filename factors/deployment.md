---
layout: post
permalink: deployment
title: Deployment
---

As described in the [Dependencies](/dependencies) factor, the code repository should include all dependencies needed to build, test and release the iOS app.

As soon as your app fulfills that requirement, you can release new app updates from **any** macOS based machine.

In an ideal world, to release an app update you would

- spawn up a completely empty, temporary container
- automatically install all dependencies (e.g. Xcode and [CocoaPods](https://cocoapods.org))
- run the deployment script (e.g. [fastlane](https://fastlane.tools))

Unfortunately, due to the fact that Xcode has to run on macOS, and macOS virtualization comes with technical as well as legal challenges, we can't use this approach ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)). One third party tool that makes it possible to have consistent macOS environments is [Veertu](https://veertu.com/).

In recent years, disposable containers gained popularity for a variety of reasons:

- fully reproducible builds with zero dependencies to the host operating system
- run on any machine (your local computer, or any server in the cloud)
- a clean build with only the most necessary dependencies

Right now, the best approach we as iOS developers can take is:

- Automate the installation of Xcode using [xcode-install](https://github.com/krausefx/xcode-install)
- Make use of an [.xcode-version file](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) to specify the exact Xcode release
- Define all dependencies in configuration files (see [Dependencies](/dependencies) factor)
- Automate the complete deployment process using a deployment tool like [fastlane](https://fastlane.tools)
- Automate code signing (e.g. [codesigning.guide](https://codesigning.guide))
- Deploy often, ideally on a weekly schedule

Many companies use the concept of `Release trains`: a schedule in which a new version of your app gets released. All code that got merged into your main branch (e.g. `master` or `release`) at the time a release train "leaves" will be shipped to the App Store. This approach is implemented by most large iOS apps.
