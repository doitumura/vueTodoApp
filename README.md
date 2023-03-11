### プルリクエスト確認用アプリ立ち上げ手順

任意のディレクトリで以下のコマンドを実行

```
git clone https://github.com/doitumura/vueTodoApp.git

cd vueTodoApp

git fetch origin todo

git checkout todo

cd todoApp

npm install

npm run dev
```

コマンド実行後、ブラウザのアドレスバーに localhost:5173 を入力

アプリを終了する場合は ctrl+c でコマンドを強制終了する
