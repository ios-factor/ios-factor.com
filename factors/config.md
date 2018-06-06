---
layout: post
permalink: config
title: Config
---

An app’s config is everything that is likely to change between deploys (App Store, TestFlight, local development) or over time without the underlying code changing. This includes:

- API keys for backend services (internal as well as external services)
- URLs for remote resources (the APIs your app uses)
- Feature toggles

Apps sometimes store config as constants in the code. This is a violation of iOS-factor, which requires **strict separation of config from code**. Config varies substantially across deploys, code does not.

A litmus test for whether an app has all config correctly factored out of the code is whether the codebase could be made open source at any moment, without compromising any credentials.

There are many ways you can inject config values during build time

- Configuration files (e.g. JSON or YAML files)
- [cocoapods-keys](https://github.com/orta/cocoapods-keys) to better hide keys and apply them to your iOS app during build time
- Custom built solution (e.g. using a build phase)

There are also techniques for providing config values at run time:

- Linking into the app with a custom url scheme
- Using a shared keychain and a separate app for configuration

As deployments on the iOS platform are significantly slower than server deployments, you might want a way to quickly update config over the air (OTA) to react to issues fast.

OTA config updates are powerful and allow you to instantly

- Run A/B tests to enable certain features or UI changes only for a subset of your active users
- Rotate API keys
- Update web hosts or other URLs that have changed
- Remotely disable features or hide buttons

Without OTA updates you have to wait for about a day for app review to accept your app. Every submission also adds the risk of being rejected and delaying the potentially urgent release.

At the same time, you might want to be backwards compatible, meaning users who can't upgrade to the most recent iOS version might not be able to install any app updates at all. By providing certain updates OTA you can keep supporting older versions of your app.

Some potential approaches when implementing OTA updates of config:

- Implement your own solution
- Proprietary web services like [Firebase remote config](https://firebase.google.com/docs/remote-config/)
