**理想的には iOS-factor アプリはシステム全体のパッケージの暗黙的な存在に依存することはありません。** すべての依存関係を依存関係宣言マニフェストによって完全かつ正確に宣言します。 これには [Xcode](https://developer.apple.com/xcode) や [CocoaPods](https://cocoapods.org)、[fastlane](https://fastlane.tools) の正確なバージョンを含みます。

明示的に依存関係を宣言するメリットは、アプリを初めて使用する開発者向けの設定を簡素化するだけでなく、再現可能な方法で過去のビルドを再実行できる信頼できるビルドシステムを持つことです。 新しい開発者は、開発マシンにアプリケーションのコードベースをチェックアウトすることができます。これには、言語ランタイムと依存関係マネージャーだけが前提条件としてインストールされている必要があります。 彼らは決定的なビルドコマンドでアプリケーションのコードを実行するために必要なものすべてを設定することができます。

**正確な依存関係を指定することで、6か月前から遡ってビルドできます。By specifying the exact dependencies you can re-trigger a build from 6 months ago, knowing that it will succeed** 正確な依存関係を指定することで、6か月前からビルドを再トリガーすることができます.Xcode、CocoaPods、Swiftの同じバージョンを使用するため、ビルドが成功することがわかります。

iOS 開発は Web 開発のようにはコンテナ化されておらず、Apple が公式のソリューション（([rdar://40669395](https://openradar.appspot.com/radar?id=4929082424819712)）を提供するまで、この要件を満たすサードパーティのツールに限られています。

当面は、さまざまなサードパーティのツールを使用することで依存関係を明示的に宣言することができます。

#### Swift ベースのツール

Appleは [Swift Package Manager](https://swift.org/package-manager) に関する優れたガイドを提供しています。

#### Xcode のバージョン指定

iOS プロジェクトのルートディレクトリで [.xcode-version](https://github.com/fastlane/ci/blob/master/docs/xcode-version.md) ファイルを使えば、Xcode の正確なバージョンを宣言することができます。.

この方法では、CI システムが指定されたバージョンの Xcode を自動的にインストールして使うよう構成することができます。（インストール済みの）Xcode のバージョンを切り替えるには、[chxcode](https://github.com/klaaspieter/chxcode) のようなツールを使うことができます。

Xcode のインストールを自動化するには、Apple が Xcode をインストールするコマンドラインツール（[rdar://40669425](https://openradar.appspot.com/radar?id=5064112975380480)）を提供するまではサードパーティ製ツールである [xcode-install](https://github.com/krausefx/xcode-install) を使います。

#### Ruby ベースのツール

Ruby は `Gemfile` で正確な依存関係を定義するために [bundler](https://bundler.io) を使います。:

```ruby
source "https://rubygems.org"

gem "fastlane", ">= 2.96.1", "<= 3.0.0"
gem "cocoapods", "~> 1.5"
```

`Gemfile` と自動的に生成される `Gemfile.lock` は Ruby ベースバージョン管理システムにチェックインされます。ビルドシステムは Ruby ベースの依存関係をインストールするために `bundle install` を実行します。

#### JavaScript ベースのツール

JavaScript ベースの iOS アプリ（例: React Native）は、`package.json` ファイルを使って必要なすべての依存関係を定義します。

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

`package.json` は再現可能なビルドのバージョン管理にチェックインされます。
