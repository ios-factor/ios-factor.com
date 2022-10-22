Apple의 가이드라인에 따라 데이터와 설정을 저장하는 것은 앱의 라이프 사이클에 치명적입니다. 특히 iCloud 동기화, 새로운 폰으로 업그레이드 그리고 백업에서 폰을 복원하는 경우에서 그렇습니다.

Apple의 공식 [iOS 데이터 저장 가이드라인](https://developer.apple.com/documentation/foundation/optimizing_your_app_s_data_for_icloud_backup)을 따르고 있는지 확인하세요.

- `Documents`: 이 폴더는 유저가 생성한 컨텐츠를 위해 사용하세요. 이 폴더는 백업이 될 것입니다.
- `Caches`: 이 폴더는 다시 생성할 수 있는 데이터를 위해 사용하세요.
- `tmp`: 이 폴더는 임시 파일을 위해 사용하세요.
- 파일에 `백업하지마세요(do not back up)` 속성을 사용하세요.

위의 폴더에 민감한 사용자 정보(패스워드나 세션)를 저장하지마세요. 대신에 Keychain API를 사용하세요.

Keychain API는 데이터가 기기에 어떻게 저장될지에 대한 컨트롤을 제공합니다. [다양한 속성](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values)이 앱의 라이프 사이클에 어떻게 영향을 미치는지 잘 알고 있어야 합니다.

사용자가 새로운 iOS 기기로 업그레이드를 할 때, 데이터(예. 로그인 세션)는 마이그레이션 되나요? 라는 질문은 종종 간과되는 질문이지만 자기 자신에게 꼭 물어봐야 하는 질문 중 하나입니다.

만약 [`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly)를 사용했기 때문에 데이터가 iCloud나 iTunes 백업에 저장되지 않는다는 것은 사용자가 기기를 업그레이드하면 모든 데이터를 잃는다는 것을 의미합니다.
