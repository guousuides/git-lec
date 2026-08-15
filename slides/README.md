# slides/ — 講義スライド

**現在、この講座のスライドは2つあります。** 当日どちらを使うか決めてください。

| ファイル | 特徴 |
|---|---|
| [`presentation.md`](presentation.md) + [`presentation.pdf`](presentation.pdf) | **既存の完成版。** 全編カバー済み、PDF書き出し済み。デザインも作り込み済み |
| [`30min.md`](30min.md) | **発表者ノート付き版。** 各スライドに【経過時刻】と進行の指示を埋め込んである |
| [`theme.css`](theme.css) | Cypher配色テーマ（**任意。無くても動きます**） |

> 💡 **迷ったら `presentation.pdf` を使ってください。** すでに書き出し済みで、当日そのまま投影できます。
> `30min.md` の発表者ノート（時間配分・「ここで全員に打たせる」等）は
> [facilitator_guide.md](../facilitator_guide.md) にも同じ内容が表形式で入っています。

---

## 2つのスライドの使い分け

| 場面 | 推奨 |
|---|---|
| 当日そのまま投影する | **`presentation.pdf`** |
| 進行台本が欲しい | **`30min.md`**（またはfacilitator_guide.md） |
| 中身を編集したい | どちらか一方に統一してから編集を推奨 |

**片方に統一する場合**：不要な方を削除して構いません。
`30min.md` を消す場合、[facilitator_guide.md](../facilitator_guide.md) に時間配分表とトラブル対応が
すべて入っているので、進行情報は失われません。

---

## そのまま見る

GitHub上で `.md` を開けば、Markdownとして読めます。
**発表者ノート（`<!-- -->` 内）は表示されませんが、内容は追えます。**

---

## スライドとして表示する

### 方法1：VS Code拡張（いちばん簡単・推奨）

1. VS Codeで拡張機能 **Marp for VS Code** をインストール
2. `slides/presentation.md` または `slides/30min.md` を開く
3. 右上の**プレビューアイコン**をクリック

これだけでスライド表示になります。**`theme.css` の設定は不要です**
（どちらの `.md` も frontmatter にスタイルを内蔵しているため）。

### 方法2：HTML / PDF に書き出す

```bash
npx @marp-team/marp-cli slides/30min.md -o slides/30min.html
```

```bash
npx @marp-team/marp-cli slides/30min.md --pdf -o slides/30min.pdf
```

```bash
# 発表者ノート付きPowerPoint
npx @marp-team/marp-cli slides/30min.md --pptx -o slides/30min.pptx
```

> ⚠️ `presentation.md` は Google Fonts を `@import` しています。
> **オフライン環境ではフォントが読み込めないため、必ず事前にPDFを書き出しておいてください。**
> （`presentation.pdf` は書き出し済みです）

### 方法3：theme.css をテーマとして使う

`theme.css` を正式なテーマとして読み込みたい場合：

1. 対象の `.md` の frontmatter を `theme: default` → `theme: cypher` に変更
2. 以下で実行：

```bash
npx @marp-team/marp-cli --theme slides/theme.css slides/30min.md -o slides/30min.html
```

VS Code拡張で使う場合は `settings.json` に：

```json
{
  "markdown.marp.themes": ["./slides/theme.css"]
}
```

> ⚠️ **この設定をしないまま `theme: cypher` にすると、ビルドがエラーになります。**
> 迷ったら `theme: default` のまま使ってください。

---

## 発表者ノートについて（`30min.md`）

各スライドの末尾に `<!-- -->` で囲まれたノートがあります。

```markdown
<!--
【12:00】
・ここで全員に打たせる
・pwd確認を飛ばすと後で全滅する
-->
```

- **【 】内は経過時刻の目安**です
- 詳しい時間配分とトラブル対応 → [facilitator_guide.md](../facilitator_guide.md)

---

## 講座前チェック

- [ ] どちらのスライドを使うか決めた
- [ ] PDF版を用意して、オフラインでも出せる状態にした
- [ ] プロジェクターで後ろの席からコードブロックが読めるか確認した
- [ ] 番外編2のデモ素材（GIF/スクショ）を `docs/images/` に配置した
- [ ] [facilitator_guide.md](../facilitator_guide.md) の時間配分表に目を通した
