# CLAUDE.md

このファイルは、Claude Code がこのリポジトリで作業する際のガイダンスを提供します。

## プロジェクト概要

タスクボードアプリケーション。タスクの作成・管理・進捗追跡を行う Web アプリ。

## Git 運用ルール

### コード変更後は必ず GitHub にプッシュする

コードを変更するたびに、以下の手順で GitHub にプッシュすること：

```powershell
git add <変更ファイル>
git commit -m "変更内容の説明"
git push origin <ブランチ名>
```

- `git add .` や `git add -A` は使わず、変更したファイルを明示的に指定する
- コミットメッセージは変更の意図が伝わる日本語または英語で記述する
- プッシュ前に `git status` と `git diff` で変更内容を確認する
- main/master ブランチへの force push は行わない
- フックが失敗した場合は `--no-verify` でスキップせず、原因を修正する

### ブランチ戦略

- 新機能・修正は feature ブランチを切って作業する
- ブランチ名例: `feature/add-task-filter`, `fix/deadline-display`
- 完了後は GitHub でプルリクエストを作成してマージする

## 開発ルール

### コーディング規約

- コメントは「なぜ」が非自明な場合のみ記述する（何をするかはコードから読み取れる）
- 不要な抽象化・将来のための設計は避け、現在のタスクに必要な最小限の実装にする
- セキュリティ: ユーザー入力は必ずバリデーション・サニタイズする（XSS, SQL インジェクション等）

### ファイル・ディレクトリ構成

```
task-boad/
├── src/
│   ├── App.jsx       # メインコンポーネント（タスクボード全体）
│   ├── App.css       # グローバルスタイル
│   └── main.jsx      # エントリポイント
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Pages 自動デプロイ
├── index.html
├── vite.config.js
└── package.json
```

### 技術スタック

| 種別 | 技術 |
|------|------|
| UI ライブラリ | React 18 |
| ビルドツール | Vite 5 |
| スタイリング | Plain CSS（CSS Modules 不使用） |
| 状態管理 | React `useState` / `useEffect` |
| データ永続化 | localStorage |
| デプロイ | GitHub Actions + GitHub Pages |

### コンポーネント命名規約

- **ファイル名**: PascalCase（例: `App.jsx`, `TaskList.jsx`）
- **コンポーネント関数名**: PascalCase でファイル名と一致させる
- **CSS クラス名**: kebab-case（例: `.task-item`, `.add-btn`）
- **イベントハンドラ**: `handle` プレフィックス（例: `handleKeyDown`, `handleSubmit`）
- **state 更新関数の引数**: `prev` を使う（例: `setTasks(prev => ...)`）

## デプロイ先

**GitHub Pages**: https://zhenliruogui947-prog.github.io/task-board/

`main` ブランチへのプッシュで GitHub Actions が自動ビルド・デプロイを実行する。

## よく使うコマンド

```powershell
# 開発サーバー起動
npm run dev

# 本番ビルド
npm run build

# ビルド結果をローカルで確認
npm run preview
```
