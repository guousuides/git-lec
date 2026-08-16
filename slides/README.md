# スライド資料（Marp形式・イラスト図解版）

本ディレクトリ（`slides/`）には、Gitの基本概念と実践ハンズオンを取り入れた、GitHub入門講座（30分）用のプレゼンテーションスライドが含まれています。

## ファイル構成

- **`presentation.md`**：メインスライド（Marp形式 Markdown）
- **`images/`**：スライド内で使用している図解・イラスト素材
  - `01_file_chaos.jpg`：ファイル名「最終版_本当の最終.docx」の混乱
  - `02_version_tree.jpg`：Gitによる履歴管理とタイムマシン機能
  - `03_four_stages.jpg`：荷物の発送でたとえる4領域モデル（ワークツリー ➡️ インデックス ➡️ ローカル ➡️ リモート）
  - `04_pull_request.jpg`：Pull Requestとチーム開発・マージ
  - `05_ai_pairing.jpg`：AIエージェント（Claude Code / Copilot）と人間の協調開発

---

## 発表・閲覧方法

### 1. VS Code でスライド表示する（推奨）

1. VS Code 拡張機能 **「Marp for VS Code」** (`marp-team.marp-vscode`) をインストールします。
2. `slides/presentation.md` を開きます。
3. エディタ右上の **「Marp プレビューアイコン」**（または `Ctrl + Shift + V` / `Cmd + Shift + V`）を押します。
4. プレビュー画面上部のアイコンから **スライドショー（全画面表示）** を開始できます。

### 2. PDF / HTML / PPTX に変換・エクスポートする

#### VS Code 拡張機能を使う場合
- エディタ右上の Marp アイコン ➡️ **「Export slide deck...」** を選択し、形式（PDF / HTML / PPTX / PNG）を選択して保存します。

#### Marp CLI を使う場合（ターミナル操作）
```bash
# npx経由でHTMLに変換
npx @marp-team/marp-cli slides/presentation.md -o slides/presentation.html

# PDFに変換（※Google Chrome等のブラウザが必要です）
npx @marp-team/marp-cli slides/presentation.md --pdf -o slides/presentation.pdf
```

---

## スライド構成と時間配分（合計30分）

| パート | スライド番号 | 目安時間 | 内容 | 関連イラスト |
|---|---|---|---|---|
| **導入** | Slide 1〜5 | 3分 (00–03分) | タイトル、ゴール、安心宣言、タイムテーブル、環境クイックチェック | - |
| **第1章** | Slide 6〜8 | 4分 (03–07分) | **バージョン管理ってなに？**<br>ファイル名地獄の悲劇とGitによる解決（タイムマシン機能） | `01_file_chaos.jpg`<br>`02_version_tree.jpg` |
| **第2章** | Slide 9〜14 | 4分 (07–11分) | **Gitの仕組みと3大用語**<br>リポジトリ・コミット・ワークツリーとインデックス、荷物発送の4領域 | `03_four_stages.jpg` |
| **第3章** | Slide 15〜17 | 2分 (11–13分) | **ターミナルの基本**<br>カレントディレクトリ、`pwd` / `ls` / `cd` | - |
| **第4章** | Slide 18〜29 | 11分 (13–24分) | **【ハンズオン本編】**<br>clone ➡️ branch ➡️ 編集 ➡️ status/diff ➡️ add ➡️ commit ➡️ push ➡️ PR作成 ➡️ Merge | `04_pull_request.jpg` |
| **第5章** | Slide 30〜32 | 3分 (24–27分) | **草の確認**<br>プロフィールで草を確認、草が生えない3大罠（メアド不一致の修正等） | - |
| **第6章** | Slide 33〜39 | 3分 (27–30分) | **まとめ & AI時代のGit**<br>コンフリクト/revert、AI自動操作と人間がdiffを読む責任、ネクストステップ | `05_ai_pairing.jpg` |
