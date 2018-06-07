**버전과 빌드 넘버는 함께 작용해서 App Store에 제출되는 앱의 희귀하게 확인할 수 있게 해줍니다.**

- 버전 넘버 (`CFBundleShortVersionString`) - Xcode에서 `Version`으로 보여지고, 또한 마케팅 버전으로 사용되기도 합니다. 이 버전은 엔드 유저에게 보여지고, 일반적인 App Store 릴리즈에서는 순차적으로 증가해야 합니다.
- 빌드 넘버 (`CFBundleVersion`) - Xcode에서 `Build`로 보여집니다. 증가하는 숫자입니다.

오늘날의 iOS 개발 과정에선 위의 숫자들을 수동적으로 바꿀 이유가 없습니다. 대신에, 최신 버전을 유지/관리하는 신뢰할 수 있는 자동화된 시스템이 필요합니다.

여기엔 써드 파티 도구를 사용할 필요가 없습니다. Xcode에는 `agvtool`이라는 도구가 내장되어 있기 때문입니다. ([자세한 사항](https://developer.apple.com/library/content/qa/qa1827/_index.html))

Xcode 프로젝트를 위한 `Versioning System`을 가능하게 한 이후에, 다음과 같은 커맨드를 사용할 수 있게 됩니다.

```sh
# 버전 넘버를 업데이트 합니다 (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# 빌드 넘버를 다음 숫자로 업데이트 합니다 (CFBundleVersion)
agvtool next-version -all
```

만약 배포 도구인 [fastlane](https://fastlane.tools)을 사용하고 계신다면, [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/)와 [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/)를 사용해서 버저닝을 배포의 한 단계로 자동화 할 수 있습니다.

그렇게 사용하기 위한 `Fastfile`의 예제는 다음과 같습니다.

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
