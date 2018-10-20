**版本号和编译号共同标识一个应用在苹果应用商店的特定提交：**

- 版本号（`CFBundleShortVersionString`）- 在 Xcode 中显示为 `Version`，由于用户可以看见这个版本，所以也被称作市场版本。应用在每次发布到苹果应用商店的时候必须递增版本号
- 编译号（`CFBundleVersion`）- 在 Xcode 中显示为 `Build`，也是一个递增的数字

现在在 iOS 的开发过程中，开发者没有必要自己手动更改这两个数字，而应该有一个可靠的自动化系统，用于协助更新版本号和编译号。

Xcode 有一个自带的工具叫做 `agvtool`([更多关于 agvtool](https://developer.apple.com/library/content/qa/qa1827/_index.html))，这意味着无需使用第三方工具。在首次为 Xcode 工程启用 `Versioning System` 之后，你可以使用以下命令：

```sh
# 更新版本号 (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# 更新编译号 (CFBundleVersion)
agvtool next-version -all
```

如果你正在使用 [fastlane](https://fastlane.tools) 作为部署工具，那么你可以使用 [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) 和 [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/)，将版本自动化作为部署步骤的一部分

`Fastfile` 例子：

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```