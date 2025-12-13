# 開発ワークフロー

このドキュメントでは、プロジェクトの開発フローを説明します。

---

## 🚀 クイックスタート

```bash
# 1. リポジトリをクローン
git clone https://github.com/[username]/[project].git
cd [project]

# 2. 依存関係をインストール
npm install

# 3. 開発サーバーを起動
npm run dev
```

---

## 📁 プロジェクト構成

```
project/
├── src/               # ソースコード
├── public/            # 静的ファイル
├── docs/              # ドキュメント
├── .kiro/steering/    # SDDドキュメント
├── .agent/workflows/  # AIワークフロー
└── dist/              # ビルド出力（.gitignore）
```

---

## 🔧 利用可能なコマンド

| コマンド | 説明 |
|----------|------|
| `npm run dev` | 開発サーバー起動 |
| `npm run build` | 本番ビルド |
| `npm run type-check` | 型チェック |
| `npm run lint` | Lintチェック |
| `npm run test` | テスト実行 |

---

## 🌿 ブランチ戦略

> ⚠️ **重要**: 機能開発を開始する前に、必ずフィーチャーブランチを作成すること。

### ブランチの種類

| ブランチ | 用途 |
|----------|------|
| `main` | 安定版（本番） |
| `feature/*` | 新機能開発 |
| `bugfix/*` | バグ修正 |
| `hotfix/*` | 緊急修正 |

### ワークフロー

```bash
# 1. mainを最新に
git checkout main
git pull origin main

# 2. フィーチャーブランチ作成
git checkout -b feature/my-feature

# 3. 開発・コミット
git add -A
git commit -m "feat: 新機能を追加"

# 4. プッシュ
git push origin feature/my-feature

# 5. マージ
git checkout main
git merge feature/my-feature
git push origin main
```

---

## 📝 コミットメッセージ規則

```
<type>: <description>
```

### Type一覧

| Type | 説明 |
|------|------|
| `feat` | 新機能 |
| `fix` | バグ修正 |
| `docs` | ドキュメント |
| `refactor` | リファクタリング |
| `chore` | 設定・ビルド |
| `style` | コードスタイル |
| `test` | テスト |

### 例

```
feat: ユーザー認証機能を追加
fix: ログイン時のエラーを修正
docs: READMEを更新
```

---

## 🚢 デプロイ

### 本番デプロイ

```bash
# 1. mainブランチで実行
git checkout main

# 2. ビルド
npm run build

# 3. デプロイ（例: Firebase）
firebase deploy --only hosting
```

### プレビューデプロイ

```bash
firebase hosting:channel:deploy preview --expires 7d
```

---

## 📚 ドキュメント

| ファイル | 説明 |
|----------|------|
| `.kiro/steering/requirements.md` | 要件定義 |
| `.kiro/steering/design.md` | 設計ドキュメント |
| `.kiro/steering/tasks.md` | タスク管理 |
| `docs/SPECIFICATION.md` | 詳細仕様 |
| `CHANGELOG.md` | 変更履歴 |

---

## 🔄 CI/CD（任意）

### GitHub Actions 設定例

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run build
      - run: firebase deploy --only hosting
        env:
          FIREBASE_TOKEN: ${{ secrets.FIREBASE_TOKEN }}
```

---

## ❓ トラブルシューティング

### ビルドエラー

```bash
# node_modulesを再インストール
rm -rf node_modules
npm install
```

### 型エラー

```bash
# 型チェック
npm run type-check
```
