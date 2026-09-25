# マンゲキ好き順メーカー

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
2. Repository name を入れて Create repository（private でも public でも公開できます）
3. 次の画面の「uploading an existing file」をクリック
4. このフォルダの**中のファイル**をまとめてドラッグ＆ドロップ（フォルダごとではなく中身を直接）
5. Commit changes

`index.html` がリポジトリの一番上にあればOKです。

### コマンドの場合

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ユーザー名/リポジトリ名.git
git push -u origin main
```

---

## Cloudflareで公開する

Cloudflareの「Create an app」画面はWorkers用に変わっています。静的サイトはPagesの導線から作ります。

1. Cloudflareダッシュボード → Compute → **Workers & Pages** → **Create**
2. 画面下の小さなリンク **Continue to Pages**（Need to use the legacy Pages workflow? の横）をクリック
3. **Import an existing Git repository** の Get started
4. GitHubを連携してリポジトリを選択 → Begin setup
5. 設定を次のとおりにする

   | 項目 | 値 |
   |---|---|
   | Project name | 好きな名前（これがURLになります） |
   | Production branch | `main` |
   | Framework preset | None |
   | Build command | 空欄 |
   | Build output directory | `/` |

6. **Save and Deploy**。1分ほどで `https://プロジェクト名.pages.dev` が発行されます

以降はGitHubにpushするたびに自動で再デプロイされます。

### 独自ドメインを使う場合

プロジェクト画面 → Custom domains → Set up a custom domain。
Cloudflareで管理しているドメインならDNSは自動設定されます。

---

## 公開したあとに直すところ

共有リンクとOGPは `https://mngksort.pages.dev/` 向けに設定済みです。
独自ドメインに変える場合のみ、下の「URLの設定について」を参照してください。

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

---

## URLの設定について

公開URL `https://mngksort.pages.dev/` を前提に設定済みです。書き換えは不要です。

- Xの投稿文に入るリンク：`index.html` 冒頭の `const SHARE_URL="https://mngksort.pages.dev/";`
- OGP：`<head>` の `og:url` / `og:image` / `twitter:image`

独自ドメインに変えたときだけ、この4か所を新しいURLに直してください。
