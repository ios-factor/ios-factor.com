Apple のガイドラインに従ったデータや設定の保存は、アプリのライフサイクル、特にiCloudの同期、新しい iPhone へのアップグレード、バックアップからの復元に不可欠です。

必ず Apple 公式の [iOS Data Storage Guidelines](https://developer.apple.com/icloud/documentation/data-storage/index.html) に従ってください。

- `Documents`: ユーザーが生成したコンテンツ用、バックアップされる
- `Caches`: 再生成可能なデータ用
- `tmp`: 一時的なファイル用
- Make use of the `do not back up` attribute for files

機密なユーザー情報（パスワードやセッションなど）をこれらのディレクトリに保存しないでください。代わりに Keychain API を使います。

Keychain APIを使用すると、データをデバイスに保存する方法を制御できます。 [さまざまな属性](https://developer.apple.com/documentation/security/keychain_services/keychain_items/item_attribute_keys_and_values) がアプリのライフサイクルにどのように影響するかをよく理解していることを確認してください。

あなた自身に問いかけるべき見落としがちな質問: ユーザーが新しいiOS端末にアップグレードしたときに、データ（ログインセッションなど）も移行する必要がありますか？

[`kSecAttrAccessibleWhenUnlockedThisDeviceOnly`](https://developer.apple.com/documentation/security/ksecattraccessiblewhenunlockedthisdeviceonly) を使うとデータは iCloud や iTunes backup には含まれず、デバイスをアップグレードしたときにデータを失います。
