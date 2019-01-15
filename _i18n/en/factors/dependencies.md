**Ideally, your build tools never rely on the implicit existence of system-wide packages.** It declares all dependencies, completely and exactly via a dependency declaration manifest. This includes the exact versions of [Xcode](https://developer.apple.com/xcode), [CocoaPods](https://cocoapods.org) and [fastlane](https://fastlane.tools).

The benefit of explicit dependency declaration is that it simplifies setup for developers new to the app, as well as having a reliable build system that is also able to run past builds again in a reproducible fashion. A new developer can check out the app’s codebase onto their development machine, requiring only the language runtime and dependency manager installed as prerequisites. They will be able to set up everything needed to run the app’s code with a deterministic build command.

**By specifying the exact dependencies you can re-trigger a build from 6 months ago, knowing that it will succeed** as it will use the same version of Xcode, CocoaPods and Swift.

Since iOS development cannot be containerized like it's already the case for web development, we're limited to third party tools trying to fulfill this requirement until Apple provides an official solution ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)). There is a 3rd party commercial (closed source) solution called [Veertu](https://veertu.com/) that allows you to generate virtual macOS environments on Apple hardware.

For the time being, you can use various third-party tooling to explicitly declare those dependencies.

#### Swift-based tooling

Apple provides an excellent guide on the [Swift Package Manager](https://swift.org/package-manager).

#### Specifying an Xcode version

You can use a [.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) file in the root of your iOS project to declare the exact version of Xcode to be used for a given iOS app.

This way, you can configure your CI-system to automatically install and use a given Xcode version. To switch the Xcode version (assuming you already have it installed), you can use a tool like [chxcode](https://github.com/klaaspieter/chxcode).

To automate the installation of Xcode, you can use the third party tool [xcode-install](https://github.com/krausefx/xcode-install) until Apple provides a command line tool to install Xcode ([rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480)).

#### Ruby-based tooling

Ruby uses [bundler](https://bundler.io) to define the exact dependencies to be used for a build in a so-called `Gemfile`:

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

The `Gemfile` and the automatically generated `Gemfile.lock` must be checked into version control. Any build system can then run `bundle install` to install all Ruby-based build dependencies.

#### JavaScript-based tooling

JavaScript based iOS apps (e.g. React Native) make use of a `package.json` file that defines all dependencies needed.

```json
{
  ...
  "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start",
    "test": "jest"
  },
  "dependencies": {
    "react": "15.4.2",
    "react-native": "0.42.3",
    ...
  }
}
```

The `package.json` should be checked into version control for reproducible builds.
