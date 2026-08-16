# git-lec — GitHub入門講座（初級編・30分）

学生AI/データサイエンスコミュニティ **Cypher** のGitHub入門ハンズオン用リポジトリです。

> **リポジトリ**（repository / 略してレポ）＝ プロジェクトの保存箱。
> ファイルと、その変更履歴がまとめて入っている場所のことです。

---

## この30分のゴール

**受講後、あなたのPull Requestがmergeされ、GitHubのプロフィールに草が1つ生えている。**

> **草**＝ GitHubのプロフィールページに出る、緑色のマス目。活動した日に色がつきます。
> **Pull Request**（プルリクエスト / 略してPR）＝「この変更を取り込んでください」というお願いの投稿。

具体的には、この講座であなたがやることは1つだけです。

**`members/` フォルダに `あなたのGitHub ID.md` という自己紹介ファイルを新しく作り、PRを出してmergeしてもらう。**

たったこれだけです。ただし、その過程でターミナルの使い方・Gitの仕組み・GitHub Flowという実務そのままの流れを一通り通ります。

---

## 最初に、いちばん大事なこと

**壊れません。**

この講座であなたが打つコマンドで、PCが壊れることも、このリポジトリが壊れることもありません。
Gitは「履歴を記録する道具」なので、むしろ**間違えた状態に戻せるようにするための道具**です。

- エラーが出る → **正常です。** 全員出ます。プロの開発者も毎日出しています。
- 何を打てばいいか分からなくなった → **手を挙げてください。** それが最速です。
- 画面が真っ黒で怖い → **みんな最初はそうでした。**

エラーメッセージは「あなたを責める文章」ではなく「次に何をすればいいかのヒント」です。
今日は**エラーを1回も出さないこと**が目標ではありません。**エラーを出しても前に進めること**が目標です。

---

## 講座の流れ（30分）

| 時間 | 内容 | 資料 |
|---|---|---|
| 0–3分 | ゴール確認・事前課題セルフチェック | このREADME |
| 3–7分 | ターミナルってなに？ `pwd` / `cd` / `ls` | [docs/00_terminal_basics.md](docs/00_terminal_basics.md) |
| 7–12分 | GitとGitHubの違い・4領域モデル | [docs/01_git_vs_github.md](docs/01_git_vs_github.md) |
| 12–24分 | **ハンズオン本編**：clone → branch → 編集 → commit → push → PR → merge | [docs/04_branch_pr.md](docs/04_branch_pr.md) |
| 24–27分 | 草を確認する・草が生えない罠 | [docs/02_kusa.md](docs/02_kusa.md) |
| 27–30分 | 番外編の予告と持ち帰り課題 | [docs/05](docs/05_extra_conflict_revert.md) / [docs/07](docs/07_extra_ai_git.md) |

**ターミナルが苦手な方へ**：全く同じことをVS Codeのマウス操作だけで行う手順書があります。
→ [docs/08_gui_version.md](docs/08_gui_version.md)

当日はどちらで進めても構いません。進行役が主線をアナウンスしますが、途中で乗り換えても大丈夫です。

---

## 事前課題（講座前日までに終わらせてください）

**所要時間の目安：30〜40分。** ここが終わっていないと当日ハンズオンに入れません。
詰まったらCypherのDiscordで聞いてください。当日朝に聞いても間に合います。

### 0. 運営からの招待メールを承認する ← 最優先

運営があなたのGitHub IDをこのリポジトリの **Collaborator**（共同編集者）に招待します。

> **Collaborator**＝ このリポジトリに直接書き込む権限をもらった人。

1. GitHubに登録したメールアドレスに `[GitHub] @guousuides has invited you to collaborate` という件名のメールが届きます
2. メール内の **View invitation** を押す
3. 開いたページで **Accept invitation** を押す

メールが見つからない場合は https://github.com/notifications からも承認できます。

> ⚠️ **これを承認しないと、当日 `git push` が必ず失敗します。** 最優先で終わらせてください。
> 招待が届いていない人は、自分のGitHub IDを運営・TAに伝えてください。

### 1. GitHubアカウントを作る

https://github.com/signup

- **GitHub ID（ユーザー名）は後で使うのでメモしておいてください。** 例：`taro-yamada`
- 大学のメールでも個人のメールでも構いません（後述の「草の罠」に関わるので、**登録したメールアドレスもメモ**してください）

### 2. Gitをインストールする

自分のPCで「履歴を記録する道具」を使えるようにします。

**Windows の方**

https://git-scm.com/download/win からインストーラをダウンロードして実行。
選択肢がたくさん出ますが、**すべてデフォルトのまま「Next」を押し続けて問題ありません。**
（この過程で **Git Bash** という黒い画面のアプリが一緒に入ります。当日はこれを使います）

**Mac の方**

「ターミナル」アプリを開いて、以下を1行だけ打ってEnter：

```bash
git --version
```

- バージョンが表示されたら → **完了です。何もしなくていいです。**
- 「開発者ツールをインストールしますか」というダイアログが出たら → **インストール**を押して待つ（5〜10分かかります）

### 3. 自分の名前とメールをGitに教える（git config）

Gitに「このPCで作業しているのは誰か」を登録します。**これをやらないと草が生えません。**

ターミナル（Windowsは Git Bash）を開いて、以下を**1行ずつ**打ってEnter：

```bash
git config --global user.name "あなたのGitHub ID"
```

```bash
git config --global user.email "GitHubに登録したメールアドレス"
```

