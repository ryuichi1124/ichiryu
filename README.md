# イチリュウ クリスマスケーキ予約サイト Shopifyテーマ

このリポジトリは、イチリュウのクリスマスケーキ予約サイト用のShopifyテーマです。

## 概要

- **テーマ名**: Dawn (カスタマイズ版)
- **対象サイト**: イチリュウ クリスマスケーキ予約サイト
- **カスタマイズ日**: 2025年11月

## 主なカスタマイズ内容

### 1. クリスマステーマカスタマイズ
- クリスマスカラーパレットの適用
- カスタムフォント（Playfair Display, Montserrat）の統合
- クリスマスバッジの追加（「事前予約特典」など）

### 2. 画像の組み込み
- **ヒーローバナー画像**: イチリュウクリスマスケーキのヒーロー画像をデフォルトとして設定
- **ロゴ画像**: 白文字/黒文字のロゴを動的に切り替え可能

### 3. カスタムスニペット
- `ichiryu-logo.liquid`: イチリュウロゴの表示用スニペット
- `christmas-badge.liquid`: クリスマスバッジ表示用スニペット

### 4. カスタムCSS
- `assets/christmas-theme.css`: クリスマステーマ用のカスタムスタイル

## ファイル構成

```
ichiryu/
├── assets/                        # テーマアセット（CSS、JS、画像など）
│   └── christmas-theme.css        # クリスマステーマ用カスタムCSS
├── config/                        # テーマ設定
│   ├── settings_data.json         # テーマの現在の設定
│   └── settings_schema.json       # テーマ設定のスキーマ
├── layout/                        # レイアウトテンプレート
│   ├── theme.liquid               # メインレイアウト（Google Fonts統合）
│   └── password.liquid            # パスワード保護ページレイアウト
├── locales/                       # 多言語対応ファイル
│   ├── ja.json                    # 日本語翻訳
│   └── en.default.json            # 英語翻訳（デフォルト）
├── sections/                      # セクションファイル
│   ├── header.liquid              # ヘッダー（ロゴ統合）
│   ├── image-banner.liquid        # ヒーローバナー（画像統合）
│   └── ...                        # その他のセクション
├── snippets/                      # 再利用可能なコードスニペット
│   ├── ichiryu-logo.liquid        # イチリュウロゴスニペット
│   ├── christmas-badge.liquid     # クリスマスバッジスニペット
│   └── ...                        # その他のスニペット
└── templates/                     # ページテンプレート
    ├── index.json                 # ホームページテンプレート
    ├── product.json               # 商品ページテンプレート
    └── ...                        # その他のテンプレート
```

## 使用方法

### 方法1: Shopify CLIを使用（推奨）

Shopify CLIを使用すると、テーマの開発とデプロイが簡単になります。

1. **Shopify CLIのインストール**
   ```bash
   npm install -g @shopify/cli @shopify/theme
   ```

2. **Shopifyストアにログイン**
   ```bash
   shopify auth login
   ```

3. **テーマをプッシュ**
   ```bash
   shopify theme push
   ```

4. **開発モードで作業**（リアルタイムプレビュー）
   ```bash
   shopify theme dev
   ```

### 方法2: ZIPファイルでアップロード

1. **ZIPファイルの作成**
   
   以下のファイル・ディレクトリを含むZIPファイルを作成：
   - `assets/`
   - `config/`
   - `layout/`
   - `locales/`
   - `sections/`
   - `snippets/`
   - `templates/`

   ⚠️ 注意: ZIPファイルのルートに直接これらのディレクトリが配置されるようにしてください。

   ```bash
   # Linuxまたはmacの場合
   zip -r ichiryu-theme.zip assets config layout locales sections snippets templates
   ```

2. **Shopify管理画面でアップロード**
   - Shopify管理画面にログイン
   - `オンラインストア` > `テーマ` に移動
   - `テーマライブラリ` セクションで `テーマをアップロード` をクリック
   - 作成したZIPファイルを選択してアップロード

3. **テーマの公開**
   - アップロードが完了したら、テーマをプレビュー
   - 問題がなければ `公開` をクリック

### 方法3: GitHubと連携

Shopifyストアは直接GitHubリポジトリと連携できます。

1. Shopify管理画面 > `オンラインストア` > `テーマ`
2. `GitHubから追加` をクリック
3. このリポジトリを選択して連携

## 画像URL

- **ヒーローバナー**: `https://cdn.shopify.com/s/files/1/0968/0689/5928/files/ichiryu_Xmas_H1_HI.jpg?v=1762394313`
- **ロゴ（白文字）**: `https://cdn.shopify.com/s/files/1/0968/0689/5928/files/ichiryulogod.png?v=1762394601`
- **ロゴ（黒文字）**: `https://cdn.shopify.com/s/files/1/0968/0689/5928/files/ichiryulogod2.png?v=1762394602`

## ライセンス

このテーマはShopifyのDawnテーマをベースにしています。

## 更新履歴

- **2025-11-06**: ZIPファイルを展開してShopify連携を可能に
  - テーマファイルをリポジトリのルートに配置
  - Shopify CLIでの開発・デプロイ方法を追加
  - GitHubとの直接連携オプションを追加
  - .gitignoreを更新して不要なファイルを除外

- **2025-11-06**: 初期カスタマイズ完了
  - クリスマステーマの適用
  - ヒーローバナー画像の統合
  - ロゴ画像の統合
  - カスタムCSSの追加

## 開発とテスト

### ローカル開発環境のセットアップ

1. **Shopify CLIのインストール**（まだインストールしていない場合）
   ```bash
   npm install -g @shopify/cli @shopify/theme
   ```

2. **開発サーバーの起動**
   ```bash
   shopify theme dev
   ```
   
   これにより、ローカルの変更がリアルタイムでShopifyストアのプレビューに反映されます。

3. **変更のテスト**
   - ブラウザで提供されたURLにアクセス
   - コードを編集すると自動的にリロードされます

### テーマのカスタマイズ

カスタムスニペットの使用例：

**イチリュウロゴの表示**
```liquid
{% render 'ichiryu-logo', logo_type: 'white', logo_width: 250 %}
```

**クリスマスバッジの表示**
```liquid
{% render 'christmas-badge', badge_text: '事前予約特典', badge_type: 'sale' %}
```

## トラブルシューティング

### テーマがアップロードできない場合
- ZIPファイルのルートに `assets/`, `config/`, `layout/`, `locales/`, `sections/`, `snippets/`, `templates/` ディレクトリが直接配置されているか確認
- 不要なファイル（`.DS_Store`, `__MACOSX`）が含まれていないか確認

### Shopify CLIでエラーが出る場合
- Shopify CLIが最新版か確認: `shopify version`
- 認証状態を確認: `shopify auth logout` してから `shopify auth login` で再ログイン

