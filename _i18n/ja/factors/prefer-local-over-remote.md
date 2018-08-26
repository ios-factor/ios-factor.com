近年いくつかの開発チームは、より多くのロジックをリモートのバックエンドに移し、iOSアプリをサーバーの結果を示すシンクライアントとして、ユーザーのアプリ体験を犠牲にして、開発作業が少なくて済むアプローチを使用しはじめました。 このアプローチでは、完全なインターネット接続（地下鉄、エレベーター、スポットのWiFiなど）が不十分な状況でアプリを使用すると、ユーザーの不満が生じます。

さまざまな理由で**できるだけ多くのビジネスロジックと計算をデバイス上で実行すべきです**。

- プライバシー: リモートサーバーにデータを送信しないようにする
- スピード: サーバーへのデータ送信やレスポンス待ち時間そして失敗（むらが多い Wi-Fi など)
- Data usage: users often have monthly data limits
- Scaling: If your app goes viral, you are responsible to scale the backend services up
- バッテリ寿命: モバイルデータを使うとバッテリ寿命いるUsing mobile data is costly for battery life
- 信頼性: ある国ではまだ信頼性の低い LTE/3G 接続がある

ほとんどの iOS アプリでは認証、より複雑な計算やコンテンツの保存など、特定のタスクにバックエンドが必要です。

**バックエンドで実行するタスクの数を制限し、Limit the number of tasks that run on the backend to a minimum to enhance the end-user's experience and to protect their privacy.**

インターネット接続を**必要**としない部分（ログインなど）はインターネット接続なしでも動作すべきです。:

- Your app's startup screen ([that shouldn't exist in the first place](https://developer.apple.com/ios/human-interface-guidelines/icons-and-images/launch-screen/)) should never wait for the first successful web response, as this causes bad UX for users with a spotty internet connection.
- もしアプリのすべての機能（ソーシャルネットワーキングアプリやライドシェアアプリ）でインターネット接続が必要であっても、履歴データ（乗車履歴、ダイレクトメッセージなど）へのアクセスはインターネット接続なしで（読み取り専用モードで）動作すべきである。
- インターネット接続が必要なアプリではサーバーに接続できないという明確なエラーメッセージを表示すべきです。
- Wi-Fi ホットスポットはログインや何らかの確認が必要な場合があり（ホテルや空港など）、HTTPS リクエストは停止して1分後にタイムアウトになることがよくあります。Apple がこの問題をシステムレベルで解決するまでは、開発者がこれらの状況を適切に対処する必要があります。
- アプリの初回起動時にユーザーがネットワークに接続していることを前提にしないでください。ユーザーはアプリをインストールしてからインターネット接続なしで出かけるまでアプリを開かないかもしれません。デプロイ時に最新のデータを使ってすぐ使える状態でアプリを出荷する責任があります。 This directly plays together with the weekly release trains described in the [deployment](/deployment) factor.
