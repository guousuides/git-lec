# docs/images/ — スクリーンショット・GIF置き場

講座資料で使う画像素材を置く場所です。

## 必要な素材一覧

### 番外編2（AIエージェント）のライブデモ代替素材

[07_extra_ai_git.md](../07_extra_ai_git.md) から参照されています。
**ライブデモが動かなかった時の保険**なので、講座前に用意しておくと安心です。

| ファイル名 | 内容 | 撮り方 |
|---|---|---|
| `ai_demo_01_status.png` | AIが `git status` を実行し、日本語で状況説明している画面 | 指示例1を実行して静止画 |
| `ai_demo_02_commit.gif` | add → commit の流れ。**承認プロンプトが出る瞬間を必ず含める** | 指示例2を画面録画 |
| `ai_demo_03_pr.gif` | push → PR作成 → URLが返るまで | 指示例3を画面録画 |
| `ai_demo_04_danger.png` | AIが `push --force` を提案し、**人間が拒否する**画面 | 意図的に再現して静止画 |

> ⚠️ **撮影時は、APIキー・トークン・実名・メールアドレスが写り込んでいないか必ず確認してください。**
> このリポジトリはPublicです。

### 撮影のコツ

- **ターミナルのフォントを大きく**（16pt以上）。プロジェクターで後ろの席から読めるように
- **承認プロンプトの部分で1〜2秒止める**（GIFの場合）。ここが伝えたい山場です
- ファイルサイズは **5MB以下**に抑える（GitHubでの表示が重くなるため）

### GIFの作り方

| OS | ツール |
|---|---|
| Mac | QuickTime で画面収録 → [Gifski](https://gif.ski/) でGIF化 |
| Windows | Xbox Game Bar（Win + G）で録画 → [ScreenToGif](https://www.screentogif.com/) |
| 両対応 | [Kap](https://getkap.co/)（Mac）/ ScreenToGif（Win）が定番 |

## その他の素材

GUI版（[08_gui_version.md](../08_gui_version.md)）のスクリーンショットを足したい場合も、
ここに置いて相対パスで参照してください。

```markdown
![説明](images/ファイル名.png)
```
