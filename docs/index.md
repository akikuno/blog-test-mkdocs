---
tags:
  - MkDocs
  - GitHub Pages
---
# MkDocsでGitHub Pagesを運用する際のメモ

## 初期設定:gear:

### 必要なものをインストールします

- `mkdocs`と`mkdocs-material`（テーマ）、`mkdocs-awesome-pages-plugin`（記事を降順に並び替えるときに利用）をインストールします

```bash
pip install -U pip
pip install -U mkdocs mkdocs-material mkdocs-awesome-pages-plugin
```

### GitHubで公開リポジトリを作ります

- リポジトリ名がURLのブログタイトルになります
> `https://akikuno.github.io/mkdocs-and-ghpages/`

- **公開リポジトリを作るだけでOKです**
    - [GitHub Pagesのチュートリアルにある設定](https://docs.github.com/ja/pages/quickstart)はしなくて良いです

- 公開リポジトリをダウンロードします

```bash
git clone https://akikuno.github.io/mkdocs-and-ghpages/
```

### mkdocsで記事を作ります

- ダウンロードした`mkdocs-and-ghpages`ディレクトリ下で、以下のコマンドを実行します

```bash
mkdocs new .
```

- ディレクトリ直下に`docs`, `mkdocs.yml`の2つが作られます
- `docs`ディレクトリに`index.md`が作られます

### GitHub Pagesにデプロイします

```bash
mkdocs gh-deploy
```

- ディレクトリ直下に`site`が作られます
    - `site`はとくに気にしなくて大丈夫です


### テーマを変更します

- デフォルトでも十分見やすいですが、せっかくなのでテーマを変更してみます
- ついでに絵文字を表示できるようにします
    - `:smile:`という表記で絵文字が表示できるようになります:smile:

- `mkdocs.yml`を以下のように変更します

```text
site_name: MkDocsとGitHub Pages

# テーマを変更します
theme:
  name: 'material'
  palette:
    primary: 'teal'
    accent: 'teal'

# 絵文字を表示します
markdown_extensions:
    - pymdownx.emoji:
        emoji_generator: !!python/name:pymdownx.emoji.to_alt
```

- `mkdocs.yml`を書き換えたあと、デプロイすれば反映されます

```bash
mkdocs gh-deploy
```

## 複数記事の投稿📚

- `docs`直下に記事をアップしているとサイドバーが見にくくなるので、サイドバーに項目を作ります

- ここでは`docs`に`blog`ディレクトリを作ります
```bash
mkdir -p docs/blog
```

- `docs/blog`ディレクトリに記事を2つ作ります
```bash
echo "# blog1" > docs/blog/blog1.md
echo "# blog2" > docs/blog/blog2.md
```

```bash
mkdocs gh-deploy
```

### 記事の表示順を降順にしたい

- シンプルにURL（マークダウンファイル名）の辞書順（昇順）のようです
    - 以下の構成では`1000-01-01`が`1000-01-02`の前に表示されます

```bash
echo "# 200" > docs/blog/1000-01-01.md
echo "# 100" > docs/blog/1000-01-02.md
```

- 表示順を日付（ファイル名）の降順にしたいときには[MkDocs Awesome Pages Plugin](https://github.com/lukasgeiter/mkdocs-awesome-pages-plugin)を使います

- `mkdocs.yml`に以下を追記します

```text
plugins:
    - search
    - awesome-pages
```

- `.pages`に降順設定を書き込むと、`.pages`のあるフォルダ内の記事に設定が反映されます

```bash
pip install -U mkdocs-awesome-pages-plugin
echo "order: desc" > docs/blog/.pages
```

- 👆これで`docs/blog`内にあるファイルは逆順（降順）に表示されるようになります

## そのほか:bulb:
### ライト・ナイトモードの切り替え

- `mkdocs.yml`の`theme`下に以下のテキストを追記します

```yaml
theme:
  palette:
    # Palette toggle for light mode
    - scheme: default
      primary: 'teal'
      accent: 'teal'
      toggle:
        icon: material/weather-night
        name: Switch to dark mode
    # Palette toggle for dark mode
    - scheme: slate
      primary: 'teal'
      accent: 'teal'
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
```

### シンタックスハイライト

- `pymdownx.highlight`と`highlight.min.js`の設定を`mkdocs.yaml`に追記します

```yaml
markdown_extensions:
    - pymdownx.highlight

extra_javascript:
    - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/highlight.min.js
    - javascripts/config.js
extra_css:
    - https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.7.0/styles/default.min.css
```


### `yaml`の書き方いろいろ

[MkDocsによるドキュメント作成](https://zenn.dev/mebiusbox/articles/81d977a72cee01)

- 著作権表示やジェネレーターの表記をオフにするなど便利機能がいっぱいあります


## 注意点⚠️

### 毎回のGitの認証がめんどう

- デプロイするときに毎回GitのユーザーIDおよびパスワードを求められるので、以下のコマンドで認証を記憶すると快適です:smile:

```bash
git config --global credential.helper store
```

### mkdocsのインデントが反映されない

- リストをネストさせる時のインデントが**スペース4個**です
    - スペース2個では反映されません

### ライト・ナイトモードの切り替えを用いるとテーマ色の設定が反映されない

- ライト・ナイトモードの切り替えを使用するときには、それぞれのsheme内にテーマ色を設定しないと反映されません

- 以下はOKな例です:ok_hand:

```yaml
theme:
  name: 'material'
  palette:
    - scheme: default
      primary: 'teal'
      accent: 'teal'
      toggle:
        icon: material/weather-night
        name: Switch to dark mode
    - scheme: slate
      primary: 'teal'
      accent: 'teal'
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
```

- 以下はダメな例です:no_good:

```yaml
theme:
  name: 'material'
  palette:
    primary: 'teal'
    accent: 'teal'
    - scheme: default
      toggle:
        icon: material/weather-night
        name: Switch to dark mode
    - scheme: slate
      toggle:
        icon: material/weather-sunny
        name: Switch to light mode
```

- ダメな例でもエラーなくデプロイされるので、原因がわかるまで時間がかかりました…

## 参考資料 :bow:

- [mkdocsを使ったGitHub Pagesの作成方法](https://aiedoc.github.io/note/Tips/Mkdocs/mkdocs%E3%82%92%E4%BD%BF%E3%81%A3%E3%81%9FGitHubPages/)
- [MKDocsを使ってFPGA開発日記の記事まとめページを作り直した](https://msyksphinz.hatenablog.com/entry/2018/07/14/120000)
- [なかけんのMkDocsノート](https://mkdocs.nakaken88.com/)
- [MKDocsで絵文字を使ってみる](https://enu23456.hatenablog.com/entry/2022/12/11/140629)
- [Auto-populate navigation sub-sections](https://github.com/mkdocs/mkdocs/issues/714#issuecomment-503439934)
- [MkDocs でスペース2個のインデントをリストのネストとして認識させたい場合](https://stakiran.hatenablog.com/entry/2018/08/02/202816)
- [Gitで毎回パスワードを聞かれないようにする](https://qiita.com/aqua_ix/items/0433f85330087c62bffa)
