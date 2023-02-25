# 画像を追加する

## セットアップ

- [公式サイト](https://squidfunk.github.io/mkdocs-material/reference/images/)を参考にし、`mkdocs-glightbox`のインストールと`mkdocs.yml`の加筆をします

```bash
pip install mkdocs-glightbox
```

```yaml
markdown_extensions:
  - attr_list
  - md_in_html
plugins:
  - glightbox
```

## 画像のアップロード

- 画像のパスを指定します

!!! Warning
    **記事からの相対パス**で反映されるので注意が必要です  
    例として`docs/images/favicon.png`を指定します  
    記事は`docs/tech/image.md`なので、`image.md`から見た`favicon.png`は`../images/favicon.png`にあります  


```markdown
<figure markdown>
  ![width 150](../images/favicon.png){ width=150 }
  <figcaption>幅150ピクセル</figcaption>
</figure>
```

<figure markdown>
  ![width 150](../images/favicon.png){ width=150 }
  <figcaption>幅150ピクセル</figcaption>
</figure>



# 参考

- [Material for MkDocs公式](https://squidfunk.github.io/mkdocs-material/reference/images/)
