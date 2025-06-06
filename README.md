## アプリ概要
介護スタッフ向けの利用者記録活用アプリです。
Next.js（App Router） と Supabase（Auth + Database） を用いて、現場でよく記録される「体重記録」を
記録・一覧・グラフ表示できるシンプルな業務支援ツールを実装予定。
将来的には食事・排泄記録や申し送り管理機能も追加予定です。

## サイトイメージ
（後ほどアプリ完成後に画像キャプチャを貼る想定）

## サイトURL
（デプロイ後にURLを記載）

## 使用技術
- フロントエンド：Next.js 15.3（App Router）
- バックエンド：Next.js 15.3 API Routes
- データベース：Supabase PostgreSQL
- 認証：Supabase Auth（メール・パスワード認証）
- デプロイ：Vercel
- バージョン管理：Git、GitHub
- テスト・デバッグ：DevTools（Chrome）
- UIライブラリ：Shadcn UI（Toast通知・モーダル）
- CI/CD：GitHub Actions（ESLint実行）

## 設計ドキュメント
[要件定義・基本設計・詳細設計一覧（Googleスプレッドシート）]https://docs.google.com/spreadsheets/d/1dMkp3gGr8eLXPs4OQAAZqtBkeIdpUbkYJBrUoJkvikc/edit?usp=sharing
- 詳細設計時のワイヤーフレーム、ER図、ワークフロー図は /docs フォルダに格納。[こちらからアクセス](./docs)

## 機能一覧
- ユーザー登録・ログイン機能
- メールアドレス＋パスワードで認証
- 認証後に業務画面へ遷移
- 利用者管理機能（管理者専用）
- 利用者の新規追加・編集・削除
- 体重記録管理機能
- 日付・体重の記録追加・編集・削除
- 記録一覧表示
- 週・月切り替え可能な体重推移グラフ表示
- ナビゲーション機能
- 下部タブバー（介護記録・申し送り・管理者・ユーザー管理）
- どのページからでも機能切り替え可能
- エラーフィードバック通知
- 操作失敗時のみ右上にエラーメッセージ表示

## 📁 ディレクトリ構成（主要部分）

```
├── app/
│   ├── globals.css                # 全体CSS
│   ├── layout.tsx                 # ルートレイアウト
│   ├── page.tsx                   # ルートトップ（リダイレクト等）
│   │
│   ├── login/page.tsx            # ログイン画面
│   ├── dashboard/                # ログイン後の職員用ダッシュボード
│   │   ├── layout.tsx
│   │   └── page.tsx
│   │
│   ├── admin/                    # 管理者専用画面（職員・利用者管理）
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── users/
│   │   │   ├── page.tsx         # 職員一覧
│   │   │   ├── new/page.tsx     # 職員新規登録
│   │   │   └── edit/[id]/page.tsx # 職員編集
│   │   └── residents/
│   │       ├── page.tsx         # 利用者一覧
│   │       ├── new/page.tsx     # 利用者新規登録
│   │       └── edit/[id]/page.tsx # 利用者編集
│   │
│   ├── residents/[id]/weights/   # 体重記録（一覧・追加・編集）
│   │   └── page.tsx
│   │
│   └── api/                      # APIルート（開発用）
│       ├── create-user/route.ts  # 管理者による職員アカウント作成
│       └── reset-password/route.ts # パスワードリセット（予定）
│
├── components/
│   ├── layout/                   # ナビバー・ログアウト等共通レイアウト
│   ├── auth/                     # 認証関連（AuthGuardなど）
│   ├── admin/                    # 管理者用フォーム（職員・利用者）
│   ├── weight/                   # 体重記録関連（チャート・モーダルなど）
│   └── ui/                       # Shadcn UIコンポーネント拡張
│
├── context/
│   ├── auth-context.tsx          # ログイン状態管理
│   └── resident-context.tsx      # 選択中の利用者状態管理
│
├── hooks/
│   ├── useAuthLogic.ts           # 認証ロジックを抽出したカスタムフック
│   └── useToast.ts               # トースト通知用フック
│
├── lib/
│   ├── supabase.ts               # Supabaseクライアント初期化
│   ├── supabase-admin.ts         # サーバー専用Supabaseクライアント（Service Role）
│   ├── supabase-setup.ts         # Supabase初期設定用（未使用なら削除候補）
│   └── utils.ts                  # 汎用関数など（必要に応じて）
```

## 今後の開発予定

- 職員新規登録フォーム（管理者専用）
- 利用者編集・登録画面のバリデーション強化
- 「前へ・次へ」などの利用者ナビゲーション機能
- グラフ表示機能（体重の推移）
- 入力エラー・認証失敗時のUX改善（トースト通知など）

## 開発方針

- 現場の業務フローに沿ったUI／無駄のない操作導線を重視
- Supabase RLSによる**安全なデータ管理**
- **再利用可能なコンポーネント設計**と**文脈共有型の状態管理**


## テスト・修正の設計及び実施書
テスト・修正の設計及び実施書（Googleスプレッドシート）

## アプリの改善案
アプリの改善案（Googleスプレッドシート）

## 備考
活用した生成AIとその用途
 - ChatGPT：設計支援、リファクタリング、機能分解
 - v0：モックアップ作成支援
 - Copilot Chat：コード補助・バグ調査

リファクタリングルール
 - 再利用UIは /components 配置
 - 再利用関数は /lib 配置
 - 変数・関数命名はキャメルケース（例：isPublished）

