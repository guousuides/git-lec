---
marp: true
theme: default
paginate: true
header: 'Cypher / GitHub入門講座 初級編'
footer: 'github.com/guousuides/git-lec'
style: |
  section {
    background: #0f1117;
    color: #e6e8ee;
    font-family: "Hiragino Sans", "Yu Gothic", "Noto Sans JP", sans-serif;
    padding: 60px 70px;
  }
  section.lead {
    background: linear-gradient(135deg, #0f1117 0%, #1a1f2e 100%);
    text-align: center;
  }
  h1 { color: #4ade80; font-size: 2.0em; border: none; }
  h2 { color: #4ade80; font-size: 1.45em; border-bottom: 2px solid #2a3040; padding-bottom: 0.2em; }
  h3 { color: #93c5fd; font-size: 1.1em; }
  strong { color: #fbbf24; }
  code { background: #1a1f2e; color: #4ade80; padding: 2px 8px; border-radius: 4px; }
  pre { background: #1a1f2e; border-left: 4px solid #4ade80; border-radius: 6px; }
  pre code { background: transparent; color: #e6e8ee; font-size: 0.85em; }
  table { font-size: 0.85em; border-collapse: collapse; }
  th { background: #1a1f2e; color: #4ade80; }
  td, th { border: 1px solid #2a3040; padding: 8px 14px; }
  blockquote { border-left: 4px solid #fbbf24; color: #c9cede; padding-left: 1em; font-size: 0.9em; }
  header, footer { color: #5a6478; font-size: 0.6em; }
  a { color: #93c5fd; }
  .big { font-size: 1.6em; line-height: 1.5; }
  .warn { color: #f87171; }
---

<!-- _class: lead -->
<!-- _paginate: false -->

# GitHub入門講座
## 初級編 — 30分

**今日、あなたのPull Requestがmergeされ、
草が1つ生えます。**

Cypher / CTO

<!--
【0:00】
・まず全員のターミナルが開いているか目視確認
・開いていない人がいたら、この時点で隣の人とペアにする
-->

---

# 今日のゴール

<div class="big">

**PRを出して、mergeされて、
プロフィールに緑のマスが1つ増える。**

</div>

やることは、実は**1つだけ**です。

> `members/<あなたのGitHub ID>.md` という
> 自己紹介ファイルを**新しく作る**

<!--
【0:30】
・ゴールを「体験」ではなく「状態」で言い切る
・「1つだけ」を強調 → 心理的ハードルを下げる
-->

---

<!-- _class: lead -->

# 最初に、いちばん大事なこと

<div class="big">

## 壊れません。

</div>

エラーが出ても、**全部やり直せます。**

<!--
【1:00】ここは絶対に飛ばさない
・「今日打つコマンドでPCは壊れません」
・「最悪、フォルダを消してcloneし直せば完全に元通り」
・「エラーは出ます。全員出ます。私も毎日出しています」
-->

---

## エラーメッセージは、あなたを責めていません

```
fatal: not a git repository
```

これは **「怒られている」のではなく**

**「今この状態だよ」と教えてくれている** だけ。

---

**今日の目標は、エラーを出さないことではありません。**
**エラーが出ても、前に進めることです。**

<!--
【1:30】
・実際にわざとエラーを出して見せると効果的
・「英語だから怖い」を「英語だけど3語しかない」に変える
-->

---

## 事前課題チェック（30秒）

ターミナルに打って、出力を確認してください。

```bash
git config --global user.email
```

**GitHubに登録したメールアドレス**が出ましたか？

- ✅ 出た → OK
- ❌ 何も出ない / 違うアドレス → **今すぐ手を挙げてください**

> ここが違うと、**草が生えません。** 今日いちばん多いトラブルです。

<!--
【2:00】
・ここで手が挙がった人は、その場でconfigを打たせる（30秒で終わる）
・Collaborator招待の未承認者もここで炙り出す
  「github.com/guousuides/git-lec を開いて Settings タブが見える人？」
-->

---

<!-- _class: lead -->

# Part 1
## ターミナル（3分）

<!--
【3:00】
-->

---

## ターミナル ＝ 文字でPCに命令する道具

**マウスでやっていることと、全く同じです。**

| やりたいこと | マウス | ターミナル |
|---|---|---|
| 今どこ？ | 上部のパス表示 | `pwd` |
| 中身を見る | フォルダを開く | `ls` |
| 移動する | ダブルクリック | `cd フォルダ名` |

> 映画のハッカーと同じ見た目ですが、
> やっているのは**「フォルダを開く」レベル**の話です。

<!--
【3:15】
・「怖い」の正体は「何が起きるか分からない」こと
・対応表を見せることで「知っている操作の別表現」に変換する
-->

---

## 全員で3つだけ打ちましょう

```bash
pwd
```
→ **今いる場所**が出ます

```bash
ls
```
→ **中身の一覧**が出ます

```bash
cd ..
```
→ **何も出ません。それが成功です**

<!--
【4:00】ここは必ず全員に打たせる。見せるだけにしない
・「何も出ない＝成功」は必ず口で言う（無言を失敗と誤解する人が多い）
・打てていない人がいないか、会場を見回す
-->

---

## 【最重要】今どこにいるか

<div class="big">

**コマンドは、
「今いる場所」に対して実行される。**

</div>

だから、今日のトラブルの半分はこれです：

> 「言われた通り打ったのにエラーが出る」
> → **場所が違うところで打っている**

---

## 迷ったら `pwd`

これだけ覚えて帰ってください。

```bash
pwd
```

**脱出コマンド**

```bash
cd ~     # ホームに戻る（完全リセット）
cd ..    # 1つ上に戻る
```

<!--
【4:45】
・「迷ったらpwd」は今日3回は言う
・後半のハンズオンで詰まった人には、まずpwdを打たせる
-->

---

<!-- _class: lead -->

# Part 2
## GitとGitHub（5分）

<!--
【5:30】
-->

---

## GitとGitHubは、別物です

|  | **Git** | **GitHub** |
|---|---|---|
| 何か | **道具（ソフト）** | **場所（Webサービス）** |
| どこ | あなたのPCの中 | インターネット上 |
| 何を | 履歴を記録する | 記録を置いて共有する |
| ネット | **不要** | 必要 |

<div class="big">

**Git = カメラ ｜ GitHub = 写真共有サービス**

</div>

<!--
【5:45】
・「Gitはネット不要」は必ず言う
・後の「commitしただけでは反映されない」の伏線
-->

---

## 4領域モデル — 今日の核心

```
 ① Working Tree  ──add──▶  ② Staging  ──commit──▶  ③ Local  ──push──▶  ④ GitHub
    作業場                    ステージ                手元の箱             ネット
    編集中の                  記録に含めると          確定した             公開された
    ファイル                  選んだもの              履歴                 履歴
```

**① ② ③ はあなたのPCの中。④ だけがインターネット。**

> **commitしただけでは、GitHubには何もありません。**
> **pushして、初めて届きます。**

<!--
【6:30】この図が今日いちばん大事。時間をかける
・板書 or 手で指しながら説明する
・「後で出てくるコマンドは全部この図の矢印です」と予告
-->

---

## 荷物の発送でたとえると

| 段階 | 荷物 | Git |
|---|---|---|
| ① 作業場 | 部屋に物が散らかっている | ファイルを編集した |
| ② ステージ | **送る物だけ箱に入れた** | `git add` |
| ③ ローカル | **箱にガムテープを貼った** | `git commit` |
| ④ リモート | **郵便局に持って行った** | `git push` |

> なぜ2段階？ → **送りたい物だけを選ぶため。**
> 部屋にある物を全部送るわけではありません。

<!--
【7:30】
・「なぜaddとcommitが分かれているのか」への回答
・ここが腑に落ちると、以降のコマンドが自然に入る
-->

---

## 迷ったら `git status`

**「今、4領域のどこに何があるか」を教えてくれます。**

```
Untracked files:              ← ① 作業場（赤）
  members/taro-yamada.md

Changes to be committed:      ← ② ステージ（緑）
  new file: members/taro-yamada.md

nothing to commit, clean      ← ③ commit済み
```

<div class="big">

**赤 → 緑 に変わったら `git add` 成功**

</div>

<!--
【8:15】
・statusは「次に打つコマンド」も括弧内で教えてくれることを見せる
・「Gitは意外と親切」
-->

---

## `git diff` — 何を変えたか

```diff
+ ## 興味分野
+ 機械学習、特に自然言語処理
- 古い行
```

| 記号 | 意味 |
|---|---|
| **`+`** | **追加された行** |
| **`-`** | **削除された行** |

<div class="big">

**commitする前に、diffを見る。**

</div>

<!--
【9:00】
・今日いちばん持って帰ってほしい習慣、と明言する
・番外編2（AI）への伏線をここで張る
  「これが後で効いてきます」
・画面が固まったら q！ を先に言っておく
-->

---

## ブランチ ＝ 自分専用の作業ライン

```
main         A ──── B ──────────────── M
                     \                /
自分のブランチ         └── C ── D ────┘
                            （PRを出してmerge）
```

**なぜ必要？**
→ **30人が同時に `main` を編集したら、確実に壊れるから。**

ブランチの中なら、**何をしても `main` は無傷です。**

<!--
【9:30】
-->

---

<!-- _class: lead -->

# Part 3
## ハンズオン（12分）

**ここからは手を動かします**

<!--
【10:30】
・資料URLを黒板/チャットに再掲
・「詰まったら手を挙げる。それが最速です」
・GUI版に乗り換えたい人はいつでもどうぞ、と伝える
-->

---

## GitHub Flow — 実務そのままの流れ

```
① Issue  →  ② Branch  →  ③ Commit  →  ④ Push
                                          ↓
        ⑦ Merge  ←  ⑥ Review  ←  ⑤ Pull Request
```

| # | | 一言で |
|---|---|---|
| ① | Issue | 「これをやります」の宣言 |
| ② | Branch | 自分専用の作業ライン |
| ⑤ | PR | 「取り込んでください」のお願い |
| ⑦ | Merge | 本線に合流（**ゴール**） |

<!--
【11:00】
・「これは今日だけの練習ではなく、実務で毎日やっていること」
-->

---

## STEP 1-2：Issue を立てて clone

**① Issue を立てる**（ブラウザ）
→ Issues → New issue → 🎉 はじめてのPR → Create
**番号をメモ！**（`#12` など）

**② PCにコピーする**

```bash
cd ~
git clone https://github.com/guousuides/git-lec.git
cd git-lec
pwd     # ← 末尾が /git-lec になっているか必ず確認
```

<!--
【11:30】
・Issue作成時点で「もう草が1つ生えました」と言う → 早い成功体験
・pwd確認は全員にやらせる。ここを飛ばすと後で全滅する
-->

---

## STEP 3：ブランチを作る

```bash
git switch -c feat/taro-yamada-profile
```

<span class="warn">**`taro-yamada` を自分のGitHub IDに！**</span>

**期待する出力**

```
Switched to a new branch 'feat/taro-yamada-profile'
```

> `fatal: not a git repository` が出たら
> → **`pwd` で場所を確認。`cd ~/git-lec`**

<!--
【13:00】
・自分のIDに置き換える、を必ず2回言う
・ここで詰まる人が出るので、会場を回る時間を取る
-->

---

## STEP 4：自己紹介ファイルを作る

```bash
cp members/_TEMPLATE.md members/taro-yamada.md
code members/taro-yamada.md
```

- テンプレの `< >` を書き換えて **保存**
- **全部埋めなくてOK。1行でも十分です**
- <span class="warn">**本名・住所・電話番号は書かない**</span>（Publicです）

```bash
git status    # 自分のファイルが赤で出ればOK
```

<!--
【14:00】ここが唯一「考える」ステップ。3分取る
・書く内容で悩む人がいるので、members/cypher-cto.md を見せる
・「よろしくお願いします、だけでもOK」と言う
・code が使えない人は Finder/エクスプローラーから開かせる
-->

---

## STEP 5：add → commit

```bash
git add members/taro-yamada.md
```

```bash
git diff --staged    # 🔴 何を記録するか、自分の目で見る
```

```bash
git commit -m "feat: taro-yamada の自己紹介を追加"
```

**期待する出力**
```
[feat/taro-yamada-profile 3a4b5c6] feat: ...
 1 file changed, 15 insertions(+)
```

<!--
【17:00】
・diff --staged は絶対に飛ばさない。ここが今日の思想の核
・画面が止まったら q！
・「エディタが開いて操作不能」→ Esc → :q! → Enter を先に言っておく
・Please tell me who you are が出たら config
-->

---

## STEP 6：push

```bash
git push -u origin feat/taro-yamada-profile
```

**期待する出力**

```
 * [new branch]  feat/taro-yamada-profile -> ...
remote: Create a pull request ... by visiting:
remote:   https://github.com/.../pull/new/feat/taro-yamada-profile
```

<div class="big">

**③ → ④ に届きました**

</div>

<!--
【19:00】
・最後に出るURLをクリックすればPR画面に直行、と教える
・403 / Permission denied → Collaborator招待が未承認
  github.com/notifications を開かせる
・Authentication failed → gh auth login
-->

---

## STEP 7：Pull Request を出す

1. リポジトリを開く → 黄色い帯の **Compare & pull request**
2. タイトルを確認
3. テンプレを埋める（`close #12` を自分の番号に）
4. **Create pull request**

### 🔴 作った後、必ず2つ確認

- **Files changed** → 自分のファイルだけか
- **Commits** → アイコンが**灰色シルエットでないか**

<!--
【20:30】
・Commitsタブの灰色シルエット確認は全員にやらせる
  → ここで草が生えるかどうかが確定する
・灰色だった人はその場で git config を直させ、
  commit --amend --reset-author で作り直す（下記スクリプトはガイド参照）
-->

---

<!-- _class: lead -->

# STEP 8：Merge 🎉

**あなたの変更が `main` に入りました**

<!--
【22:00】
・ここで拍手を入れる。区切りを明確にする
・mergeは講師がまとめて押してもよい（時間管理優先）
-->

---

<!-- _class: lead -->

# Part 4
## 草（3分）

<!--
【24:00】
-->

---

## 草を確認する

**`https://github.com/あなたのID`** を開く

→ 今日の日付が **緑** になっていれば成功 🌱

### 生えていない人へ

**まず5分待ってリロード。** 反映に時間がかかります。

<!--
【24:00】
・スマホでも確認できる（プロジェクターに出すなら講師のIDで）
・ここは「できた！」を共有する時間。焦らせない
-->

---

## 草の罠 — なぜ生えないのか

| 罠 | 対処 |
|---|---|
| **`git config` のメール不一致** | GitHub登録済みアドレスに直す |
| **fork内のcommit** | 今日はforkを使っていないのでOK |
| PRを出していない | PRまで進む |
| 反映待ち | 5分待つ |

### 判定方法

PRの **Commits** タブ →
**灰色の人型シルエット** なら、メールが一致していません。

<!--
【25:00】
・「なぜ今日forkを使わなかったのか」をここで回収する
  → fork内commitは草にならないから、全員Collaboratorにした
・メール不一致だった人には noreply アドレスを勧める
  github.com/settings/emails
-->

---

## そして、正直な話

**草の量 ＝ エンジニアの実力、ではありません。**

- 業務のコードは会社のプライベートリポジトリにあります
- **優秀な人でも草が真っ白なことは普通にあります**

---

**今日の本当の成果は、緑のマスではなく**

<div class="big">

**「PRを出してmergeされる」流れを
一度自分の手でやったこと**

</div>

<!--
【26:00】
・草を目的化させない。ここは正直に言う
・ただし「初めての緑は普通に嬉しい」も認める
-->

---

<!-- _class: lead -->

# Part 5
## 番外編の予告（3分）

<!--
【27:00】
-->

---

## 番外編1：コンフリクト

**同じファイルの同じ行を、2人が変更した時に起きます。**

```
<<<<<<< HEAD
今日のひとこと: 自分が書いた内容
=======
今日のひとこと: 相手が書いた内容
>>>>>>> 9f8e7d6
```

**やることは1つ：記号を全部消して、あるべき形にする**

> **事故ではなく、安全装置です。**
> Gitが勝手に選んでいたら、誰かの変更が黙って消えます。
> 詰んだら `git merge --abort` で元に戻れます。

<!--
【27:00】
・練習場を用意してあることを伝える → conflict-playground/
・時間があれば実演。無ければ資料誘導のみ
-->

---

## 番外編2：AIエージェント

**Claude Code / GitHub Copilot は、
自然言語でGit操作を実行できます。**

```
「変更をコミットして、PRを作って」
```

→ AIが `git status` `git diff` `git add`
　`git commit` `git push` `gh pr create` を実行

<div class="big">

**AIが打つのは、
今日みなさんが打ったコマンドと同じです。**

</div>

<!--
【28:00】
・ここでライブデモ。不安定なら images/ のGIFで代替
・「AIが打っているのは、さっき自分が打ったコマンド」を必ず言う
-->

---

## だから、順番が大事でした

**AIは、承認を求めてきます。**

```
このコマンドを実行していいですか？ [y/n]
  git add -A
  git commit -m "..."
```

<div class="big">

**承認するのは、あなたです。**

</div>

**そのdiffが正しいか判定できるのは、
4領域とdiffの読み方を知っている人だけ。**

<!--
【28:30】
・本編との接続をここで明示する
・「だから番外編2は最後にありました」
-->

---

## AIも間違えます

| 危険な操作 | 何が起きるか |
|---|---|
| `git push --force` | **他人の作業がGitHubから消える** |
| `git reset --hard` | **未commitの作業が完全に消える** |
| `.env` をcommit | **APIキーが世界中に公開される** |

### 曖昧な指示が事故を生みます

| ❌ 危ない | ✅ 安全 |
|---|---|
| 「全部コミットして」 | 「members/ の変更だけコミットして」 |
| 「なかったことにして」 | 「直前のコミットを revert して」 |

<!--
【29:00】
・「AIがダメ」ではなく「曖昧な指示が危ない」というフレーミング
・請求書は自分に来る、という具体性が効く
-->

---

<!-- _class: lead -->

# 今日の結論

<div class="big">

**AIに任せる範囲が増えるほど、
「何が起きたか」を読む力が要る。**

</div>

今日の30分は、AIを**使わない**ための知識ではなく
AIを**安全に使い倒す**ための知識です。

<!--
【29:30】
・ここで締める。一番言いたいことなので、間を取る
-->

---

<!-- _class: lead -->

# お疲れさまでした 🎉

**持ち帰り課題**

1. `members/<自分のID>.md` を編集して、**2つ目のPR**を出す
2. 番外編を読む → `docs/05` と `docs/07`

**github.com/guousuides/git-lec**

質問は Issue か Discord `#git-lec` へ

<!--
【30:00】
・2回目は圧倒的に速い、と伝える（1回目の記憶が新しいうちに）
・Issueを立てるのも草になる、をもう一度言う
-->
