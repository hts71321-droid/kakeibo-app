# セットアップガイド（購入者向け）

所要時間：約15〜30分  
必要なもの：Googleアカウント、GitHubアカウント

---

## Step 1：GitHubにリポジトリを作る

1. [github.com](https://github.com) にログイン
2. 右上の「＋」→「New repository」をクリック
3. Repository name に好きな名前を入力（例：`kakeibo`）
4. **Public** を選択（GitHub Pages の無料枠に必要）
5. 「Create repository」をクリック

---

## Step 2：ファイルをアップロードする

1. 作成したリポジトリを開く
2. 「uploading an existing file」をクリック
3. 購入した `index.html` をドラッグ＆ドロップ
4. 「Commit changes」をクリック

---

## Step 3：GitHub Pages を有効にする

1. リポジトリの「Settings」タブ → 左メニュー「Pages」
2. Branch を `main` / `(root)` に設定して「Save」
3. しばらくすると `https://あなたのID.github.io/kakeibo/` でアクセスできるようになります

---

## Step 4：Firebase プロジェクトを作る

1. [firebase.google.com](https://firebase.google.com) にアクセス
2. 「コンソールへ移動」→「プロジェクトを追加」
3. プロジェクト名を入力（例：`kakeibo-family`）→ Google アナリティクスはオフでOK
4. 「プロジェクトを作成」をクリック

---

## Step 5：Realtime Database を作る

1. Firebase コンソール左メニュー「構築」→「Realtime Database」
2. 「データベースを作成」→ロケーションは `asia-southeast1`（シンガポール）を選択
3. セキュリティルールは **「テストモードで開始」** を選択して「有効にする」
4. 作成後、左メニュー「Realtime Database」→「ルール」タブを開き以下に変更して「公開」：

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

---

## Step 6：ウェブアプリを追加して設定値を取得する

1. Firebase コンソール「プロジェクトの概要」→「＜/＞」（ウェブアプリ追加）
2. アプリのニックネームを入力（なんでもOK）→「アプリを登録」
3. 表示される `firebaseConfig` の内容をコピーしておく

```javascript
// こういう形式のものが表示されます
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "xxx.firebaseapp.com",
  databaseURL: "https://xxx.firebasedatabase.app",
  projectId: "xxx",
  storageBucket: "xxx.firebasestorage.app",
  messagingSenderId: "000...",
  appId: "1:000...:web:xxx"
};
```

---

## Step 7：index.html に設定値を書き込む

1. ダウンロードした `index.html` をテキストエディタ（メモ帳・VS Codeなど）で開く
2. ファイル内の `firebaseConfig` という箇所を探す（Ctrl+F で検索）
3. Step 6 でコピーした内容に書き換える
4. 上書き保存

---

## Step 8：GitHub にアップロードして完了

1. Step 2 と同じ手順で、書き換えた `index.html` を再アップロード
2. `https://あなたのID.github.io/kakeibo/` にアクセスして動作確認

---

## 初回の使い方

1. アプリを開くと「ファミリーコード」の入力画面が表示される
2. 家族で共通の合言葉を決めて入力（例：`yamada-2025`）
3. 「このコードで始める」をタップ
4. 家族全員が **同じコード** を入力すれば、データが自動で同期されます

> ⚠️ ファミリーコードは他人に知られないようにしてください。コードを知っている人はデータを読み書きできます。

---

## よくある質問

**Q：スマホのホーム画面に追加したい**
Safari（iPhone）または Chrome（Android）の「共有」→「ホーム画面に追加」でアプリのように使えます。

**Q：複数の家族（世帯）で別々に使いたい**
それぞれ別のファミリーコードを使えば、データは完全に分離されます。

**Q：データのバックアップは？**
Firebase コンソールから JSON 形式でエクスポートできます。

**Q：Firebase の料金が心配**
支払い情報を登録しなければ一切課金されません。無料枠は家族数人の利用では十分です。
