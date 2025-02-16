# grep
https://learn.microsoft.com/ja-jp/powershell/module/microsoft.powershell.utility/select-string?view=powershell-7.4#6


## Shif-JIS環境でのソースgrep

```powershell
# 単体ファイル内から検索
Select-String -Path .\Path\*.log -Pattern 'SearchWord' -Encoding oem -SimpleMatch

# 再帰的に探す
Get-ChildItem -Path .\Path\*.txt -Recurse | Select-String -Pattern 'SearchWord' -CaseSensitive
# -SimpleMatchだと正規表現を使わない
```

# more考察記事
https://coffeekemuri.blogspot.com/2018/08/powershell-powershellmoreunixmore.html

```powershell
Get-Content target.txt | Out-Host -Paging
```

# diff
```powershell
diff (cat ".\diff1.txt") (cat ".\diff2.txt")
```


