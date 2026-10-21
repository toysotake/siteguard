# SiteGuard JS — セキュリティ簡易診断

構成は静的フロントエンド `index.html` + Cloudflare Worker `worker.js`。PHP不要。

## 公開

1. Node.jsを入れ、Cloudflareアカウントで `npx wrangler login`
2. このフォルダ内で `npx wrangler deploy` を実行
3. 発行された `https://...workers.dev` のURLを控える
4. `index.html` の `const endpoint=...` をそのURLへ変更（末尾の `/` は省略）
5. `index.html` を GitHub Pages などに配置

ローカルWorker実行：`npx wrangler dev` → HTML内の標準設定 `http://localhost:8787` を利用（ブラウザのCORS設定に注意）。

## 注意点

- 公開ドメイン名のみ対応、リダイレクトは追跡しません。
- 1回のHTTP GETから取得できる情報だけを判定。脆弱性を実際に突く検査はありません。
- ヘッダーが欠けていることだけで直ちに「脆弱性あり」と断定しないでください。
- Cloudflareの実行環境によっては `Set-Cookie` の取得に制約があります。
- フロントの結果は簡易評価です。正式な脆弱性診断や監査ではありません。
- 本番公開前にレート制限、CAPTCHA、監視、利用規約、対象所有権確認を追加してください。
- サーバー側でのDNS解決や接続先制御はCloudflareの仕様にも依存します。SSRF対策のための厳密な運用をする場合は追加のアクセス制御が必要です。
