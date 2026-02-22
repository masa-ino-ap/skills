# Claude Code Skills

[Claude Code](https://claude.ai/code) 用のカスタムスキル集です。

## スキル一覧

### ui-to-figma

WebアプリのUIを分析・改善し、Figma MCPサーバー経由でFigmaにデザインを送るワークフロースキル。

**使用場面:**
- 「UIを見てFigmaに送って」
- 「このページのデザインを改善してFigmaに反映して」
- 「UIを分析してFigmaにデザイン案を作って」

**前提:**
- Playwright（webapp-testingスキル）が利用可能であること
- Figma MCPサーバーが設定済みであること

詳細は [ui-to-figma/SKILL.md](./ui-to-figma/SKILL.md) を参照。

## インストール方法

```bash
# スキルディレクトリに配置する
cp -r ui-to-figma ~/.claude/skills/
```

## ライセンス

MIT
