# Card Cabinet - PWA設置ガイド

Androidだけで完結する手順（所要時間: 10分、完全無料）。

---

## 📱 GitHub Pagesで公開する（おすすめ）

### 1. GitHubアカウントを作る（未所有の場合）
1. Chromeで [github.com](https://github.com/signup) を開く
2. Email・パスワード・ユーザー名を登録（以後この `<username>` を使う）
3. メール認証を完了

### 2. リポジトリを作る
1. 右上の「＋」→「New repository」
2. Repository name: `card-cabinet` （好きな名前でOK）
3. **Public** にチェック（Private は無料枠で Pages が使えない）
4. 「Create repository」

### 3. ファイルをアップロード
1. 作った空のリポジトリの画面で「uploading an existing file」リンクをタップ
2. 「choose your files」から以下の **5ファイルすべて** を選択:
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icon-192.png`
   - `icon-512.png`
   - `icon-512-maskable.png`
3. 下の「Commit changes」をタップ

### 4. Pagesを有効化
1. リポジトリの **Settings** タブを開く
2. 左メニュー「**Pages**」
3. Branch: `main` / Folder: `/ (root)` を選んで「Save」
4. 1〜2分待つと上に `Your site is live at https://<username>.github.io/card-cabinet/` と出る

### 5. Androidにインストール
1. そのURLをChromeで開く
2. メニュー（右上の︙）→「**ホーム画面に追加**」または「アプリをインストール」
3. 名前は "Cabinet" のまま追加
4. ホーム画面にアイコンができる → タップするとフルスクリーンでアプリ起動

---

## 🔄 共有するには

公開後の **URLを送るだけ** でOKです。  
相手もChromeでURLを開いて「ホーム画面に追加」すれば、相手の端末で自分のアプリになります。  
データは各人のブラウザ内 localStorage に保存されるので、あなたのカードは相手からは見えません。

---

## 🔧 アップデートしたいとき

`index.html` や `sw.js` を修正してGitHubに上げ直すと、リロード時に新しいバージョンが降ってきます。  
バージョンを変えたいときは `sw.js` の `const CACHE = 'card-cabinet-v1';` を `v2` に書き換えてください（古いキャッシュを捨てるため）。

---

## 💾 古いHTMLからデータ移行

前のスタンドアロンHTML (`pokemon_3d_collection.html`) でカードを追加してた場合:
1. 古いHTML版でメニュー → 「バックアップを書き出す」 → JSONファイル保存
2. 新しいPWA版でメニュー → 「バックアップから復元」 → そのJSONを選ぶ
3. 全部移行完了

---

## 🌐 別の公開方法（GitHubなしで）

**Netlify Drop** ([app.netlify.com/drop](https://app.netlify.com/drop))  
このフォルダをそのままドラッグ&ドロップ（モバイルだとフォルダ選択が少し面倒）

**Cloudflare Pages** - Git必須

GitHubが一番モバイルフレンドリーです。

---

## ❓ トラブルシュート

- 「ホーム画面に追加」が出ない → HTTPSでアクセスしているか確認（`https://` で始まるURL）
- インストール後に起動してもアイコンだけで白画面 → Service Workerがキャッシュ済みの古い画面を見てる。アプリを一度アンインストールして再インストール
- Three.jsのCDNが落ちてると起動不可 → オフライン対応のため、最初にオンライン時に一度開いてキャッシュさせる
