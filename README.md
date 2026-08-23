# 根拠でわかる技術士一次（建設）— 公開ページ

App Store Connect で必須になる2つのURLを置くための、静的サイトです。

- `index.html` … サポートページ（App Store Connect の「サポートURL」に指定）
- `privacy.html` … プライバシーポリシー（同「プライバシーポリシーURL」に指定）
- `icon.png` … サポートページに表示するアプリアイコン

アプリ本体のリポジトリとは分けてあります。本体は非公開、このページだけを公開するためです。

## 公開の手順

GitHub CLI（`gh` 2.98.0）を導入済みです。次の3ステップで公開できます。

### 1. GitHubにログインする（あなたの操作）

```
gh auth login
```

聞かれたら、こう答えます。

- What account do you want to log into? → **GitHub.com**
- What is your preferred protocol? → **HTTPS**
- Authenticate Git with your GitHub credentials? → **Yes**
- How would you like to authenticate? → **Login with a web browser**

ブラウザが開くので、表示された8桁のコードを貼り付けて承認します。
GitHubのアカウントをまだ持っていない場合は、先に https://github.com/signup で作成してください。

### 2. リポジトリを作って公開する

```
gh repo create gijutsushi1-site --public --source=. --remote=origin --push
```

`--public` が必須です。GitHub Pages で公開するため、非公開リポジトリでは使えません。
（アプリ本体のリポジトリは、これとは別に非公開のままにしておきます）

### 3. GitHub Pages を有効にする

ブラウザで リポジトリ → **Settings** → **Pages** → Source を
**Deploy from a branch** ／ ブランチ `main` ／ フォルダ `/ (root)` にして Save。

数分待つと、次のURLで見えるようになります。

- サポートURL … `https://<ユーザー名>.github.io/gijutsushi1-site/`
- プライバシーポリシーURL … `https://<ユーザー名>.github.io/gijutsushi1-site/privacy.html`

## 公開したあとに必ずやること

- [ ] **両方のURLを実際にブラウザで開いて、中身が表示されるか確認する**
      （中身のないURLは審査で「内容が確認できない」と指摘されます）
- [ ] スマートフォンでも開いて、文字がはみ出していないか見る
- [ ] `info@tochigigurashi.com` 宛に自分でテストメールを送り、届くか確かめる

## 内容を更新するとき

ファイルを直して、次の2行だけです。

```
git add -A && git commit -m "更新内容"
git push
```

数分で公開ページに反映されます。

## 更新が必要になる場面

- 収録内容が練習問題から過去問題に変わったとき → `index.html` のFAQと、
  `privacy.html` の記述を実装に合わせる
- データの書き出し・読み込み機能を追加したとき → FAQ「機種変更をすると記録は
  引き継がれますか」の答えを書き換える
- 収集するデータが増えたとき（解析ツールや広告を入れたときなど）
  → `privacy.html` を必ず先に更新する。**申告と実装の食い違いは審査で見られます**
