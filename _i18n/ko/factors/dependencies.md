**이상적으로, iOS-factor 앱은 시스템 패키지에 내장된 존재에 절대 의존하지 않습니다.** 그 앱은 완벽하고 정확하게 모든 디펜던시를 디펜던시 선언 매니페스트로 선언합니다. 그리고 [Xcode](https://developer.apple.com/xcode), [CocoaPods](https://cocoapods.org) 그리고 [fastlane](https://fastlane.tools)의 정확한 버전을 포함하고 있습니다.

명시적인 디펜던시 선언의 이점은 재작성이 가능한 방식으로 과거의 빌드를 다시 실행할 수 있는 신뢰도 있는 빌드 시스템을 보유하는 것 뿐만아니라 앱을 처음 사용하는 개발자의 설치 과정도 간소화하는 것입니다. 새로운 개발자는 전제 조건으로 제시된 대로 디펜던시 매니저를 설치하고 요구되는 언어만 맞춘다면 개발 기기에서 바로 앱의 코드베이스를 확인할 수 있게 될 것입니다. 또한 그들은 정해진 빌드 명령으로 앱의 코드를 실행하는데에 필요한 모든 것을 설정할 수 있게됩니다.

**특정 디펜던시를 지정하게 되면, 6개월 전의 빌드도 다시 트리거 할 수 있으며,** 그때와 동일한 Xcode, CocoaPods, Swift 버전을 사용하는 것으로 성공여부도 미리 알 수 있을 것입니다.

iOS 개발은 웹 개발처럼 컨테이너화할 수 없기 때문에, Apple이 공식 해결책을 제공하기 전까지는 요구 사항을 충족시키는 써드 파티 도구를 사용하는 것으로 제한될 것입니다. ([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712))

당분간 우리는 다양한 써드 파티 도구를 사용해서 그러한 디펜던시를 명시적으로 선언해야 합니다.

#### Swift 기반 도구

Apple이 [Swift Package Manager](https://swift.org/package-manager)에 대한 훌륭한 가이드를 제공하고 있습니다.

#### Xcode 버전 정확하게 하기

iOS 프로젝트 폴더의 루트에 있는 [.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) 파일을 사용해서 그 iOS 앱을 개발할 때 사용할 Xcode 버전을 정확히 선언할 수 있습니다.

이 방법을 사용하면, CI 시스템이 주어진 Xcode 버전을 자동으로 설치하고 사용하도록 설정할 수 있습니다.

Xcode 설치를 자동화하려면, Apple이 커맨드 라인툴을 제공하기 전까지는 써드 파티 도구인 [xcode-install](https://github.com/krausefx/xcode-install)을 사용하면 됩니다. ([rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480))

#### Ruby 기반 도구

Ruby는 [bundler](https://bundler.io)를 사용해서 정확한 디펜던시를 정의하는 `Gemfile`을 만들고 이를 빌드에 사용합니다.

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

`Gemfile`과 자동으로 생성되는 `Gemfile.lock`은 반드시 버전 컨트롤에 추가되어야 합니다. 어떤 빌드 시스템이든 Ruby 기반 빌드 디펜던시를 설치하기 위해 `bundle install`를 사용할 수 있어야 하니까요.

#### JavaScript 기반 도구

JavaScript 기반 iOS 앱(예. React Native)은 `package.json` 파일을 사용해서 필요한 모든 디펜던시를 정의합니다.

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

재생성 가능한 빌드를 위해 `package.json`은 꼭 버전 컨트롤에 추가해주셔야 합니다.
