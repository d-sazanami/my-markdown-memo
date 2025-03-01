# Vim・「行末」に文字を挿入する手順
https://japanrock-pg.hatenablog.com/entry/20100628/1277739776

# 複数行行末に一気に同じ文字を挿入
- refs: https://japanrock-pg.hatenablog.com/entry/20100628/1277739776

# 選択範囲内置換

# エディタタブの並び替え
exコマンドで、

```
:tabm+1
:tabm-1
```

# ヤンク内容をexコマンドにペースト

`Ctrl + r`, `"` と順番に入力

# mark機能

## markする

`m`, `[a-zA-Z]`と順番に入力

## 移動

`, `[a-zA-Z]`と順番に入力

## exコマンド

```
#一覧
:marks

# マークを削除
:delmarks a
```

