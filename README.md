# latex文書をtextlint+redpen

latex文書に対するtextlint+redpenをgithub actionsで走らせるサンプル。

まずはredpen部分を実装しました。

## 導入方法

Overleafと連携している前提で構築しています。
Overleafではcommit先branchを指定できないことから（おそらくデフォルトになります）、以下の手順で導入してください。

1. 元々のデフォルトブランチが`master`であると仮定します（最近は`main`になるみたいです）。
1. 自分の文章が入っているtexレポジトリで新たにbranchを作成します。ここでは`devel`を作成したとします。
1. デフォルトbranchを`devel`に切り替えます。
    * デフォルトブランチの切り替えは、レポジトリのSettings > Branchesで行えます。
1. 自分の文章が入っているtexレポジトリに、このレポジトリの`.github/workflows/`をディクトリごとコピーします。
1. 元々のデフォルトブランチが`master`ではない場合は、`.github/workflows/main.yml`を6行目のブランチ名を書き換えます。
1. `.github/workflows/`を`master`にcommit & pushします。
1. 必要があれば`conf/`内の設定ファイルを変更してcommit & pushしてください。

設定ファイル名|内容
---|---
redpen-conf.xml|redpenの設定ファイル
redpen_invalid-words.txt|redpen-conf.xmlで設定している、不正な単語リストファイル

## 使い方

`master`ブランチにPull Requestを出すことで、redpenが実行され、reviewdogでPull Requestにコメントとして表示されます。

1. tex文章の作成を`devel`ブランチで行います。
    * もちろん、`devel`からさらにブランチを切って作業し、`devel`にマージしていまっても問題ありません。
1. チェックしたいタイミングが来たら、`devel`→`master`のPull Requestを作成します。
1. あとは待っていれば作成したPull Requestにチェック結果が反映されて表示されます。

## Relies on

- [tsuyoshicho - GitHub Action: Run redpen with reviewdog](https://github.com/tsuyoshicho/action-redpen)
- [reviewdog](https://github.com/reviewdog/reviewdog)

## License

Copyright (c) 2021, Shigemi ISHIDA

本レポジトリのすべてのファイルはMITライセンスでリリースされています。
