# faviconを変更する

- faviconをダウンロードします
    - 今回は[fontawesomeからSVGをダウンロード](https://fontawesome.com/icons/pen-to-square?s=regular&f=classic)し、丸背景に加工しました
    - ファイル名は`favicon.png`としました

- `docs/images`ディレクトリにfaviconを保存します

- `mkdocs.yml`に以下を追加します

```yaml
theme:
  favicon: images/favicon.png
```
