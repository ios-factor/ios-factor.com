根据苹果官方指南，数据和配置的存储对应用的生命周期至关重要，尤其是在 iCloud 同步、更新数据至一个新手机以及恢复手机备份时。

请参考苹果官方的 [iOS 数据存储指南](https://developer.apple.com/documentation/foundation/optimizing_your_app_s_data_for_icloud_backup):

- `Documents`：该目录用于存储用户生成的内容，且会备份
- `Caches`：该目录用于存储可以被重新生成的数据
- `tmp`：该目录用于存储临时文件
- 使用文件的 `do not back up` 属性

绝不应该在这些目录中存储用户敏感信息（如：密码或会话），而应该使用钥匙串（Keychain）的 API。

钥匙串 API 可以让你控制数据的存储方式。请确保你对[这些属性](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values)是如何影响应用的生命周期有着足够的理解。

你应该问自己一个问题——这个问题经常被人忽视——当用户升级到了一个新的 iOS 设备，数据（如：登录会话）是否也应该迁移过去？

如果你使用 [`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly) 属性，则数据不会被 iCloud 或 iTunes 的备份，这意味着用户如果更新他们的设备，则会丢失这些数据。
