# latex文書をtextlint+redpen

latex文書に対するtextlint+redpenをgithub actionsで走らせるサンプル。

まずはredpen部分を実装しました。

## 導入方法

Overleafと連携している前提で構築しています。
Overleafではcommit先branchを指定できないことから（おそらくデフォルトになります）、以下の手順で導入します。

1. 元々のデフォルトブランチが`master`であると仮定します（最近は`main`になるみたいです）。
1. 自分の文章が入っているtexレポジトリに、このレポジトリの`.github/workflows/`をディクトリごとコピーします。
1. `.github/workflows/`を`master`にcommit & pushします。
1. 自分の文章が入っているtexレポジトリに、このレポジトリの`conf/`をディクトリごとコピーします。
1. `conf/`を`master`にcommit & pushします。
    * 必要があれば`conf/`内の設定ファイルを変更してからcommit & pushしてください。
1. 自分の文章が入っているtexレポジトリで、`review`ブランチを作成します。

設定ファイル名|内容
---|---
conf/redpen-conf.xml|redpenの設定ファイル
conf/redpen_invalid-words.txt|redpen-conf.xmlで設定している、不正な単語リストファイル

## 使い方

`review`ブランチにPull Requestを出すことで、redpenが実行されてreviewdogでPull Requestにコメントとして表示されます。
単純に、[redpen+reviewdogのgithub action](https://github.com/tsuyoshicho/action-redpen)を呼び出しているだけです。

1. tex文章の作成を`master`ブランチで行います。
    * もちろん、`master`からさらにブランチを切って作業し、`master`にマージしていく形でも構いません。
1. チェックしたいタイミングが来たら、`master`→`review`のPull Requestを作成します。
1. チェックが完了するのを待ちます。
1. 作成したPull Requestにチェック結果が表示されます。
1. 指摘に対する修正などを行って`review`にcommitします。
    * Pull Request画面でsuggestionを作成してcommitしてもOKです。
1. `review`にcommitすると再びredpen+reviewdogが実行されますので、問題なくなる（あるいは無視してOKになるまで）修正を繰り返します。
1. Pull Requestをマージしてcloseします。
1. `master`に`review`をマージします。
    * `review`→`master`のPull Requestを作成するなどしてマージします。
    * これをやらないと、チェックして修正した結果が反映されません。

## Relies on

* [tsuyoshicho - GitHub Action: Run redpen with reviewdog](https://github.com/tsuyoshicho/action-redpen)
* [reviewdog](https://github.com/reviewdog/reviewdog)

## License

Copyright (c) 2021, Shigemi ISHIDA

本レポジトリのすべてのファイルはMITライセンスでリリースされています。
