---
layout: post
permalink: app-versioning
---

**Version and the build numbers work together to uniquely identify a particular App Store submission for an app:**

- Version number (`CFBundleShortVersionString`) - shown as `Version` in Xcode, also called the marketing version: The version that's visible to the end-user, it has to be incremented on each public App Store release
- Build number (`CFBundleVersion`) - shown as `Build` in Xcode: an incrementing number

In today's iOS development processes there is no reason you should manually change those numbers. Instead, you want a reliable and automated system taking care of keeping the versions up to date.

There is no need to use third-party tools, Xcode has a tool called `agvtool` built-in. ([more details](https://developer.apple.com/library/content/qa/qa1827/_index.html))

After initially enabling the `Versioning System` for your Xcode project, you can use the following commands:

```sh
# Update the version number (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# Update the build number (CFBundleVersion) to the next one
agvtool next-version -all
```

If you use the deployment tool _fastlane_ you can use [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) and [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/) to automate the version bump as part of your deployment step

Example `Fastfile`:

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
