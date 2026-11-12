# Markdown Design

VS Code標準のMarkdownプレビューを読みやすくする、CSSベースの拡張機能です。
`markdown.previewStyles` でプレビューにスタイルを追加します。実行時のJavaScriptやビルド処理は不要です。

## 現在できること

- 見出しの階層を下線・左罫線・余白で明確化
- 表のヘッダー・罫線・交互背景を調整
- 引用を共通のカード風デザインで表示
- コードブロック、チェックリスト、`<details>` の見た目を調整
- VS Codeテーマの色と、既存のMarkdownフォント設定を利用

編集画面やVS Code本体のUIは変更しません。チェックリストは表示のみで、クリックしてMarkdownを書き換える機能はありません。

## 開発を始める

1. VS Code **1.100.0以上**でこのリポジトリを開きます。
2. `F5` を押し、`Markdown Design: 拡張をデバッグ` を起動します。
3. 起動したExtension Development Hostで `examples/preview.md` を開きます。
4. `Ctrl+Shift+V`、または「Markdown: Open Preview」で表示します。
5. `styles/preview.css` を編集し、開発ホストで「Developer: Reload Window」を実行して再確認します。

CSSのみのため、開発ホストでの確認に `npm install` やコンパイルは不要です。

## ファイル構成

```text
.
├─ .vscode/launch.json  # F5で拡張開発ホストを起動
├─ examples/preview.md # 表示確認用サンプル（配布対象外）
├─ styles/preview.css  # プレビュー用CSS
├─ .vscodeignore       # VSIXに含めないファイル
├─ package.json        # 拡張機能の定義
├─ LICENSE
└─ README.md
```

## VSIXを作成・インストール

Node.js 22以上とnpmが使える環境で実行します。パッケージ作成時は `npx` が `@vscode/vsce` を取得するため、ネットワーク接続が必要です。

```sh
npm run package
code --install-extension vscode-markdown-design-0.0.1.vsix
```

VS Codeの拡張機能画面にある「Install from VSIX...」からもインストールできます。
この操作はMarketplaceへ公開しません。`publisher` はリポジトリ所有者に合わせた仮の識別子 `crttc-ssato` です。Marketplace公開時は登録済みのPublisher IDに合わせてください。

## 表示確認

`examples/preview.md` で以下を確認します。

- ライト・ダーク・ハイコントラストの各テーマで文字と罫線が読めること
- 狭いプレビューペインでも本文、表、コードが読めること
- 見出し・引用・表・チェックリストの余白が適切なこと
- `<details>` がマウスとキーボードで開閉できること
- `markdown.preview.fontSize` / `markdown.preview.fontFamily` の設定が反映されること

他のMarkdownスタイル拡張や `markdown.styles` を併用すると、CSSが競合する場合があります。

## 今後の拡張候補

- `[!NOTE]` / `[!WARNING]` / `[!DECISION]` / `[!TODO]` を種類別のカードとして描画するMarkdown-itプラグイン
- プロジェクト共通のフォントサイズ・余白などの設定
- Mermaid描画環境と組み合わせた図のスタイル調整

このひな型は独自記法の解析やMermaidの描画エンジンを含みません。引用は共通スタイルで表示し、VS Codeや別拡張が追加する描画機能はそれぞれの環境に依存します。

拡張ポイントの詳細は [VS Code公式のMarkdown拡張ガイド](https://code.visualstudio.com/api/extension-guides/markdown-extension) を参照してください。

## ライセンス

MIT
