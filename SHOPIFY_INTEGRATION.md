# Shopify連携ガイド

このドキュメントでは、イチリュウのShopifyテーマをShopifyストアと連携する方法を詳しく説明します。

## 前提条件

- Shopifyストアへの管理者アクセス権
- Node.js（Shopify CLIを使用する場合）
- Gitがインストールされていること（GitHub連携を使用する場合）

## 連携方法の比較

| 方法 | 難易度 | 推奨度 | メリット | デメリット |
|------|-------|-------|---------|----------|
| Shopify CLI | 中 | ★★★★★ | リアルタイムプレビュー、バージョン管理が容易 | CLIのセットアップが必要 |
| GitHub連携 | 易 | ★★★★☆ | 自動同期、コラボレーションが容易 | GitHubアカウントが必要 |
| ZIPアップロード | 易 | ★★★☆☆ | 最もシンプル | 手動更新が必要 |

## 方法1: Shopify CLI（推奨）

### ステップ1: Shopify CLIのインストール

```bash
# npmを使用してインストール
npm install -g @shopify/cli @shopify/theme

# インストールの確認
shopify version
```

### ステップ2: Shopifyストアに接続

```bash
# リポジトリのディレクトリに移動
cd /path/to/ichiryu

# Shopifyにログイン
shopify auth login
```

ブラウザが開き、Shopifyストアにログインを求められます。

### ステップ3: テーマをプッシュ

```bash
# 既存のテーマとして追加
shopify theme push

# または、新しいテーマとして追加
shopify theme push --unpublished --theme-name="イチリュウ クリスマスケーキ"
```

### ステップ4: 開発モードで作業（オプション）

```bash
# リアルタイムプレビューで開発
shopify theme dev

# 特定のストアで開発
shopify theme dev --store=your-store.myshopify.com
```

開発サーバーが起動し、URLが表示されます（例：`http://127.0.0.1:9292`）。このURLにアクセスすると、ローカルの変更がリアルタイムで反映されます。

### ステップ5: テーマの公開

Shopify管理画面で：
1. `オンラインストア` > `テーマ` に移動
2. アップロードしたテーマを見つける
3. `カスタマイズ` でプレビュー
4. 問題がなければ `公開` をクリック

## 方法2: GitHub連携

### ステップ1: GitHubリポジトリの準備

このリポジトリは既にGitHubに存在しているため、このステップはスキップできます。

### ステップ2: Shopifyとの連携

1. Shopify管理画面にログイン
2. `オンラインストア` > `テーマ` に移動
3. `GitHubから追加` ボタンをクリック
4. GitHubアカウントを認証
5. `ryuichi1124/ichiryu` リポジトリを選択
6. `copilot/expand-zip-file-for-shopify` ブランチを選択
7. `接続` をクリック

### 自動同期の仕組み

GitHub連携を使用すると：
- ブランチにプッシュするたびに、Shopifyテーマが自動的に更新されます
- Shopify管理画面でテーマをカスタマイズすると、変更がGitHubにコミットされます

## 方法3: ZIPファイルでアップロード

### ステップ1: ZIPファイルの作成

```bash
# リポジトリのルートディレクトリで実行
cd /path/to/ichiryu

# 必要なディレクトリをZIP化
zip -r ichiryu-theme.zip assets config layout locales sections snippets templates

# またはGitリポジトリ全体から（不要なファイルを除外）
git archive --format=zip --output=ichiryu-theme.zip HEAD assets config layout locales sections snippets templates
```

### ステップ2: Shopifyにアップロード

1. Shopify管理画面にログイン
2. `オンラインストア` > `テーマ` に移動
3. `テーマライブラリ` セクションまでスクロール
4. `テーマをアップロード` ボタンをクリック
5. 作成したZIPファイルを選択
6. アップロードが完了するまで待機

### ステップ3: テーマの確認と公開

1. アップロードされたテーマの `アクション` > `プレビュー` をクリック
2. すべてが正常に表示されることを確認
3. `アクション` > `公開` をクリックしてテーマを有効化

## テーマのカスタマイズ

テーマをアップロードした後、Shopify管理画面でカスタマイズできます：

1. `オンラインストア` > `テーマ` > `カスタマイズ` をクリック
2. 左側のパネルでセクションや設定を変更
3. 右側でリアルタイムプレビューを確認
4. 完了したら `保存` をクリック

### カスタマイズ可能な項目

- **ヘッダー**: ロゴの表示・サイズ変更
- **ヒーローバナー**: 画像やテキストの変更
- **カラースキーム**: クリスマステーマの色調整
- **フォント**: Playfair Display、Montserratの設定
- **商品ページ**: レイアウトと表示オプション

## トラブルシューティング

### アップロードが失敗する場合

**問題**: ZIPファイルのアップロードが失敗する

**解決策**:
1. ZIPファイルのサイズを確認（50MB以下である必要があります）
2. ZIPファイルのルートに必要なディレクトリが配置されているか確認
3. 不要なファイル（`.DS_Store`, `__MACOSX`, `.git`）を除外

### Shopify CLIでエラーが出る場合

**問題**: `shopify theme push` でエラーが発生

**解決策**:
1. Shopify CLIが最新版か確認: `shopify upgrade`
2. 認証をリセット: `shopify auth logout` してから `shopify auth login`
3. ストアのURLを明示的に指定: `shopify theme push --store=your-store.myshopify.com`

### GitHub連携が機能しない場合

**問題**: GitHubへのプッシュ後、Shopifyテーマが更新されない

**解決策**:
1. Shopify管理画面で連携状態を確認
2. 正しいブランチが選択されているか確認
3. GitHub Actionsのログを確認（リポジトリに設定されている場合）

### テーマのプレビューが正しく表示されない場合

**問題**: カスタム画像やロゴが表示されない

**解決策**:
1. Shopify CDNの画像URLが正しいか確認
2. `snippets/ichiryu-logo.liquid` のURLを確認
3. 必要に応じて、Shopify管理画面からファイルタブで画像を再アップロード

## テーマの更新

### Shopify CLIを使用している場合

```bash
# 変更をコミット
git add .
git commit -m "テーマの更新"

# Shopifyにプッシュ
shopify theme push
```

### GitHub連携を使用している場合

```bash
# 変更をコミットしてプッシュ
git add .
git commit -m "テーマの更新"
git push origin copilot/expand-zip-file-for-shopify
```

Shopifyが自動的に変更を検出して更新します。

### ZIPアップロードを使用している場合

1. 新しいZIPファイルを作成
2. Shopify管理画面で再度アップロード
3. 古いバージョンのテーマを削除

## ベストプラクティス

1. **バージョン管理**: 常にGitでバージョン管理を行う
2. **テスト環境**: 本番環境にプッシュする前に、開発テーマでテストする
3. **バックアップ**: 重要な変更の前にテーマをダウンロードしてバックアップ
4. **ドキュメント化**: カスタマイズ内容を `README.md` に記録
5. **段階的な更新**: 大きな変更は小さな変更に分割して段階的に適用

## サポート

問題が発生した場合：

1. このドキュメントのトラブルシューティングセクションを確認
2. [Shopify公式ドキュメント](https://shopify.dev/themes)を参照
3. [Shopify Community Forums](https://community.shopify.com/)で質問
4. GitHubリポジトリでIssueを作成

## 参考リンク

- [Shopify CLI ドキュメント](https://shopify.dev/themes/tools/cli)
- [Shopify Theme 開発ガイド](https://shopify.dev/themes)
- [Liquid テンプレート言語](https://shopify.github.io/liquid/)
- [Dawn テーマリファレンス](https://github.com/Shopify/dawn)
