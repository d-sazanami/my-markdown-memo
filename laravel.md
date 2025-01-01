# sessionテーブルがない

初期状態でLaravelを起動直後辺りに出ることがある。その際は、マイグレーションを実行する。

```bash
$ sail artisan migrate
```

# migrateが永続化されない

現象：sail downすると、migrate前の状態に戻ってしまう
sail downでコンテナを終了するのではなく、sail stopで終了した方が良さそう

## refs
https://teratail.com/questions/338586

# VSCodeのphp.validate.executablepathを解決する

## refs
- mac用のシェルファイルで解決する方法(https://qiita.com/kyukei/items/e951a237f5e50b67537b)

# Laravelバージョン確認

```bash
sail artisan -v
```

# docker-composeのvolumeで指定したmy.cnfが反映されない

Windowsのファイル・プロパティから読み取り専用にしたら、反映された

## refs:
https://zenn.dev/re24_1986/articles/21043cb43a9a50