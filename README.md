# 保育記録システム — セットアップガイド

## 全体の流れ（所要時間：30〜60分）

```
Firebase作成（15分）→ Vercelにデプロイ（5分）→ 各端末にインストール（5分）
```

---

## STEP 1 ｜ Firebase プロジェクトを作成する

1. https://console.firebase.google.com にアクセス（Googleアカウントでログイン）
2. 「プロジェクトを作成」をクリック
3. プロジェクト名を入力（例：`hoiku-record`）→ 続行
4. Google アナリティクスは「無効」で OK → プロジェクトを作成

---

## STEP 2 ｜ Realtime Database を有効にする

1. 左サイドバー「構築」→「Realtime Database」をクリック
2. 「データベースを作成」→ 地域は **us-central1** または **asia-southeast1** を選択
3. セキュリティルールは「**テストモード**で開始」を選択 → 有効にする
4. ルールタブを開き、以下に書き換えて「公開」（内部ツールなので簡易ルールでOK）:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

---

## STEP 3 ｜ アプリの設定情報を取得する

1. Firebaseコンソール → 左上の歯車アイコン →「プロジェクトの設定」
2. 「マイアプリ」セクションまでスクロール →「</>」（ウェブ）をクリック
3. アプリのニックネームを入力（例：`保育記録PWA`）→ 「アプリを登録」
4. 表示された `firebaseConfig` の各値をメモしておく

```js
// このような形で表示されます
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "hoiku-record.firebaseapp.com",
  databaseURL: "https://hoiku-record-default-rtdb.firebaseio.com",
  projectId: "hoiku-record",
  storageBucket: "hoiku-record.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef"
};
```

---

## STEP 4 ｜ アイコン画像を用意する（任意・推奨）

以下のサイトで無料生成できます：
- https://favicon.io/favicon-generator/

「Text」タブで好きな文字（例：「保」）を入力し、背景色 `#1D9E75`・文字色 `#ffffff` に設定してダウンロード。
`icon-192.png` と `icon-512.png` をこのフォルダに追加してください。

なくてもアプリは動きます。

---

## STEP 5 ｜ Vercel にデプロイする（無料）

### 方法A：ドラッグ＆ドロップ（最も簡単）
1. https://vercel.com にアクセスしてアカウント作成（GitHubアカウントでOK）
2. ダッシュボードの「Add New → Project」
3. 「Browse」からこのフォルダを選択してドラッグ＆ドロップ
4. 設定はそのまま「Deploy」をクリック
5. デプロイ完了後、`https://your-project.vercel.app` のURLが発行される

### 方法B：GitHub経由（更新が楽）
1. このフォルダをGitHubリポジトリに push
2. Vercelでリポジトリを選択して連携
3. 以後、ファイルを更新してpushするだけで自動デプロイ

---

## STEP 6 ｜ 各端末で初回設定をする

1. スマホ・タブレットのブラウザで発行されたURLを開く
2. 「初回セットアップ」画面が表示される
3. STEP 3 でメモした値を入力して「接続して開始する」をタップ
4. 接続成功後、アプリが起動する

> 設定は端末ごとに1回だけ必要です。以後はURLを開くだけで使えます。

---

## STEP 7 ｜ ホーム画面に追加する（PWAインストール）

### iPhone / iPad（Safari）
1. 下部の共有ボタン（□↑）をタップ
2. 「ホーム画面に追加」を選択
3. 名前を確認して「追加」をタップ

### Android（Chrome）
1. アプリ内に「ホーム画面に追加」バナーが表示される
2. 「追加する」をタップ
   ※ 表示されない場合：Chromeメニュー（⋮）→「ホーム画面に追加」

---

## 費用について

| サービス | 無料枠 |
|---|---|
| Firebase Realtime Database | 1GB ストレージ・10GB/月 転送量 |
| Vercel | 100GB/月 帯域・無制限デプロイ |

保育園1〜2クラス規模の利用であれば、**ほぼ永続的に無料**で使えます。

---

## よくある質問

**Q: 先生のスマホが変わったら？**  
A: 新しいスマホでURLを開き、同じ設定情報を入力するだけです。データはFirebase上にあるので引き継がれます。

**Q: オフラインでも使える？**  
A: ホーム画面からアプリとして開いている場合、基本的な画面表示はオフラインでも可能です。データの追加・同期にはネット接続が必要です。

**Q: データのバックアップは？**  
A: Firebaseコンソール → Realtime Database → データのエクスポート（JSON）でバックアップできます。

**Q: セキュリティが心配**  
A: 現在の設定はURLを知っている人なら誰でもアクセスできます。より厳密にする場合は Firebase Authentication（メール認証）の追加をご相談ください。
