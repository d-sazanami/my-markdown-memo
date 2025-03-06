# 複数のgithubリポジトリを指定する

```bash
git remote set-url origin git@github-sazanami:d-sazanami/professional-laravel9.git
```

# addを取り消し

```bash
git reset HEAD
```

# addを取り消し

```bash
git reset HEAD
```

# diffで表示するファイルを制限する

```bash
git diff --name-only --diff-filter=ACRM HEAD...[comitt-hash]
```

`git archive` で削除されたファイルを除外する時に便利

-refs: https://tracpath.com/docs/git-diff/

# リモートブランチからローカルブランチを作ってチェックアウトする

```bash
git checkout -b new_branch_name origin/main
```