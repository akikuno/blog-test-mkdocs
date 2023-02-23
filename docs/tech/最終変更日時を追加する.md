# 最終更新日時を追加する

- `mkdocs-git-revision-date-localized-plugin`をインストールします

```bash
pip install -U mkdocs-git-revision-date-localized-plugin
```

- `mkdocs.yaml`に以下を加筆します

```yaml
plugins:
    - git-revision-date-localized
```

- `git`に保存された最終更新日がブログ下部に記載されます
