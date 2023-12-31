### マージコンフリクトの解決

マージコンフリクトを作成し、修正していきましょう。 パートナーと別々のブランチを作成後、同一ファイル名でファイルを作成し、マージしてみましょう。 1番目のブランチは正常にマージしますが、2番目のブランチにはマージコンフリクトが発生してしまいます。 協力して、マージコンフリクトを解決しましょう。

1. クラスのリポジトリで、 `USERNAME-conflict` のようなわかりやすい名前で、作業するブランチを作成します。
1. パートナーと両方で編集するためのファイルを選択します。（先の作業で作成したファイルの一つがよいでしょう）まず、あなたのブランチでそのファイルを編集します。そのファイル名は、パートナーが編集するファイルと同じファイル名である必要があります。そのファイルの中身が異なっていて、空でないことを確認してください。
1. クラスのリポジトリで、`base: main` と `compare: USERNAME-conflict` で Pull Request を作成します。
1. *1番目* の Pull Request が問題なくマージできることを確認します。
1. *2番目* の Pull Request では、マージコンフリクトが発生するので、協力してマージコンフリクトを解決しましょう。
    1. ローカル環境で、 `main` ブランチをフィーチャーブランチにマージします。
    1. マージコンフリクトが発生しても大丈夫！コンフリクトがあるファイルは `Unmerged Paths` に表示されます。 `git status` を実行して、どのファイルにコンフリクトがあるかを確認します。
    1. そのファイルをテキストエディタで開き、マージコンフリクトのマーカーを探します。 (`<<<<<<<`, `=======`, `>>>>>>>`)
    1. 両方のブランチのコードがあるので、残したい方を選択し、変更を保存します。
    1. マージコンフリクトを解決するために、保存した変更をステージに追加しコミットします。
    1. そのフィーチャーブランチをリモートにプッシュし、 Pull Request で解決したことを確認します。
1. Pull Request をマージします。

### マージコンフリクトの解決（一人で演習を行う場合）

パートナーとの作業が難しい場合など、一人で演習を行う場合は下記をご参考ください。

1. GitHub の class repository で、 `main` ブランチにいることを確認します。
1. `USERNAME-modify-first` ブランチを作成します。
1. `USERNAME-modify-first` ブランチのまま、自分のスライドファイル `_slides/##-USERNAME.md` の 6行目を変更し、コミットします。
1. **一度 `main` ブランチを開きなおして**から、2つ目として `USERNAME-modify-conflict` ブランチを作成します。
1. `USERNAME-modify-conflict` ブランチのまま、先ほど変更した同じファイルの同じ位置（ `_slides/##-USERNAME.md` の 6行目）を別の文字列に変更し、コミットします。
   - ここでのポイントは、変更する対象が、"同じファイル", "変更箇所が同じハンクで変更内容が異なる", "ファイルが空でない" 場合にコンフリクトが発生するという点です。
1. `base: main` と `compare: USERNAME-modify-first` で Pull Request を作成します（タイトル: `USERNAME merge first`）
1. `base: main` と `compare: USERNAME-modify-conflict` で Pull Request を作成します（タイトル: `USERNAME resolve conflict`）
1. `USERNAME merge first` の Pull Request をマージします。
1. `USERNAME resolve conflict` の Pull Request でマージコンフリクトが発生していることを確認し、マージコンフリクトを解消しましょう。
   1. ローカル環境で、下記の操作を行い、 `main` ブランチの更新取込みを行います。

      ```sh
      git switch main
      git pull
      ```

   1. `git fetch` でリモート（ GitHub 上）の情報を取込み、リモートで作成した `USERNAME-modify-conflict` ブランチをアップストリームに設定した上で、ローカルのブランチを切り替えます。

      ```sh
      git fetch
      git switch USER-modify-conflict
      ```

   1. `main` ブランチをフィーチャーブランチにマージします。

      ```sh
      git merge main
      ```

   1. マージコンフリクトが発生しても大丈夫！コンフリクトがあるファイルは `Unmerged Paths` に表示されます。 `git status` を実行して、どのファイルにコンフリクトがあるかを確認します。

      ```sh
      git status
      ```

   1. そのファイルをテキストエディタで開き、マージコンフリクトのマーカーを探します。 (`<<<<<<<`, `=======`, `>>>>>>>`)

      ```sh
      # Visual Studio Code で開く場合
      code _slides/##-USERNAME.md
      ```

   1. マーカーに囲まれた両ブランチのコードのうち、残したい方を残し、変更を保存します。
   1. マージコンフリクトを解決するために、保存した変更をステージに追加しコミットします。

      ```sh
      git add _slides/##-USERNAME.md
      git commit
      ```

   1. そのフィーチャーブランチをリモートにプッシュします。

      ```sh
      git push
      ```

1. `USERNAME resolve conflict` の Pull Request で解決したことを確認し、マージします。

> マージメッセージとは？ 今回の場合では、再帰的なマージを行っています。 再帰的なマージは、この２つのブランチがマージされた時点を永続的に記録する、新しいコミットを作成します。 Gitのマージの活用については、後ほど説明します。
