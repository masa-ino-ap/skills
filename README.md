# Claude Code Skills

[Claude Code](https://claude.ai/code) 用のカスタムスキル集です。

## スキル一覧

### ui-to-figma

既存プロジェクトのCSS・Tailwind設定・コンポーネントを解析してデザイントークンを把握した上で、UIを視覚的に改善しFigma MCPサーバー経由でFigmaに送るワークフロースキル。

単なるUI改善ではなく「プロジェクトのデザインシステムに整合した改善」が特徴。新しい色や間隔をハードコードせず、既存トークン・命名規則の範囲内で提案する。

**使用場面:**
- 「UIを見てFigmaに送って」
- 「このページのデザインを改善してFigmaに反映して」
- 「UIを分析してFigmaにデザイン案を作って」

**前提:**
- 対象Webアプリのソースコードがローカルにあること
- 対象Webアプリがローカルで起動できること（`localhost:PORT`）
- Playwright（webapp-testingスキル）が利用可能であること
- Figma MCPサーバーが設定済みであること

詳細は [ui-to-figma/SKILL.md](./ui-to-figma/SKILL.md) を参照。

## インストール

```bash
npx skills add masa-ino-ap/skills@ui-to-figma -g -y
```

Claude Code、Cursor、Codex、Gemini CLI、Kiro CLI など主要AIエージェントに対応しています。

## ライセンス

MIT
