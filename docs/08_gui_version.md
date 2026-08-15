# 08. VS Code GUI版 — マウス操作だけで全部やる

**所要：12分（本編と同じ内容）** ｜ 対応：[04. ハンズオン本編](04_branch_pr.md) のGUI版

このページのゴール：**ターミナルを1回も使わずに、PRをmergeまで持っていく。**

> 💡 **CLI版（[04](04_branch_pr.md)）とGUI版、どちらでも結果は同じです。**
> 当日、講師が主線をアナウンスしますが、**途中でこちらに乗り換えても構いません。**
> 「黒い画面が無理」と思ったら、遠慮なくこのページに来てください。

---

## 前提知識だけは共通です

**マウスでやる場合でも、以下の3つは知っておく必要があります。**

| 概念 | 資料 |
|---|---|
| **カレントディレクトリ**（今どこにいるか） | [00_terminal_basics.md](00_terminal_basics.md#最重要パスとカレントディレクトリ) |
| **4領域モデル**（変更がどこにあるか） | [01_git_vs_github.md](01_git_vs_github.md#4領域モデル) |
| **diffの読み方**（`+` と `-`） | [01_git_vs_github.md](01_git_vs_github.md#git-diff-は何を変えたかを見せてくれる) |

**GUIはコマンドを隠してくれますが、概念は隠してくれません。**
ボタンの名前が違うだけで、裏で動いているものは同じです。

### ボタンとコマンドの対応表

| VS Codeの操作 | 実行されるコマンド | 4領域 |
|---|---|---|
| Clone Repository | `git clone` | ④ → ①③ |
| ブランチ名をクリック → Create new branch | `git switch -c` | — |
| ファイル横の **+** | `git add` | ① → ② |
| **✓ Commit** ボタン | `git commit` | ② → ③ |
| **Sync Changes** / **Publish Branch** | `git push` | ③ → ④ |
| Source Controlの ↻ / Pull | `git pull` | ④ → ① |

**「今どのボタンが、どの矢印なのか」を意識すると、CLIに移行する時も迷いません。**

---

## STEP 0：準備（2分）

### 0-1. VS Codeをインストール

https://code.visualstudio.com/ からダウンロードして起動してください。

### 0-2. 日本語化する（任意・おすすめ）

1. 左端の**四角が4つ並んだアイコン**（Extensions / 拡張機能）をクリック
2. 検索欄に `Japanese` と入力
3. **Japanese Language Pack for Visual Studio Code** の **Install** を押す
4. 右下に出る **Change Language and Restart** を押す

> 💡 このページは**英語表示のまま**の名前で説明します（日本語名も併記します）。
> 日本語化した人は、括弧内の日本語を探してください。

### 0-3. 画面の見方

VS Codeの**左端に縦に並んだアイコン**を「アクティビティバー」と呼びます。

| アイコン | 名前 | 用途 |
|---|---|---|
| 📄 書類が2枚 | **Explorer**（エクスプローラー） | ファイル一覧 |
| 🔍 虫めがね | Search（検索） | 検索 |
| **⑂ 枝分かれした線** | **Source Control**（ソース管理） | **← 今日メインで使うのはここ** |
| 🐞 虫 | Run and Debug | 実行 |
| ⊞ 四角4つ | Extensions（拡張機能） | 拡張機能 |

> ⑂ のアイコンに**青い丸の数字**が付いたら、「変更されたファイルの数」を表しています。

---

## STEP 1：Issueを立てる（1分）

**ここはブラウザで行います。CLI版と全く同じです。**

1. https://github.com/guousuides/git-lec/issues を開く
2. 緑の **New issue** を押す
3. **`🎉 はじめてのPR（自己紹介ページを作る）`** の **Get started** を押す
4. タイトルの `<あなたのGitHub ID>` を自分のIDに書き換える
5. 緑の **Create** を押す
6. **画面上部の番号（`#12` など）をメモ**

> 🌱 この時点で、今日の草はもう1つ生えています。

---

## STEP 2：リポジトリをPCにコピーする（clone）（2分）

### 2-1. Cloneを始める

1. VS Codeを起動する（何も開いていない状態でOK）
2. **command + Shift + P**（Windowsは **Ctrl + Shift + P**）を押す
   → 画面上部に入力欄が出ます（**コマンドパレット**と言います）
3. `git clone` と入力
4. **Git: Clone**（Git: 複製）を選んでEnter

> 💡 **コマンドパレット（command/Ctrl + Shift + P）は、VS Codeで迷った時の万能入口です。**
> やりたいことを日本語/英語で打つと、該当機能が出てきます。覚えておくと一生役立ちます。

### 2-2. URLを入力

入力欄に以下を貼り付けてEnter：

```
https://github.com/guousuides/git-lec.git
```

### 2-3. 保存場所を選ぶ

フォルダ選択ダイアログが開きます。

**「デスクトップ」を選んで、`Select as Repository Destination`（リポジトリの宛先として選択）を押してください。**

> 💡 **場所を必ず覚えておいてください。** これが [00](00_terminal_basics.md) で言う「カレントディレクトリ」にあたります。
> 迷子になりやすいので、**デスクトップを推奨**します。

### 2-4. 開く

右下に **Would you like to open the cloned repository?**（複製したリポジトリを開きますか？）
と出るので、**Open**（開く）を押します。

**期待する状態**

- 左のExplorerに `docs` `members` `slides` などのフォルダが並んでいる
- ウィンドウのタイトルバーに `git-lec` と表示されている

### 2-5. 🔴 「信頼しますか」ダイアログ

**Do you trust the authors of the files in this folder?**（このフォルダー内のファイルの作成者を信頼しますか？）

→ **Yes, I trust the authors**（はい、作成者を信頼します）を押してください。

**これを押さないと編集ができません。**

### よくあるトラブル

| 症状 | 対処 |
|---|---|
| 認証を求められる | ブラウザが開くので、GitHubにログインして許可 |
| `Repository not found` | Collaborator招待を承認していない → https://github.com/notifications |
| 何も起きない | 左下の歯車 → **Accounts**（アカウント）でGitHubにサインインしているか確認 |

---

## STEP 3：ブランチを作る（1分）

> **ブランチ**＝ `main` を壊さないための、自分専用の作業ライン。

### 3-1. 現在のブランチを確認

**VS Codeの左下（ステータスバー）に、⑂ マークと `main` という文字**が出ています。

### 3-2. ブランチを作る

1. その **`main` の文字をクリック**
2. 上部にメニューが出るので、**`+ Create new branch...`**（+ 新しいブランチの作成...）を選ぶ
3. ブランチ名を入力してEnter：

```
feat/taro-yamada-profile
```

> ⚠️ **`taro-yamada` を自分のGitHub IDに書き換えてください。**
> ルール → [CONTRIBUTING.md](../CONTRIBUTING.md)

### 3-3. 確認

**左下の表示が `feat/taro-yamada-profile` に変わっていればOKです。**

> 💡 ここが `main` のままだと、**本線に直接コミットしてしまいます。** 必ず確認してください。

---

## STEP 4：自己紹介ファイルを作る（3分）

### 4-1. テンプレートを見る

1. 左のExplorerで **`members`** フォルダをクリックして開く
2. **`_TEMPLATE.md`** をクリックして中身を見る
3. **`cypher-cto.md`** も見てみる（記入済みサンプル）

### 4-2. 自分のファイルを作る

**方法A：テンプレートをコピーする（推奨）**

1. `_TEMPLATE.md` を右クリック → **Copy**（コピー）
2. `members` フォルダを右クリック → **Paste**（貼り付け）
   → `_TEMPLATE copy.md` ができます
3. それを右クリック → **Rename**（名前の変更）
4. `taro-yamada.md` に変更してEnter

**方法B：新規作成する**

1. `members` フォルダにマウスを乗せる
2. 右側に出る **📄+**（New File / 新しいファイル）アイコンをクリック
3. `taro-yamada.md` と入力してEnter
4. `_TEMPLATE.md` の中身をコピーして貼り付け

> ⚠️ **ファイル名は「あなたのGitHub ID」+ `.md`** にしてください。
> 大文字小文字も、GitHubのIDと合わせてください。

### 4-3. 編集する

`<>` で囲まれた部分を、自分の内容に書き換えてください。

**全部埋めなくてOKです。書きたくないことは書かなくて構いません。**

> ⚠️ **個人情報（本名・住所・電話番号）は書かないでください。** このリポジトリはPublicです。

### 4-4. 🔴 保存する

**command + S**（Windowsは **Ctrl + S**）

> ⚠️ **保存していないと、次のステップで何も出てきません。**
> タブのファイル名の横に **●（白い丸）** が出ていたら未保存です。消えたら保存済み。

### 4-5. プレビューで見てみる（任意）

**command + Shift + V**（Windowsは **Ctrl + Shift + V**）で、Markdownの完成形が見られます。

---

## STEP 5：変更を記録する（add → commit）（2分）

**ここからが Source Control パネルの出番です。**

### 5-1. Source Controlを開く

**左端の ⑂（枝分かれ）アイコン**をクリック。

**期待する画面**

```
SOURCE CONTROL
┌────────────────────────────────┐
│ Message (⌘Enter to commit...)  │  ← コミットメッセージ入力欄
└────────────────────────────────┘
   [ ✓ Commit ]

▼ Changes                      1
    taro-yamada.md    members    U
                                 ↑
                        U = Untracked（新規ファイル）
```

> **`U`** = Untracked（Gitがまだ知らない新規ファイル）
> **`M`** = Modified（変更されたファイル）
>
> 今、あなたの変更は **① 作業場** にあります。

### 5-2. 🔴【最重要】何を変えたか確認する

**ファイル名をクリックしてください。**

差分（diff）が表示されます。

```
┌─────────────────┬─────────────────┐
│  変更前          │  変更後          │
│                 │  + # taro-yamada │
│                 │  +               │
│                 │  + ## ひとこと    │
└─────────────────┴─────────────────┘
```

- **緑の背景 / `+`** = 追加された行
- **赤の背景 / `-`** = 削除された行

**確認すること：**
- ✅ 自分のファイルだけが変更されている
- ❌ 身に覚えのないファイルが混ざっている → 手を挙げてください

> 💡 **この「コミット前にdiffを見る」習慣が、今日いちばん持って帰ってほしいものです。**
> GUIだとクリック1つで見られるので、CLIより簡単です。**必ず見てください。**
> → [06_safety.md](06_safety.md) / [07_extra_ai_git.md](07_extra_ai_git.md)

### 5-3. ステージに乗せる（① → ②）

**ファイル名の右にマウスを乗せると出てくる `+`（プラス）をクリック。**

**期待する状態**：ファイルが **Staged Changes**（ステージされている変更）というセクションに移動します。

```
▼ Staged Changes               1
    taro-yamada.md    members    A
                                 ↑
                        A = Added（追加済み）
```

**これが `git add` です。** 変更が **② ステージ** に移りました。

> 💡 **間違えて `+` を押した場合**：**`−`（マイナス）**を押せば戻せます。ファイルの中身は消えません。

### 5-4. コミットメッセージを書く

**上部の入力欄**に入力します：

```
feat: taro-yamada の自己紹介を追加
```

> ⚠️ ルール（[CONTRIBUTING.md](../CONTRIBUTING.md)）：
> **`種類: 内容`** の形式。コロンの後に**半角スペース**が必要です。

### 5-5. コミットする（② → ③）

**青い `✓ Commit`（コミット）ボタン**を押す。

**期待する状態**

- Source Control の一覧が**空**になる
- 左端の ⑂ アイコンから青い数字バッジが消える

> これが `git status` で言う **`working tree clean`** の状態です。

### よくあるトラブル

**「ステージされている変更がありません。すべての変更をステージしてコミットしますか？」**

→ `+` を押し忘れています。**Yes** を押せばまとめてやってくれますが、
**今日は No を押して、5-3 に戻って `+` を押してください。**（何が起きているか分かる方が大事です）

**`Make sure you configure your 'user.name' and 'user.email' in git.`**

→ 事前課題の `git config` が終わっていません。

**GUIだけで直す方法**：
1. **command/Ctrl + Shift + P** → `terminal` と入力 → **Terminal: Create New Terminal** を選ぶ
2. VS Code下部にターミナルが開くので、以下を1行ずつ実行：

```bash
git config --global user.name "あなたのGitHub ID"
git config --global user.email "GitHubに登録したメールアドレス"
```

3. もう一度 Commit ボタンを押す

> ⚠️ **メールアドレスがGitHub登録済みのものと一致していないと、草が生えません。** → [02_kusa.md](02_kusa.md)

---

## STEP 6：GitHubに送る（push）（1分）

**`✓ Commit` ボタンがあった場所が、`Publish Branch`（ブランチの発行）に変わっています。**

**それをクリック。**

> 💡 2回目以降は **`Sync Changes`**（変更の同期）という表示になります。同じものです。

**期待する状態**

- 右下に **Successfully published branch**（ブランチを発行しました）のような通知が出る
- ボタンが `Sync Changes` に変わる

**これが `git push` です。** 変更が **④ GitHub** に届きました。

### 確認

ブラウザで https://github.com/guousuides/git-lec を開いてください。
上部に黄色い帯で **`feat/taro-yamada-profile had recent pushes`** と出ていれば成功です。

### よくあるトラブル

| 症状 | 対処 |
|---|---|
| 認証画面が出る | ブラウザでGitHubにログイン → **Authorize**（承認） |
| **403 / Permission denied** | Collaborator招待が未承認 → https://github.com/notifications で **Accept invitation** |
| `rejected` と出る | Source Control の **…** → **Pull** を実行してから、もう一度 |

---

## STEP 7：Pull Requestを出す（2分）

**ここはブラウザで行います。**（VS Codeの拡張機能でもできますが、今日はブラウザが確実です）

1. https://github.com/guousuides/git-lec を開く
2. 黄色い帯の右の緑ボタン **Compare & pull request** を押す

> 帯が無い場合：**Pull requests** タブ → **New pull request** →
> `compare:` から自分のブランチを選択 → **Create pull request**

3. **タイトル**を確認：`feat: taro-yamada の自己紹介を追加`
4. **本文**にテンプレートが入っています。**項目を消さずに埋められるところを埋める**
   - `close #12` の番号を、STEP 1 でメモしたIssue番号に変更
   - 分からない項目は「分かりません」でOK
5. 緑の **Create pull request** を押す

### 🔴 作成後、必ず確認する2箇所

**① Files changed タブ**

- ✅ 自分のファイル1つだけが緑（追加）で表示されている
- ❌ 他のファイルが混ざっている → 手を挙げてください

**② Commits タブ**

| 見た目 | 判定 |
|---|---|
| **あなたのアイコン + IDがリンク** | ✅ 草が生えます |
| **灰色の人型シルエット + IDがただの文字** | ❌ メール不一致 → [02_kusa.md](02_kusa.md) |

---

## STEP 8：レビューとmerge（1分）

1. 講師がレビューして **Approve**（承認）します
2. 緑の **Merge pull request** ボタンを押す（講師が押す場合もあります）
3. **Confirm merge** を押す

**期待する状態**：PRの表示が紫色の **Merged** に変わります。

## 🎉 完了です

---

## STEP 9：草を確認する（1分）

1. https://github.com/あなたのGitHub-ID を開く
2. 下にスクロールして緑のマス目を探す
3. **今日の日付が緑になっていれば成功** 🌱

**生えていない場合はまず5分待ってリロード。** それでもダメなら [02_kusa.md](02_kusa.md) のチェックリストへ。

---

## STEP 10：後片付け（余裕があれば）

1. **左下のブランチ名をクリック** → `main` を選ぶ
2. Source Control パネルの **…**（三点メニュー）→ **Pull**（プル）

**期待する状態**：`members` フォルダに、**他の受講者のファイルも増えている**はずです。

これが「チームで開発している」ということです。

---

## GUI版まとめ：4領域とボタンの対応

```
① Working Tree ──[ + ]──> ② Staged ──[ ✓ Commit ]──> ③ Local ──[ Sync ]──> ④ GitHub
   ファイルを編集         ファイル横の         青いボタン        Publish/Sync
   して保存               プラス                                Changes
```

**押しているボタンが違うだけで、CLI版と全く同じことをしています。**

| もっと知りたい | 資料 |
|---|---|
| 実際のコマンドを知る | [03_basic_commands.md](03_basic_commands.md) |
| コンフリクト解消（**GUIが圧倒的に楽です**） | [05_extra_conflict_revert.md](05_extra_conflict_revert.md) |
| 秘密情報を守る | [06_safety.md](06_safety.md) |
| AIエージェントに任せる | [07_extra_ai_git.md](07_extra_ai_git.md) |

> 💡 **GUIで慣れてからCLIに移行するのは、全く恥ずかしいことではありません。**
> 実務のエンジニアも、コンフリクト解消やdiffの確認はGUIを使う人が多いです。
> **道具は使い分けるものです。**

---

**← [目次（README）に戻る](../README.md)**
