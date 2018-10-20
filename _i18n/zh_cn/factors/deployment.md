如在[依赖](/dependencies)中所说，应用代码仓库应包含构建、测试以及发布时所有的依赖。

只要应用符合这个要求，那么你可以在**任何** macOS 机器上部署应用更新。

在实际工作中，部署应用更新你需要；
- 生成一个空的、临时性的容器；
- 自动安装所有依赖（如 Xcode 和 [CocoaPods](https://cocoapods.org)）；
- 运行部署脚本（如 [fastlane](https://fastlane.tools)）。

然而，由于 Xcode 必须运行在 macOS 平台，所以我们不能使用这种方法（[rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)）。在虚拟环境中运行 macOS 不光技术上存在难度，还有可能面临法律问题。有一个第三方的商业（接近开源）解决方案 [Veertu](https://veertu.com/) 可以让你在苹果的硬件上生成虚拟 macOS 环境。

近年来，一次性容器很受欢迎，其原因在于：
- 主机操作系统无需安装任何依赖，即可达到完全可重复的构建；
- 可在任何机器上运行（本地的计算机，或者任何云服务器）；
- 只有必需依赖的纯净构建。

当下，作为 iOS 开发者的我们，可以做的有：

- 使用 [xcode-install](https://github.com/krausefx/xcode-install) 自动化 Xcode 的安装过程；
- 使用 [.xcode-version 文件(https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) 指定 Xcode 的版本；
- 在配置文件中声明所有的依赖（见[依赖](/dependencies)）；
- 使用类似 [fastlane](https://fastlane.tools) 的部署工具自动化整个部署流程；
- 代码签名自动化（如 [codesigning.guide](https://codesigning.guide))；
- 经常部署，最好每周部署一次。

许多公司使用`发布列车`的概念：即一个应用发布新版本的时间表。当`发布列车`即将离开时，所有合并到主分支的代码都将被送往苹果应用商店。这种方式被大多数大型的 iOS 应用所采用。