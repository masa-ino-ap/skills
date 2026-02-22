# Figma MCP サーバー リファレンス

## Figma MCPとは

Claude Code for Figma は **Figma MCP Server** を通じてFigmaと連携する。
MCPサーバーがClaudeとFigmaのブリッジとなり、Figmaのフレーム・コンポーネント・スタイルをAPIで操作できる。

---

## セットアップ

### 1. Figma MCPスキルのインストール

```bash
npx skills add figma/mcp-server-guide@implement-design -g -y
```

### 2. Figma MCPサーバーのインストール

```bash
npm install -g @figma/mcp-server
```

### 3. Claude Desktop の設定

`~/.claude/claude_desktop_config.json` に追加:

```json
{
  "mcpServers": {
    "figma": {
      "command": "figma-mcp-server",
      "env": {
        "FIGMA_ACCESS_TOKEN": "your_figma_access_token"
      }
    }
  }
}
```

### 4. Figma Access Token の取得

1. Figma → Account Settings → Personal access tokens
2. 「Generate new token」でトークンを生成
3. 上記の `your_figma_access_token` に設定

---

## 主なMCP操作

### フレームの作成

```
figma.create_frame({
  name: "Improved UI - Desktop",
  width: 1440,
  height: 900,
  fileKey: "YOUR_FILE_KEY"  # FigmaファイルURLから取得
})
```

### テキストの追加

```
figma.create_text({
  content: "タイトル",
  fontSize: 24,
  fontWeight: "Bold",
  color: "#1A1A1A",
  x: 40, y: 40
})
```

### 矩形・コンポーネントの追加

```
figma.create_rectangle({
  width: 200, height: 48,
  fill: "#4F46E5",
  cornerRadius: 8,
  x: 40, y: 100
})
```

### スタイル（デザイントークン）の設定

```
figma.create_color_style({ name: "Primary/600", color: "#4F46E5" })
figma.create_text_style({ name: "Heading/H1", fontSize: 32, fontWeight: "Bold" })
figma.create_effect_style({ name: "Shadow/Card", ... })
```

---

## デザイントークン抽出パターン

UIコードからデザイントークンを抽出してFigmaに送る:

```python
# CSS変数やTailwindクラスからカラーパレットを抽出
import re

def extract_colors(css_content):
    # CSS変数パターン
    colors = re.findall(r'--[\w-]+:\s*(#[0-9a-fA-F]{3,8}|rgb[a]?\([^)]+\))', css_content)
    return list(set(colors))

def extract_spacing(css_content):
    # スペーシング値の抽出
    spacing = re.findall(r'(?:margin|padding|gap):\s*(\d+(?:\.\d+)?(?:px|rem|em))', css_content)
    return list(set(spacing))
```

---

## FigmaファイルキーのURLからの取得

```
https://www.figma.com/file/XXXXXXXXXXX/My-Design
                           ^^^^^^^^^^^
                           これがfileKey
```

---

## よくある問題

| 問題 | 原因 | 対処 |
|------|------|------|
| 認証エラー | トークン期限切れ・権限不足 | Figmaで新トークン生成 |
| ファイルが見つからない | fileKeyが間違い | FigmaのURLから再確認 |
| MCP接続失敗 | サーバー未起動 | `figma-mcp-server` を再起動 |
| レート制限 | API呼び出しが多い | 操作をバッチ化・待機を追加 |
