# 03. 基本コマンド逆引き辞典

**所要：読み物（ハンズオン中は参照用）** ｜ 前 → [02. 草の話](02_kusa.md) ｜ 次 → [04. ブランチとPR（ハンズオン本編）](04_branch_pr.md)

このページのゴール：**手が止まった時に、ここを開けば次の1行が見つかる状態になる。**

> ⚠️ **このページを暗記する必要はありません。**
> 実務でも、みんな毎回ググっています。**引ければ十分**です。
> ハンズオン中は [04](04_branch_pr.md) の手順に従い、詰まった時だけここに戻ってきてください。

---

## 全部、この図の話です

```
① Working Tree ──[add]──> ② Staging ──[commit]──> ③ Local ──[push]──> ④ GitHub
   (作業場)                  (ステージ)              (手元の箱)          (ネット)
      ^                                                                    |
      └──────────────────────[pull]───────────────────────────────────────┘
```

（詳しくは [01. 4領域モデル](01_git_vs_github.md)）

---

## 目次

| やりたいこと | コマンド |
|---|---|
| GitHubからPCにコピーする | [`git clone`](#git-clone) |
| **今どうなっているか知りたい** | [`git status`](#git-status) |
| **何を変えたか見たい** | [`git diff`](#git-diff) |
| 記録する候補に入れる | [`git add`](#git-add) |
| 記録を確定する | [`git commit`](#git-commit) |
| GitHubに送る | [`git push`](#git-push) |
| GitHubから取り込む | [`git pull`](#git-pull) |
| 履歴を見る | [`git log`](#git-log) |
| ブランチを作る/切り替える | [`git switch`](#git-switch) |

---

## `git clone`

**GitHubにあるリポジトリを、自分のPCにまるごとコピーする。**

4領域で言うと：**④ → ①③ に一気にコピー**（最初の1回だけ実行）

```bash
git clone https://github.com/guousuides/git-lec.git
```

**期待する出力**
```
Cloning into 'git-lec'...
remote: Enumerating objects: 42, done.
remote: Counting objects: 100% (42/42), done.
remote: Compressing objects: 100% (30/30), done.
Receiving objects: 100% (42/42), 15.23 KiB | 3.81 MiB/s, done.
Resolving deltas: 100% (5/5), done.
```

**実行後どうなるか**：今いる場所に `git-lec` というフォルダができます。

```bash
ls
```
→ `git-lec` が見えるはず

```bash
cd git-lec
pwd
```
→ 末尾が `/git-lec` になっていればOK

### よくあるエラー

| エラー | 意味 | 対処 |
|---|---|---|
| `destination path 'git-lec' already exists` | すでにcloneしてある | `cd git-lec` で入るだけでOK。cloneし直す必要はありません |
| `Repository not found` | URLが違う / 権限がない | URLを確認。Collaborator招待を承認したか確認（[README](../README.md)） |

> ⚠️ **cloneは1回だけです。** 2回目以降は `cd git-lec` で入るだけ。
> 「よく分からないからもう1回clone」をすると、`git-lec 2` のようなフォルダが増えて余計に混乱します。

---

## `git status`

**今、4領域のどこに何があるかを表示する。今日いちばん使うコマンド。**

```bash
git status
```

**迷ったらこれ。** 何回打っても何も壊れません。1分に1回打っていいくらいです。

### 出力の読み方

| 出力に出る言葉 | 意味 | どの段階 |
|---|---|---|
| `Untracked files:` （赤） | Gitがまだ知らないファイル | ① 作業場 |
| `Changes not staged for commit:` （赤） | 変更したが add していない | ① 作業場 |
| `Changes to be committed:` （緑） | add 済み。次のcommitに入る | ② ステージ |
| `nothing to commit, working tree clean` | 未記録の変更なし | ③ commit 済み |
| `Your branch is ahead of 'origin/main' by 1 commit` | commit したが push していない | ③ ローカルのみ |

**赤 = まだステージに入っていない ｜ 緑 = ステージに入っている**

これだけ覚えておけば十分です。

### 便利な機能

`git status` は、**次に打つべきコマンドを教えてくれます。**

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
              ^^^^^^^^^^^^^^^^^^ ← これが次に打つコマンド
```

括弧の中を読んでください。**Gitは意外と親切です。**

---

## `git diff`

**中身が何から何に変わったかを表示する。**

```bash
git diff
```

**期待する出力**（例）
```diff
diff --git a/members/taro-yamada.md b/members/taro-yamada.md
--- a/members/taro-yamada.md
+++ b/members/taro-yamada.md
@@ -1,3 +1,4 @@
 # 山田太郎
 
 ## 興味分野
+機械学習、特に自然言語処理
```

### 読み方

| 記号 | 意味 |
|---|---|
| `+` の行（緑） | 追加された行 |
| `-` の行（赤） | 削除された行 |
| 記号なし | 変わっていない行（文脈表示） |

### 使い分け

| コマンド | 何を見せる |
|---|---|
| `git diff` | ① 作業場 の変更（**まだ add していない**もの） |
| `git diff --staged` | ② ステージ の変更（**add 済み**のもの） |

> ⚠️ **`git add` した後に `git diff` を打つと、何も出ません。**
> 「変更が消えた！」と焦りますが、**ステージに移動しただけ**です。
> `git diff --staged` で見えます。

### 画面が固まったら

diffが長いと、下に `:` だけが表示されて動かなくなります。**壊れていません。**

| キー | 動作 |
|---|---|
| **`q`** | **終了する（これを押せばOK）** |
| ↓ / Enter | 1行進む |
| スペース | 1画面進む |

**`q` を押す。** これだけ覚えてください。

---

## `git add`

**「次の記録に含める」とファイルを選ぶ。① → ②**

```bash
git add members/taro-yamada.md
```

**期待する出力**

**何も出ません。** 成功です。

**確認**：
```bash
git status
```
→ ファイル名が **緑色** の `Changes to be committed:` の下に移動していればOK

### 書き方のバリエーション

| コマンド | 意味 | 使いどころ |
|---|---|---|
| `git add ファイル名` | そのファイルだけ | **今日はこれを使います（推奨）** |
| `git add .` | 今いる場所以下の変更を全部 | 便利だが、余計なものが混ざる危険あり |
| `git add -A` | リポジトリ全体の変更を全部 | 同上 |

> ⚠️ **`git add .` は便利ですが、危険でもあります。**
> `.env`（パスワードが入ったファイル）や、巨大なデータファイルまで巻き込むことがあります。
> 使う時は、**必ず `git status` で何が入ったか確認してから commit してください。**
> → [06_safety.md](06_safety.md)

### 間違えて add した時の取り消し

```bash
git restore --staged members/taro-yamada.md
```

**ファイルの中身は消えません。** ② から ① に戻すだけです。安心してください。

> `git status` の出力にも `(use "git restore --staged <file>..." to unstage)` と書いてあります。

---

## `git commit`

**記録を確定させる。② → ③**

```bash
git commit -m "feat: taro-yamada の自己紹介を追加"
```

- `-m` は **m**essage の略。この後ろに、何をしたかを書きます
- メッセージは**ダブルクォート `"` で囲みます**
- 書き方のルール → [CONTRIBUTING.md](../CONTRIBUTING.md)

**期待する出力**
```
[feat/taro-yamada-profile 3a4b5c6] feat: taro-yamada の自己紹介を追加
 1 file changed, 12 insertions(+)
 create mode 100644 members/taro-yamada.md
```

読み方：
- `feat/taro-yamada-profile` — 今いるブランチ名
- `3a4b5c6` — このコミットのID（**コミットハッシュ**。世界で唯一の番号）
- `1 file changed, 12 insertions(+)` — 1ファイルに12行追加した

### よくあるエラー

**`nothing to commit, working tree clean`**

→ `git add` を忘れています。add してから commit してください。

**`Please tell me who you are`**

```
*** Please tell me who you are.
Run
  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"
```

→ 事前課題の `git config` が終わっていません。**表示された通りのコマンドを実行**してください。
→ [README の事前課題3](../README.md#3-自分の名前とメールをgitに教えるgit-config)

**エディタが開いて操作不能になった**

`-m "メッセージ"` を書き忘れると、Gitがエディタを開いてメッセージを書かせようとします。
Vim という古典的なエディタが開くことが多く、初見では脱出できません。

**脱出方法**：
1. **`Esc` キー**を押す
2. `:q!` と打つ（コロン、q、ビックリマーク）
3. **Enter**

これでコミットがキャンセルされて戻れます。`-m` を付けて打ち直してください。

> これは今日いちばん焦るトラブルですが、**壊れていません。** 落ち着いて `Esc` → `:q!` → Enter。

---

## `git push`

**手元の記録をGitHubに送る。③ → ④**

```bash
git push -u origin feat/taro-yamada-profile
```

- `origin` — GitHub上のリポジトリの呼び名（cloneすると自動で付きます）
- `feat/...` — 送るブランチ名
- `-u` — 「次からは `git push` だけでいいよ」と紐付ける設定（初回だけ必要）

**2回目以降は、これだけでOK**：
```bash
git push
```

**期待する出力**
```
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Writing objects: 100% (4/4), 512 bytes | 512.00 KiB/s, done.
To https://github.com/guousuides/git-lec.git
 * [new branch]      feat/taro-yamada-profile -> feat/taro-yamada-profile
branch 'feat/taro-yamada-profile' set up to track 'origin/feat/taro-yamada-profile'.

remote: Create a pull request for 'feat/taro-yamada-profile' on GitHub by visiting:
remote:      https://github.com/guousuides/git-lec/pull/new/feat/taro-yamada-profile
```

> 💡 **最後に出るURLをクリックすると、PR作成画面に直行できます。** 覚えておくと便利です。

### よくあるエラー

**`Authentication failed` / `could not read Username`**

→ GitHubにログインできていません。

```bash
gh auth login
```

を実行し直してください（[README の事前課題4](../README.md#4-githubにログインできる状態にする認証設定)）。

> ⚠️ **GitHubのログインパスワードは使えません。** 2021年に廃止されています。

**`Permission denied` / `403`**

→ Collaborator招待を承認していません。https://github.com/notifications を確認してください。

**`src refspec ... does not match any`**

→ ブランチ名の打ち間違いです。`git branch` で正しい名前を確認してください。

**`Updates were rejected`**

→ GitHub側に、自分が持っていない変更があります。

```bash
git pull
```

してから、もう一度 push してください。

> ⚠️ ここで `git push --force` を使ってはいけません。**他人の作業が消えます。**
> → [05_extra_conflict_revert.md](05_extra_conflict_revert.md)

---

## `git pull`

**GitHub上の最新を、手元に取り込む。④ → ①**

```bash
git pull
```

**期待する出力**（更新がある場合）
```
Updating 3a4b5c6..7d8e9f0
Fast-forward
 members/hanako-s.md | 10 ++++++++++
 1 file changed, 10 insertions(+)
 create mode 100644 members/hanako-s.md
```

**期待する出力**（更新がない場合）
```
Already up to date.
```

### いつ使うか

- **作業を始める前**（他の人の変更を取り込んでおく）
- push が `rejected` された時
- 自分のPRがmergeされた後、`main` を最新にする時

> 💡 **作業開始前に `git pull`** を習慣にすると、コンフリクトが激減します。

---

## `git log`

**これまでの記録（履歴）を見る。③ の中身**

```bash
git log
```

**期待する出力**
```
commit 3a4b5c6d7e8f9a0b1c2d3e4f5a6b7c8d9e0f1a2b (HEAD -> feat/taro-yamada-profile)
Author: taro-yamada <taro@example.com>
Date:   Thu Aug 14 14:23:11 2026 +0900

    feat: taro-yamada の自己紹介を追加

commit 1a2b3c4d5e6f7a8b9c0d1e2f3a4b5c6d7e8f9a0b (origin/main, main)
Author: cypher-cto <cto@example.com>
Date:   Wed Aug 13 09:15:42 2026 +0900

    docs: ハンズオン資料を追加
```

> 💡 **`Author:` のメールアドレスを見てください。** ここが GitHub 登録済みのアドレスと違うと、草が生えません。
> → [02_kusa.md](02_kusa.md)

**画面が固まったら `q` を押す。** （`git diff` と同じです）

### 見やすくする

```bash
git log --oneline
```

**期待する出力**
```
3a4b5c6 (HEAD -> feat/taro-yamada-profile) feat: taro-yamada の自己紹介を追加
1a2b3c4 (origin/main, main) docs: ハンズオン資料を追加
```

**1コミット1行になって圧倒的に見やすいです。** こちらを普段使いにしてください。

```bash
git log --oneline --graph --all
```

ブランチの分岐が線で見えます。ちょっとカッコいいので試してみてください。

---

## `git switch`

**ブランチを作る / 切り替える。**

### 新しいブランチを作って、そこに移動する

```bash
git switch -c feat/taro-yamada-profile
```

`-c` は **c**reate（作る）の意味です。

**期待する出力**
```
Switched to a new branch 'feat/taro-yamada-profile'
```

### 既存のブランチに移動する

```bash
git switch main
```

**期待する出力**
```
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

### 今どのブランチにいるか確認する

```bash
git branch
```

**期待する出力**
```
* feat/taro-yamada-profile
  main
```

`*` が付いているのが**今いるブランチ**です。

> 💡 `git status` の1行目にもブランチ名が出ます。
> 実は `git status` だけで、場所もブランチも変更状況も全部わかります。**だから最強なんです。**

### `git checkout` との違い

古い資料では `git checkout -b` と書かれていることがあります。**やることは同じ**です。

`git checkout` は機能が多すぎて初心者を混乱させたため、
2019年に**ブランチ操作専用の `git switch`** が作られました。**今日は `git switch` を使います。**

---

## 困った時の3つの魔法

| 状況 | 打つコマンド |
|---|---|
| 今どこにいるか分からない | `pwd` |
| 今どういう状態か分からない | `git status` |
| 何を変えたか分からない | `git diff` |

**この3つは何回打っても絶対に壊れません。** 迷ったら打ってください。

---

## このページのまとめ

**暗記しないでください。** 手が止まったらこのページに戻ってくる、それで十分です。

覚えておくと得なのは以下だけ：

- **`git status` を打てば、次に何をすべきか Git が教えてくれる**
- **画面が固まったら `q`**
- **エディタから脱出したかったら `Esc` → `:q!` → Enter**

**次 → [04. ブランチとPR（ハンズオン本編）](04_branch_pr.md)**
