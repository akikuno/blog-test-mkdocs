---
tags:
  - tags
---

# tagをつける

- `mkdocs.yml`の`plugins`に以下のように`tags`を追加します

```yaml
plugins:
    - search
    - awesome-pages
    - tags:
        tags_file: tags.md
```

- マークダウンファイルのyamlに以下を記載します

```yaml
---
tags:
  - tags
---
```

- `tags.md`をdocsディレクトリに作ります

```markdown
# タグ一覧

[TAGS]
```

- ブログで「タグ一覧」をクリックすると、タグが一覧できます
