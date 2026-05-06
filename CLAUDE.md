# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

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
