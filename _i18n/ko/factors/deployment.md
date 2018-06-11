[디펜던시](/ko/dependencies) 요소에서 설명했듯이, 코드 레포지토리는 빌드, 테스트 그리고 iOS 앱의 배포까지 할 수 있는 모든 디펜던시를 포함하고 있어야 합니다.

앱이 이러한 요구 사항을 충족한다면, 여러분은 **어떤** macOS 기반 기기에서도 새로운 앱을 릴리즈할 수 있게 될 것입니다.

이상적인 세계에선, 앱 업데이트를 릴리즈하기 위해선 다음과 같은 것들이 필요합니다.

- 완전히 비어있는 임시 컨테이너를 생성하세요.
- 모든 디펜던시를 자동으로 설치하세요. (예. Xcode와 [CocoaPods](https://cocoapods.org))
- 배포 스크립트를 실행하세요. (예. [fastlane](https://fastlane.tools))

불행하게도, Xcode가 macOS에서만 실행된다는 사실과 macOS를 기술적으로 가상화 하는 것은 법적인 문제이기 때문에 이 접근 방식([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712))은 사용할 수 없습니다. macOS 개발환경을 일관성있게 유지해줄 수 있게 해주는 써드 파티 도구에는 [Veertu](https://veertu.com/)가 있습니다.

최근 몇 년 동안, 일회용 컨테이너는 다양한 이유로 인기를 얻어왔습니다.

- 호스트 운영 체제에 디펜던시 없이 완벽하게 재생성 가능한 빌드
- 어떠한 기기에서도 실행됨 (여러분의 로컬 컴퓨터부터 클라우드에 있는 어떤 서버까지)
- 꼭 필요한 디펜던시만 가진 깨끗한 빌드

이제, iOS 개발자들이 할 수 있는 최고의 접근 방식은 다음과 같을 것입니다.

- [xcode-install](https://github.com/krausefx/xcode-install)를 사용한 Xcode 설치 자동화
- [.xcode-version file](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md)를 사용해서 Xcode 릴리즈를 지정
- 설정 파일에서 모든 디펜던시를 정의함 ([디펜던시](/ko/dependencies) 요소를 읽어보세요)
- [fastlane](https://fastlane.tools)과 같은 배포 도구를 사용해서 완벽한 배포를 자동화함
- 코드 사이닝 자동화 (예. [codesigning.guide](https://codesigning.guide))
- 배포를 자주하고, 이상적으로는 일주일에 한 번이 좋음

많은 회사들이 앱의 새 버전이 출시되는 일정에 `배포 기차` 컨셉을 사용합니다. `master`나 `release`와 같은 메인 브랜치에 머지된 모든 코드는 배포 기차가 "떠나는" 시점에 App Store에 배포됩니다. 이 접근 방식은 대부분의 큰 iOS 앱에서 구현돼있는 방식입니다.
