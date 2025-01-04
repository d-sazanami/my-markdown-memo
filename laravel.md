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

# webサーバーが起動しない

localhostにアクセスできなくなったので、dockerのログを確認したところ、compowerがPHPバージョンが低すぎて起動できなかったみたい

```
laravel.test-1  | 2025-01-01 06:56:58,364 INFO spawned: 'php' with pid 10                                                                                                               
laravel.test-1  | Composer detected issues in your platform:
laravel.test-1  | 
laravel.test-1  | Your Composer dependencies require a PHP version ">= 8.2.0". You are running 8.1.31.                                                                                  
laravel.test-1  |                                                                                                                                                                       
laravel.test-1  | PHP Fatal error:  Composer detected issues in your platform: Your Composer dependencies require a PHP version ">= 8.2.0". You are running 8.1.31. in /var/www/html/venlaravel.test-1  | 2025-01-01 06:56:58,466 INFO exited: php (exit status 255; not expected)
```

参照するDockerfileのバージョンを8.3を見るようにdocker-compose.yml編集
--no-cacheでビルドし直して、再起動させたらwebサーバーが起動できた

## refs
https://qiita.com/mitashun/items/decbc4346e99edaec907

# laravel-langが導入できない

```
warning:  cannot set modif./access times for /var/www/html/vendor/composer/7a2ee95b/Laravel-Lang-lang-0937695/source/fortify/1.x/fortify.json Operation not permitted
```

等々の権限がなくて、ファイルアクセスができないWargning頻発後、Failedで導入が終わる。

## solve

1. wslで起動しているLinuxディストリビューション上で、`/etc/wsl.conf` を作成。以下をコピペする。

```
[automount]
enabled = true
options = "metadata"
mountFsTab = false
```

2. WSLを使っているWindowsアプリケーション、Dockerも終了する
3. PowerShellを起動

```powershell
> wsl --list
# 入れているwslサブシステム一覧が表示される。
# 1.で起動したサブシステムの名前を見つける
> wsl --terminate Debian    # Debianの部分は、上コマンドで見つけたサブシステムの名前をいれる
```

4. 1.のディストリビューションをWindowsのアプリケーション一覧から起動

## refs
- https://qiita.com/haruto_dev/items/9342d81cb9d965e10dc8
- https://github.com/Microsoft/WSL/issues/81#issuecomment-796798258

# laravel-langで日本語化

```bash
# langディレクトリは初期状態ではないため、以下で作成する
sail artisan lang:publish

# composerでlaravel-langを導入
sail composer require laravel-lang/lang
#vendorにlaravel-langのファイルが入るが、実態はjsonで、laravelが参照するのはphpなので、書籍『プロフェッショナルWebプログラミング』の通りだと、多分バージョン指定で解決するかも？

# laravel-lang/langの日本語化ファイルを元に、lang/ja/validation.phpなどの言語ファイルを更新
sail artisan lang:update
```

## refs
- https://saiko1988.hatenablog.com/entry/2023/08/20/011654

# 個別のシーダの実行

```bash
php artisan db:seed --class=UserSeeder
```

## refs
- https://readouble.com/laravel/11.x/ja/seeding.html
    - シーダの実行

# Laravel Breezeを入れるときに、権限でfatalとなった

```
The repository at "/var/www/html" does not have the correct ownership and git refuses to use it:
                                                                                                                                                                                        
fatal: detected dubious ownership in repository at '/var/www/html'                                                                                                                      
To add an exception for this directory, call:                                                                                                                                           
                                                                                                                                                                                        
        git config --global --add safe.directory /var/www/html 
```

# RouteserviceProvider::HOMEがない

app\Http\Controllers\Auth\AuthenticatedSessionController.php#storeで、 `/dashbord` にリダイレクトしているので、ここを書き換える？

## refs
- `bootstrap/app.php` で対応する
    - https://blog.regrex.jp/2024/07/22/laravel11-guest%E3%83%9F%E3%83%89%E3%83%AB%E3%82%A6%E3%82%A7%E3%82%A2%E3%81%AE%E3%83%AA%E3%83%80%E3%82%A4%E3%83%AC%E3%82%AF%E3%83%88%E5%85%88%E3%81%AE%E5%A4%89%E6%9B%B4%E6%96%B9%E6%B3%95%E3%81%8C/
    - https://tech.arms-soft.co.jp/entry/2024/07/10/090000
    - ここを書き換えるだけではできなかった
- 個別にリダイレクトさせる
    - https://qiita.com/wonky39325441/items/0e6818911896b0c85479
- 『Laravelの教科書』
    - routes/web.phpで `/dashbord` のパスに指定するControllerを変えたい処理のControllerに書き換える

# Unable to locate file in Vite manifest

```bash
# viteが依存しているプラグインの解決
sail npm install --save-dev vite laravel-vite-plugin
sail npm install --save-dev @vitejs/plugin-vue

# ビルドしなおし
sail npm run build

# vite起動
sail npm run dev
# 起動しっぱなしにしないと解決できない
```

## refs
https://qiita.com/zakki_engineer/items/170ac2386c23b9d78c4b