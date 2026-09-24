# マンゲキランキングメーカー

渋谷よしもと漫才劇場（東京）とよしもと漫才劇場（大阪）の所属芸人を2択で並べかえて、
自分だけのランキング画像を作る非公式ファンサイトです。

- 劇場（東京／大阪）とメンバー区分（極／翔／全員）で対象を切り替え
- 全組でソート、または自分で選んだ組だけでソート
- 対戦中に「分からない」を押した組は以降の2択から自動で外れ、結果では最下位にまとめて並びます
- 結果はPNG画像として保存でき、Xの投稿画面をワンタップで開けます

## ファイル構成

| ファイル | 用途 |
|---|---|
| `index.html` | サイト本体（HTML・CSS・JSすべて1ファイル） |
| `favicon.svg` / `favicon.png` / `favicon.ico` | ファビコン |
| `apple-touch-icon.png` | iOSホーム画面用アイコン（180px） |
| `icon-512.png` | 大きめのアイコン素材 |
| `ogp.png` | OGP画像（1200×630） |
| `banner-1500x500.png` | Xヘッダーなどのバナー |
| `README.md` | このファイル |

外部依存はGoogle Fonts（Zen Kaku Gothic New / Oswald）だけです。ビルド作業はありません。
ローカルで確認したいときは `index.html` をブラウザにドラッグするだけで動きます。

---

## GitHubに置く

### ブラウザだけで済ませる場合

1. GitHubにログインし、右上の「+」→ New repository
2. Repository name に `mangeki-ranking-maker` などを入れ、Public のまま Create repository
3. 次の画面の「uploading an existing file」をクリック
4. このフォルダの中身（`index.html` や画像類）をまとめてドラッグ＆ドロップ
   - フォルダごとではなく、**中のファイルを直接**入れてください。`index.html` がリポジトリの一番上に来るのが正解です
5. 下の Commit changes を押す

### コマンドで済ませる場合

```bash
cd マンゲキランキングメーカーのフォルダ
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ユーザー名/mangeki-ranking-maker.git
git push -u origin main
```

---

## Cloudflare Pagesで公開する

1. [Cloudflareダッシュボード](https://dash.cloudflare.com/)にログイン
2. 左メニューの **Workers & Pages** → **Create** → **Pages** タブ → **Connect to Git**
3. GitHubアカウントを連携し、さきほどのリポジトリを選ぶ
4. ビルド設定を次のようにする（どれも空欄・None でかまいません）

   | 項目 | 値 |
   |---|---|
   | Production branch | `main` |
   | Framework preset | None |
   | Build command | （空欄） |
   | Build output directory | `/` |

5. **Save and Deploy** を押す。1分ほどで `https://プロジェクト名.pages.dev` が発行されます
6. 以降はGitHubにpushするだけで自動的に再デプロイされます

### 独自ドメインを使う場合

Pagesのプロジェクト → **Custom domains** → Set up a custom domain。
Cloudflareで管理しているドメインならDNSは自動で設定されます。

---

## 公開したあとに直すところ

**共有リンクは自動で入ります。** `index.html` の `SHARE_URL` は空のままでよく、
Xに投稿するときは開いているページのURLが自動で使われます。
固定したい場合だけ次のように書いてください。

```js
const SHARE_URL="https://あなたのドメイン/";
```

**OGP画像は絶対URLに直す必要があります。** Xやその他SNSでカードを表示させるには、
`index.html` の `<head>` にある次の3か所を公開URLに書き換えてください。

```html
<meta property="og:url" content="https://あなたのドメイン/">
<meta property="og:image" content="https://あなたのドメイン/ogp.png">
<meta name="twitter:image" content="https://あなたのドメイン/ogp.png">
```

書き換えたら [Card Validator](https://cards-dev.twitter.com/validator) などでキャッシュを更新すると、
反映が早くなります。

---

## 出演者データを更新する

`index.html` の中ほどにある4つの配列を編集してください。書式は `["コンビ名","メンバー / メンバー"]` です。
ピン芸人はメンバー欄を `""` にします。組数の表示や対戦回数の目安は自動で計算されます。

| 配列名 | 対象 |
|---|---|
| `TOKYO_KIWAMI` | 渋谷・極メンバー |
| `TOKYO_SHO` | 渋谷・翔メンバー |
| `OSAKA_KIWAMI` | 大阪・極メンバー |
| `OSAKA_SHO` | 大阪・翔メンバー |

データ元：
[渋谷よしもと漫才劇場 所属芸人一覧](https://shibuya-manzaigekijyo.yoshimoto.co.jp/profile/) /
[よしもと漫才劇場（大阪）所属芸人一覧](https://manzaigekijyo.yoshimoto.co.jp/profile/)

---

## 注意

非公式のファンサイトです。芸人名・劇場名などの権利は各権利者に帰属します。
利用者のデータはどこにも送信・保存していません（すべてブラウザ内で完結します）。

制作：ふかせ（[@F6rPd](https://x.com/F6rPd)）
