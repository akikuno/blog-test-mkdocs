# 非公開記事を作成する

- 非公開記事を作成するには、`docs`以外のディレクトリに保存すればOKです:ok_hand:

```bash
mkdir -p draft
echo "# 下書き" > draft/draft.md
mkdocs gh-deploy
```


- ちなみにdraftディレクトリ中のファイルをGitHubで公開されないようにするためには、`.gitignore`で以下のように設定します

```text
# draft/draft.md以外のファイルをGit管理から外します
draft/*
!draft/draft.md
```

!!! メモ
    [mkdocs公式のblogプラグインを使えばyamlの設定だけで非公開にできるようです](https://squidfunk.github.io/mkdocs-material/setup/setting-up-a-blog/#drafts)  
    しかし、現時点（2023-02-24）では課金勢でしか使えないみたいです
