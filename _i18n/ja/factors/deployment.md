[Dependencies](/dependencies) で述べたように、コードのリポジトリは iOS アプリのビルド、テスト、リリースに必要なすべての依存関係を含むべきです。

その要件を満たせば、**どんな** macOS のマシンからでもアプリをリリースすることができます。

理想では、アプリをリリースするために、

- 完全に空の、一時的なコンテナを生成する
- 自動的にすべての依存関係をインストールする（Xcode や [CocoaPods](https://cocoapods.org) など）
- デプロイスクリプトを実行する（[fastlane](https://fastlane.tools) など）

残念ながら、Xcode は macOS 上で動かす必要があり、macOS の仮想化は技術的にも法的にも課題があるため、私たちはこのアプローチを利用することができません（[rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712))。[Veertu](https://veertu.com/) というサードパーティー製の商用ソリューションで Apple のハードウェア上で macOS の仮想環境を構築することができます。

近年、使い捨てのコンテナはさまざまな理由で人気を得ています。

- ホスト OS に依存しない完全に再現可能なビルド
- どんなマシンでも実行できる（ローカルコンピューターやクラウドのサーバーなど）
- 最低限必要な依存関係だけのクリーンビルド

いま iOS デベロッパーがとれるベストなアプローチは次のとおりです。

- [xcode-install](https://github.com/krausefx/xcode-install) を使って Xcode インストールを自動化する
- 正確な Xcode バージョンを指定するために [.xcode-version ファイル](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) を使う
- 設定ファイルですべての依存関係を定義する（[Dependencies](/dependencies) ファクターを参照)
- [fastlane](https://fastlane.tools) のようなデプロイツールを使った完全なデプロイプロセスの自動化する
- コード署名を自動化する（例: [codesigning.guide](https://codesigning.guide)）
- 頻繁に、理想的には毎週デプロイする

多くの企業は `リリーストレイン`（新しいアプリをリリースするスケジュール）の概念を用います。リリーストレインが"出発する"ときにメインのブランチ（`master` や `release` など）にマージされたすべてのコードが App Store へ出荷されます。このアプローチは大規模な iOS アプリのほとんどで実装されています。
