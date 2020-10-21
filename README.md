
## アーキ

## 概念
* input ... folder/ファイルを実行中のdockerの中にアップロードして使う
* outputが定義されてたら、勝手にディレクトリができる
* 最初にパイプラインを作成したらpauseしている
* trigger 
  * Job の WebUI 上の + ボタンをクリックする(前のセクションで触れた通りです)
  * Resource の検出から Job を起動する(これは次のレッスン Resource から Job を起動する でご紹介します)
  * fly trigger-job -j pipeline/jobname コマンド
  * POST の HTTP リクエストを Concourse API に送る
  * ダッシュボードではトリガーでないリソースは点線

## コマンド
```sh
# login
fly --target tutorial login --concourse-url http://127.0.0.1:8080 -u admin -p admin

# taskの実行
fly -t tutorial execute -c task_hello_world.yml
fly -t tutorial e -c task_hello_world.yml
# -i でinputフォルダをタスクに渡す　. を渡すとカレントディレクトリにあるファイルを全部渡す
fly -t tutorial e -c inputs_required.yml -i some-important-input=.
# pipelineの作成
fly -t tutorial set-pipeline -c pipeline.yml -p hello-world
fly -t tutorial sp -c pipeline.yml -p hello-world
# ビルドを見る
fly -t tutorial builds
# ログをクライアントから見る
fly -t tutorial watch -j hello-world/job-hello-world
# build番号でみる
fly -t tutorial watch -b num
# コマンドでjobを実行
fly -t tutorial trigger-job -j hello-world/job-hello-world
fly -t tutorial tj -j pipeline/job
# パイプラインの削除
fly -t tutorial destroy-pipeline -p hello-world

```