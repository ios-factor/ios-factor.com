**バージョンとビルド番号は特定のアプリの App Store 提出の一意の識別子**

- バージョン番号（`CFBundleShortVersionString`） - Xcode では `Version` と表示されていてマーケティングバージョンとも呼ばれます。エンドユーザーに表示されるバージョンでリリースごとにインクリメントする必要があります。
- ビルド番号（`CFBundleVersion`） - Xcode では `Build` と表示されるインクリメント番号。

今日の iOS アプリ開発プロセスではこれらの番号を手動で変更する必要はありません。代わりに、バージョンを最新に保つ信頼性のある自動化されたシステムが必要です。

サードパーティー製ツールを使う必要はありません。Xcode には `agvtool` というビルトインのツールがあります。（[詳細](https://developer.apple.com/library/content/qa/qa1827/_index.html)）

最初に Xcode プロジェクトの `Versioning System` を有効にすると、次のコマンドを使用できます。

```sh
# Update the version number (CFBundleShortVersionString)
agvtool new-marketing-version 2.0

# Update the build number (CFBundleVersion) to the next one
agvtool next-version -all
```

デプロイメントツール [fastlane](https://fastlane.tools) を使うのであれば、開発ステップの一部としてバージョンを自動であげるために [increment_version_number](https://docs.fastlane.tools/actions/increment_version_number/) と [increment_build_number](https://docs.fastlane.tools/actions/increment_build_number/) を使うことができます。

例 `Fastfile`:

```ruby
lane :beta do
  increment_build_number
  build_ios_app
  testflight
end
```
