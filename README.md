# latex文書をtextlint+redpen

latex文書に対するtextlint+redpenをgithub actionsで走らせるサンプル。

まずはredpen部分を実装しました。
textlint部分は設定中です。

## 導入方法

Overleafと連携している前提で構築しています。
Overleafではcommit先branchを指定できないことから（おそらくデフォルトになります）、以下の手順で導入します。

1. 元々のデフォルトブランチが`master`であると仮定します（最近は`main`になるみたいです）。
1. 自分の文章が入っているtexレポジトリに、このレポジトリの`.github/workflows/`をディクトリごとコピーします。
1. `.github/workflows/`を`master`にcommit & pushします。
1. 自分の文章が入っているtexレポジトリに、以下に示す設定ファイル群をコピーして、`master`にcommit & pushします。
    * 必要があれば設定ファイルを変更してからcommit & pushしてください。
1. 自分の文章が入っているtexレポジトリで、`lint`ブランチ、`review`ブランチの2つのブランチを作成します。

設定ファイル名|内容
---|---
`redpen-conf.xml`|redpenの設定ファイル
`redpen-invalid-words.txt`|`redpen-conf.xml`で設定している、不正な単語リストファイル
`.textlintrc`|textlint用の設定ファイル
`package.json`|textlint及びそのplugin、ruleを導入する設定ファイル
`package-lock.json`|`package.json`から生成されるファイル。`package.json`を更新したらnpmを用いて更新すること。

[textlint+reviewdogのgithub action](https://github.com/tsuyoshicho/action-textlint)では、npm ciを用いているため、`package-lock.json`が必須です。

## 使い方

`lint`ブランチ、`review`ブランチにそれぞれPull Requestを出すことで、textlint、redpenがそれぞれ実行され、reviewdogでPull Requestにコメントとして表示されます。
単純に、[textlint+reviewdogのgithub action](https://github.com/tsuyoshicho/action-textlint)、[redpen+reviewdogのgithub action](https://github.com/tsuyoshicho/action-redpen)を呼び出しているだけです。

1. tex文章の作成を`master`ブランチで行います。
    * もちろん、`master`からさらにブランチを切って作業し、`master`にマージしていく形でも構いません。
1. チェックしたいタイミングが来たら、`lint`←`master`または`review`←`master`のPull Requestを作成します。
    * `master`以外で作業して、`lint`、`review`にPull Requestしても構いません。
1. チェックが完了するのを待ちます。
1. 作成したPull Requestにチェック結果が表示されます。

チェック後はコメントを参考に修正しましょう。

**最後に`master`に反映させるのを忘れずに！**（修正完了後の`lint`、`review`ブランチから`master`にPull Requestを出すなどして反映させます）

## Relies on

* [tsuyoshicho - GitHub Action: Run redpen with reviewdog](https://github.com/tsuyoshicho/action-redpen)
* [tsuyoshicho - GitHub Action: Run textlint with reviewdog](https://github.com/tsuyoshicho/action-textlint)
* [reviewdog](https://github.com/reviewdog/reviewdog)

## License

Copyright (c) 2021, Shigemi ISHIDA

本レポジトリのすべてのファイルはMITライセンスでリリースされています。