> ⚠️ **メールアドレスはGitHubに登録したものと完全に一致させてください。**
> ここが違うと、コミットはできるのに草が生えません。当日いちばん多いトラブルです。
> 詳しい理由は [docs/02_kusa.md](docs/02_kusa.md) にあります。

**確認**：以下を打って、さっき入力した内容が返ってくればOK。

```bash
git config --global --list
```

期待する出力（一部）：

```
user.name=taro-yamada
user.email=taro@example.com
```

### 4. GitHubにログインできる状態にする（認証設定）

自分のPCからGitHubに書き込むための「鍵」を用意します。**いちばん簡単な方法**を案内します。

**GitHub CLI を使う方法（推奨・全OS共通）**

1. https://cli.github.com/ からインストール
2. ターミナルで以下を実行：

```bash
gh auth login
```

3. 聞かれたら、矢印キーとEnterで以下を選ぶ：
   - `GitHub.com`
   - `HTTPS`
   - `Yes`（Gitの認証にも使う）
   - `Login with a web browser`
4. 画面に8桁のコード（例：`ABCD-1234`）が出る → コピーしてEnter → ブラウザが開く → コードを貼り付けて認証

**確認**：以下を打って、自分のIDが出ればOK。

```bash
gh auth status
```

期待する出力（一部）：

```
github.com
  ✓ Logged in to github.com account taro-yamada
```

> パスワード入力を求められた場合、**GitHubのログインパスワードは使えません**（2021年に廃止されました）。
> 上の `gh auth login` をやり直してください。

### 5. VS Codeをインストールする（GUI版で進めたい人・推奨）

https://code.visualstudio.com/

ターミナルが不安な方は、VS Codeを入れておくと当日マウス操作だけで進められます。
入れておいて損はないので、**全員インストールを推奨します。**

---

## 事前課題セルフチェック

当日開始前に、以下がすべて ✅ になっているか確認してください。
**ターミナルにコマンドを打って、期待する出力が返ってくるかで判定します。**

| # | 確認すること | 打つコマンド | 期待する出力 |
|---|---|---|---|
| 1 | Collaborator招待を承認した | （コマンドなし） | https://github.com/guousuides/git-lec を開いて、右上に **Settings** タブが見える |
| 2 | Gitが入っている | `git --version` | `git version 2.xx.x` のような行 |
| 3 | 名前を設定した | `git config --global user.name` | 自分のGitHub ID |
| 4 | メールを設定した | `git config --global user.email` | GitHubに登録したメールアドレス |
| 5 | GitHubに認証できている | `gh auth status` | `✓ Logged in to github.com account ...` |
| 6 | VS Codeが入っている（推奨） | （コマンドなし） | アプリが起動する |

**1つでも ✅ にならなかった人**：当日の開始10分前に来てください。もしくはDiscordで質問してください。
「できませんでした」と当日言ってもらえれば大丈夫です。**隠して当日詰まるのがいちばん困ります。**

---

## ドキュメント一覧

### 本編（この順に読む）

| 資料 | 内容 |
|---|---|
| [00_terminal_basics.md](docs/00_terminal_basics.md) | ターミナルとは何か、`pwd` / `cd` / `ls`、パスの読み方 |
| [01_git_vs_github.md](docs/01_git_vs_github.md) | GitとGitHubの違い、4領域モデル（作業場・ステージ・ローカル・リモート） |
| [02_kusa.md](docs/02_kusa.md) | 草の文化。カウントされる条件・されない条件・生えない時の直し方 |
| [03_basic_commands.md](docs/03_basic_commands.md) | `clone` `status` `add` `commit` `push` `pull` `log` `diff` の逆引き辞典 |
| [04_branch_pr.md](docs/04_branch_pr.md) | **ハンズオン本編。** GitHub Flow（issue → branch → PR → review → merge） |
| [06_safety.md](docs/06_safety.md) | `.gitignore`、APIキーや `.env` を上げない、上げてしまった時の対処 |
| [08_gui_version.md](docs/08_gui_version.md) | 上記すべてのVS Code GUI版（マウス操作のみ） |

### 番外編（**本編を手で1周してから**読んでください）

| 資料 | 内容 |
|---|---|
| [05_extra_conflict_revert.md](docs/05_extra_conflict_revert.md) | 番外編1。コンフリクト解消、`revert` と `reset` の違い |
| [07_extra_ai_git.md](docs/07_extra_ai_git.md) | 番外編2。AIエージェントによるGit自動操作と、人間側の責任 |

### その他

| 資料 | 内容 |
|---|---|
| [CONTRIBUTING.md](CONTRIBUTING.md) | コミットメッセージとブランチ名のルール |
| [facilitator_guide.md](facilitator_guide.md) | ファシリテーター用ガイド（受講者は読まなくてOK） |
| [conflict-playground/](conflict-playground/) | 壊してよい練習場。番外編1で使います |

---

## 講座が終わった後に

1. **草が生えたか確認する** → https://github.com/あなたのID のプロフィールページ
2. **番外編を読む** → [コンフリクト](docs/05_extra_conflict_revert.md) と [AIエージェント](docs/07_extra_ai_git.md)
3. **もう1回やってみる** → `members/あなたのID.md` を編集して2つ目のPRを出す。1回目より圧倒的に速いはずです
4. **自分のプロジェクトで使う** → 今日やったことは、そのまま実務の流れです

---

## 質問・詰まったとき

- 当日：**手を挙げる**（いちばん速い）
- 当日以降：[Issueを立てる](https://github.com/guousuides/git-lec/issues/new/choose) → `❓ 質問・困っています` を選択
- Cypher Discord の `#git-lec` チャンネル

Issueを立てるのも立派なGitHubの練習です。遠慮なくどうぞ。
