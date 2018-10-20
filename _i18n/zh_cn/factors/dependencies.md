**理想情况下，iOS-factor 应用使用到的系统级的依赖库不应该“不可见”。**应用应该在一张清单上完整且准确地声明所有的依赖。这些依赖包括 [Xcode](https://developer.apple.com/xcode)、[CocoaPods](https://cocoapods.org/)和 [fastlane](https://fastlane.tools/) 的准确版本。

显式声明依赖的好处在于，那些刚接触该应用的开发人员可以更便捷地完成安装及设置，同时也能拥有一个稳定的构建系统，这样历史构建也能顺利运行。新的开发人员可以将应用的代码库检出到开发机器上，而他仅需搞定语言的运行时环境，以及使用依赖管理器安装依赖。它们会使用确定好的构建命令设置好应用代码运行所需的一切。

**准确声明依赖后，你能重新触发6个月前的一次构建，并且这次构建一定会成功，**因为构建使用的 Xcode，CocoaPods 和 Swift 都是和当时一样的版本。

由于 iOS 的开发不能像 web 那样容器化，因此在苹果提供官方解决方案（[[rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)](https://openradar.appspot.com/radar?id=4929082424819712)）之前，我们只能使用第三方工具以试图满足这个需求。

目前，很多第三方工具都支持依赖的显式声明。

#### 基于 Swift 的工具

苹果提供了一个非常好的指南，即 [Swift Package Manager](https://swift.org/package-manager)。

#### 指定一个 Xcode 版本

你可以在 iOS 工程根目录的 [.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) 文件中声明 iOS 应用使用的 Xcode 版本。

这样，你就能在 CI 中配置安装及使用指定版本的 Xcode。如果需要改变 Xcode 版本（假定你已经安装），你可以使用类似 [chxcode](https://github.com/klaaspieter/chxcode) 这样的工具。

鉴于苹果没有提供官方的安装 Xcode 的命令行工具[rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480)），现在只能使用第三方工具 [xcode-install](https://github.com/krausefx/xcode-install) 自动化 Xocde 的安装。

#### 基于 Ruby 的工具

Ruby 使用 [bundler](https://bundler.io/) 在 `Gemfile` 文件中声明构建过程使用到的依赖：

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

`Gemfile` 和 `Gemfile.lock` 文件必须纳入版本控制。 有了这两个文件，任何构建系统都可以运行 `bundle install` 命令安装构建过程基于 Ruby 的依赖。

#### 基于 JavaScript 的工具

基于 JavaScript 的 iOS 应用（如：React Native）利用 `package.json` 文件声明依赖。

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

需要把 `package.json` 文件纳入版本控制才能进行可重复的构建。

