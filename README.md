## 概要
サブフォルダを新規リポジトリに分割するテストです。

今回の分割では`git filter-branch`というcommandを使用してサブフォルダを新規リポジトリに分割します。

（参考：https://docs.github.com/ja/github/getting-started-with-github/splitting-a-subfolder-out-into-a-new-repository）

このリポジトリに存在するfolderを新規リポジトリとして分割を行います。

分割したリポジトリについては以下を御覧ください。
https://github.com/vivid344/Sub_Subfolder

## 検証内容と結果
検証内容と結果は以下の内容になっています。
- commit logの引き継ぎ
  - 可能。該当するファイルのコミットだけに絞り込まれる。
- PRの引き継ぎ
  - 不可。あくまでのgithubの機能のため。PRのマージコミットなどは見られるのでそこでは確認できる。
- issueの引き継ぎ
  - 不可。これについてもgithubの機能であるため。
- master, staging, developの扱いはどうなるの
  - `git filter-branch`では1ブランチ分の情報しか持ってくることが出来ない。そのため、元のリポジトリに対しdevelop、staging、masterの3ブランチに対して情報を持ってくる（3回コマンドを実行する）必要がある。
- 先に分割した後に、元のファイルに分割があった場合におって追加することはできるのか
  - 可能。もう一度`git filter-branch`を行うことで前と同じ内容＋そこからの差分（コミット）で作成することができる。
- その他
  - `git filter-branch`を実行したリポジトリは、該当のディレクトリに上書きされる。（今回の場合、このREADME.mdなどが消えて、folderの中身であるhoge1.txtが最上位の階層に置き換わる）間違ってremoteのurlを変えずにそのままコミットすると大変なことになる。
  - 既存のコードについては消えるわけではないので、後々削除が必要。
