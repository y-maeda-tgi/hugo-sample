---
title: "ドキュメント更新ハンズオン"
date: 2022-09-01
weight: 20
---

## ゴール

- Markdown の基本的な記法が理解できる
- VS Code Remote Continer 上の Hugo で Markdown を Web サイトコンテンツに変換できる
- GitHub Action を利用する方法がわかる
- 【Want】 Hugo の設定を変更して、Web サイトコンテンツをカスタマイズできる

## 目次

1. VS Code Remote Container で Hugo を動かしてみよう
2. Markdown でドキュメントを書いてみよう
3. 自由練習１～　好きに Markdown を書いて、Web サイトに記事を追加してみましょう
4. GitHubAction で作業を自動化してみよう
5. 自由練習２
6. Hugo の設定を変更して、Web サイトコンテンツをカスタマイズしてみよう

## VS Code Remote Container で Hugo を動かしてみよう

VS Code Remote Continer の設定がされた Git リポジトリをクローンして、さっそく Hugo がどんなものなのか体験してみましょう

### (A) Windows端末

1. WSL2 を起動します（Windowsキーを押下→Ubuntuを入力）
1. Docker を起動しておきます： `sudo service docker start`
1. 任意の作業用のフォルダに移動します（例：ホームディレクトリでよければ `cd` を打てばＯＫ）
1. 演習用の GitHub リポジトリを取得します（ `git clone --recursive https://github.com/kazuo278/hugo-sample.git` ）
1. `cd hugo-sample` でリポジトリに移動します
1. `code .` で VS Code を起動します(初めて実行する場合はインストールが発生します)
1. もし、VSCode を起動した際に信頼するかの警告が出たら「はい、作成者を信頼します」を選択します
1. 右下に「Folder containes a Dev Container configuration file...」というポップアップが出たら「Reopen in Container」を選択します
1. 開発用のコンテナが起動するまで待ちます（初回は時間がかかります）
1. 上部メニュー＞ターミナル＞新しいターミナルを選択します
1. 開いたターミナルで `hugo server -w` のコマンドを実行します
1. ブラウザで「[http://localhost:1313/](http://localhost:1313/)」を開きます
1. md ファイルの１つを更新して保存したときに、すぐにブラウザ側に反映されていることを確認します

### (B) Mac端末

1. VSCodeを起動します
1. `shift + command + p` を押します
1. `shell command`を入力し、「Shell Command: Install 'code' command in PATH」を選択します。
1. Docker Desktopを起動します。
1. ターミナルを開き、任意の作業用のフォルダに移動します（例：ホームディレクトリでよければ `cd` を打てばＯＫ）
1. 演習用の GitHub リポジトリを取得します（ `git clone --recursive https://github.com/kazuo278/hugo-sample.git` ）
1. `cd hugo-sample` でリポジトリに移動します
1. `code .` で VS Code を起動します  
   うまくいかない場合は、VSCodeの「File -> Open Folder」から取得したリポジトリを選択してください。
1. もし、VSCode を起動した際に信頼するかの警告が出たら「はい、作成者を信頼します」を選択します
1. 右下に「Folder containes a Dev Container configuration file...」というポップアップが出たら「Reopen in Container」を選択します
1. 開発用のコンテナが起動するまで待ちます（初回は時間がかかります）
1. 上部メニュー＞ターミナル＞新しいターミナルを選択します(`ctrl + shift + @` でも可)
1. 開いたターミナルで `hugo server -w` のコマンドを実行します
1. ブラウザで「[http://localhost:1313/](http://localhost:1313/)」を開きます
1. md ファイルの１つを更新して保存したときに、すぐにブラウザ側に反映されていることを確認します


## Markdwon でドキュメントを書いてみよう

[Markdown記法 サンプル集](https://qiita.com/tbpgr/items/989c6badefff69377da7) を参考にさせてもらいながら、 Markdown の記述方法を学びましょう

＋α で Hugo の記事を作成する際に必要になる「メタデータ」の記載方法は以下のようになります。

```md
---
title: "タイトル名を書きます"
date: 2022-09-08
---
ドキュメントの冒頭に"---"で囲んだ範囲に、yaml形式(ざっくりいうとパラメータと値を : で区切って表現する形式)でメタ情報を記載します！
```

## 自由練習１：好きに Markdown を書いて、Web サイトに記事を追加してみましょう

1. 拡張子.mdでファイルを新規に作成します。  
2. 冒頭に title と date のメタデータを書いて保存します。  
3. ブラウザで「[http://localhost:1313/](http://localhost:1313/)」を開いて記事が追加されていることを確認します
4. あとは自由に Markdown で記事を書いてみてください

## GitHubAction で作業を自動化してみよう

[Qiita GitHub ActionsでHello World](https://qiita.com/Teach/items/d2c4d7bec98228df1807)を参考にさせてもらいながら、GitHub Actionsを動かしてみましょう。

- 参考：
  - [GitHub Actionsについて学ぶ](https://docs.github.com/ja/actions/learn-github-actions/understanding-github-actions)
  - [GitHub Actionsのワークフロー構文](https://docs.github.com/ja/actions/using-workflows/workflow-syntax-for-github-actions)
  - [GitHub Marketplace](https://github.com/marketplace?type=actions)

## 自由練習２：任意のブランチにPush時にソースコードを取得(checkout)するActionsを呼び、好きなLinuxコマンドを実行させてみよう

1. `helloworld.yml`の`on`以下を変更します

    ```yaml
    on:
      - workflow_dispatch
      - <ブランチPushイベント>
    ```

    参考：[ワークフローをトリガーするイベント](https://docs.github.com/ja/actions/using-workflows/events-that-trigger-workflows)

1. 'steps'以下を自由に変更します

    ```yaml
    steps:
      - run: echo "Hello World!"
      - uses: <アクション>
        with: <呼び出すアクションに応じて指定する>
      - run: <好きなlinuxコマンド>
    ```

## Hugo の設定を変更して、Web サイトコンテンツをカスタマイズしてみよう

- Hugo の設定ファイルを変更してみよう（[参考](https://www.docsy.dev/docs/get-started/basic-configuration/) ）
- layouts にファイルを作成して theme を上書きしてみよう（[参考](https://ja.takp.me/posts/how-to-customize-the-hugo-themes/)）
