# 講師用ガイド — GitHub入門講座（初級編・30分）

**受講者は読まなくて構いません。** 講師・TA向けの運営マニュアルです。

---

## この講座の設計思想

**この3つを守れば、30分で全員がゴールに到達します。**

### 1. 本編では絶対にコンフリクトを起こさない

全員が `members/<自分のID>.md` という**別々の新規ファイル**を作ります。
同じ行を触る人が構造的に存在しないため、コンフリクトが起きません。

**初回でコンフリクトが発生すると、30分では絶対に終わりません。**
衝突は `conflict-playground/` に完全隔離し、番外編でのみ扱います。

### 2. forkを使わない（Collaborator方式）

| | fork方式 | **Collaborator方式（採用）** |
|---|---|---|
| 手順の長さ | 長い（remoteが2つ） | **短い** |
| forkの概念説明 | 必要 | **不要** |
| commitの草 | **生えない** | **生える** |
| 講師の事前準備 | 不要 | **全員招待が必要** |

「草を1つ生やして帰る」がゴールなので、**Collaborator方式一択**です。
その代わり、**事前の招待作業が講師の最重要タスク**になります（後述）。

### 3. 番外編2（AI）は、必ず本編の後

`docs/07_extra_ai_git.md` は、**本編を手で1周した人にだけ意味があります。**
順序を入れ替えないでください。理由は資料の冒頭に明記してあります。

---

## 事前準備チェックリスト

### 1週間前

- [ ] 受講者のGitHub IDを集める（フォーム / Discordで回収）
- [ ] **全員をCollaboratorに招待する**（下記スクリプト参照）
- [ ] 受講者に事前課題（[README](README.md#事前課題講座前日までに終わらせてください)）を案内
- [ ] **「招待メールの承認が最優先」を明示**して周知する

### 前日

- [ ] 招待の承認状況を確認（下記スクリプト）
- [ ] 未承認者に個別リマインド
- [ ] スライドをPDFで書き出す（[slides/README.md](slides/README.md)）
- [ ] 番外編2のデモ素材を `docs/images/` に配置（[docs/images/README.md](docs/images/README.md)）
- [ ] プロジェクターでコードブロックが後ろの席から読めるか確認

### 当日・開始30分前

- [ ] 自分の環境でハンズオンを1周する（リハーサル）
- [ ] `conflict-playground` の仕込み方針を決める（[instructor_setup.md](conflict-playground/instructor_setup.md)）
- [ ] ターミナルのフォントを**18pt以上**に設定
- [ ] Wi-Fi の状況を確認（`git clone` が30人同時に走ります）

### 当日・開始10分前

- [ ] 事前課題が終わっていない受講者を集めて個別対応
- [ ] 資料URLをチャット/黒板に掲示

---

## Collaborator一括招待スクリプト

`gh` CLI が必要です。

### 招待する

```bash
# ids.txt に1行1IDで書いておく
while read -r id; do
  [ -z "$id" ] && continue
  echo "inviting: $id"
  gh api -X PUT "repos/guousuides/git-lec/collaborators/$id" \
    -f permission=push >/dev/null && echo "  ✅ ok" || echo "  ❌ 失敗（IDを確認）"
done < ids.txt
```

> `permission=push` は「ブランチを作ってpushできる」権限です。
> `admin` は不要です（設定を壊されるリスクがあるため付けないでください）。

### 承認状況を確認する

```bash
# 承認済み
echo "=== 承認済み ==="
gh api "repos/guousuides/git-lec/collaborators" --paginate --jq '.[].login' | sort

# 招待中（未承認）← ここに残っている人が要注意
echo "=== 未承認（リマインド対象）==="
gh api "repos/guousuides/git-lec/invitations" --jq '.[].invitee.login'
```

> ⚠️ **未承認者は当日 `git push` で必ず 403 になります。**
> 前日と当日朝の2回、必ず確認してください。

### 当日その場で招待する（飛び込み参加者用）

```bash
gh api -X PUT "repos/guousuides/git-lec/collaborators/<GitHub ID>" -f permission=push
```

受講者側は https://github.com/notifications から即座に承認できます。**所要10秒です。**

---

## 時間配分表

| 経過 | 時間 | パート | 内容 | 判断ポイント |
|---|---|---|---|---|
| 0:00 | 3分 | **導入** | ゴール提示 / 「壊れません」 / 事前課題チェック | ここで未承認者を炙り出す |
| 3:00 | 4分 | **ターミナル** | `pwd` `ls` `cd` を全員に打たせる | 打てない人がいたらペア化 |
| 7:00 | 5分 | **Git/GitHub** | 4領域モデル / status / diff / ブランチ | ここは時間をかける |
| 12:00 | 12分 | **ハンズオン** | clone → branch → 編集 → commit → push → PR → merge | **遅れたらここで吸収** |
| 24:00 | 3分 | **草** | 確認 / 罠 / 草の量は実力ではない話 | 灰色シルエット確認は必須 |
| 27:00 | 3分 | **番外編予告** | コンフリクト / AIエージェント | デモ不調なら資料誘導のみ |
| 30:00 | — | 終了 | 持ち帰り課題 | |

### ハンズオン12分の内訳

| 経過 | 所要 | STEP | 詰まりやすさ |
|---|---|---|---|
| 12:00 | 1分 | Issue作成 | 低 |
| 13:00 | 2分 | clone + `cd` + **`pwd` 確認** | **高** ← ここが山場1 |
| 15:00 | 1分 | ブランチ作成 | 中（ID置換のミス） |
| 16:00 | 3分 | ファイル作成・編集 | 中（**書く内容で悩む**） |
| 19:00 | 2分 | add → diff確認 → commit | **高** ← ここが山場2 |
| 21:00 | 1分 | push | **高** ← ここが山場3（認証） |
| 22:00 | 2分 | PR作成 + 確認 | 中 |

### 🚨 遅延した時の削減優先順位

**上から順に削ってください。**

1. **STEP 10（後片付け）を丸ごと省略** → 2分浮く。持ち帰りにする
2. **`git diff --staged` の説明を短縮**（実行はさせる。説明を削る） → 1分
3. **ブランチの図の説明を口頭のみに** → 1分
4. **Issue作成を省略**（PRだけ出させる） → 1分 ※草は生えるので許容範囲
5. **番外編の予告を「資料を読んでください」だけに** → 3分

### ❌ 絶対に削ってはいけないもの

| 削らないもの | 理由 |
|---|---|
| **「壊れません」の宣言** | ここを削ると、詰まった人が固まって動けなくなります |
| **clone後の `pwd` 確認** | 全トラブルの半分の予防策です |
| **`git diff --staged` の実行** | 講座全体の思想の核です（番外編2への伏線） |
| **PR の Commits タブ確認** | 草が生えるかどうかがここで決まります |
| **merge まで到達すること** | ゴールそのものです |

**時間が足りなければ、番外編を全部捨ててでも merge まで行かせてください。**

---

## 進行の型

### 全体を通して

| 場面 | 言うこと |
|---|---|
| コマンドを出す時 | **「打ったらEnter。何も出なければ成功です」** |
| エラーが出た人がいた時 | **「正常です。全員出ます」**（会場全体に聞こえるように） |
| 詰まっている人を見つけた時 | **まず `pwd` を打たせる**。9割これで判明します |
| 進捗を確認する時 | 「◯◯が出た人？」と**出力を挙手で聞く**（「できた人？」だと嘘が混ざります） |

### 挙手確認のタイミング（3回だけ）

1. **clone後**：「`pwd` の末尾が `/git-lec` になっている人？」
2. **commit後**：「`1 file changed` と出た人？」
3. **push後**：「`new branch` と出た人？」

**この3点で全員を揃えてから次に進んでください。**

### TAの配置

- 受講者10名につきTA 1名が理想
- TAには**このガイドの「トラブルQ&A」だけ**を渡しておけば足ります
- **TAが最初にやることは「`pwd` を打たせる」**、と統一しておく

---

## トラブルQ&A — 即答スクリプト集

> 💬 **話し言葉のまま読み上げられる形**で書いてあります。
> 慌てている受講者に対しては、**まず「大丈夫です」から入ってください。**

---

### 🔴 A. push できない（403 / Permission denied）

**症状**
```
remote: Permission to guousuides/git-lec.git denied to taro-yamada.
fatal: unable to access '...': The requested URL returned error: 403
```

**原因**：Collaborator招待が未承認。**当日いちばん多いトラブルです。**

> 💬 **「大丈夫です、権限の話です。コードは何も間違っていません。**
> **github.com/notifications をブラウザで開いてください。**
> **招待が来ているので、Accept invitation を押してください。**
> **押したら、さっきのpushコマンドを↑キーで出して、もう一度Enterです。」**

**招待が届いていない場合**（講師が即座に実行）：

```bash
gh api -X PUT "repos/guousuides/git-lec/collaborators/<ID>" -f permission=push
```

---

### 🔴 B. 認証エラー（Authentication failed）

**症状**
```
fatal: Authentication failed for 'https://github.com/...'
remote: Support for password authentication was removed on August 13, 2021.
```
または
```
fatal: could not read Username for 'https://github.com': No such device or address
```

**原因**：GitHubにログインできていない。パスワード認証は廃止済み。

> 💬 **「GitHubのパスワードは、実はもう使えないんです。2021年に廃止されました。**
> **代わりに、これを打ってください。」**

```bash
gh auth login
```

> 💬 **「GitHub.com を選んで、HTTPS を選んで、Yes、**
> **最後に Login with a web browser を選んでください。**
> **8桁のコードが出るので、コピーしてEnter。ブラウザが開いたら貼り付けます。」**

**`gh` が入っていない場合の代替**（Windows）：

> 💬 **「Windowsの人は、一度これを打ってみてください。」**

```bash
git config --global credential.helper manager
```

> 💬 **「もう一度pushすると、ログイン画面がポップアップで出ます。」**

**それでもダメな場合の最終手段（Personal Access Token）**

1. https://github.com/settings/tokens/new を開く
2. Note に `git-lec`、Expiration は `7 days`
3. **`repo` にチェック**
4. Generate token → **表示された文字列をコピー**
5. push時のパスワード欄に、そのトークンを貼る

> ⚠️ トークンは**画面を離れると二度と見られません。** メモさせてください。

---

### 🔴 C. 草が生えない

**まず確認する順番**

> 💬 **「まず5分待ってリロードしてください。反映に時間がかかります。」**

それでもダメなら：

> 💬 **「PRのページを開いて、Commits タブを押してください。**
> **コミットの左のアイコン、あなたの顔（アバター）になっていますか？**
> **それとも灰色の人型のシルエットですか？」**

| 回答 | 診断 |
|---|---|
| **アバター** | ✅ 紐付いています。単なる反映待ち |
| **灰色シルエット** | ❌ メールアドレス不一致 |

**灰色だった場合**

> 💬 **「原因が分かりました。Gitに登録しているメールアドレスが、**
> **GitHubのアカウントのものと違っています。**
> **コミットは成功しているんですが、GitHubが『誰のコミットか分からない』状態です。」**

```bash
git config --global user.email
```

> 💬 **「これで出たアドレスを、GitHubに登録してあるものに直します。」**

**推奨：noreplyアドレスを使う**（メール公開の心配がなく、確実）

1. https://github.com/settings/emails を開かせる
2. `Keep my email addresses private` にチェック
3. すぐ下の `12345678+taro-yamada@users.noreply.github.com` をコピー

```bash
git config --global user.email "12345678+taro-yamada@users.noreply.github.com"
```

**既存のコミットを作り直す**（時間があれば）

```bash
git commit --amend --reset-author --no-edit
git push --force-with-lease
```

> ⚠️ **`--force-with-lease` は、自分1人しか使っていないブランチでのみ使えます。**
> 今日の受講者のブランチは自分専用なので安全です。
> **`--force` ではなく `--force-with-lease` を使わせてください。**
>
> 💬 **「今これを打つのは、あなた専用のブランチだから安全です。**
> **みんなが使う main では絶対に打たないでください。」**

**時間がない場合**

> 💬 **「configだけ直しておいてください。今日はPRを出したので、それで草は生えます。**
> **次にコミットする時から、ちゃんとあなたのものになります。」**

---

### 🔴 D. カレントディレクトリを見失う

**症状**
```
fatal: not a git repository (or any of the parent directories): .git
```

**これが今日の全トラブルの半分です。**

> 💬 **「大丈夫です。場所の問題です。まず、これを打ってください。」**

```bash
pwd
```

> 💬 **「何て出ましたか？ 最後が /git-lec になっていますか？」**

| pwdの結果 | 対処 |
|---|---|
| `/Users/taro` （git-lecが無い） | `cd ~/git-lec` |
| `/Users/taro/git-lec/docs` （深すぎる） | `cd ..` |
| `/Users/taro/Desktop/git-lec` | **そこで正解**。別の原因を疑う |
| `git-lec 2` のようなフォルダ | cloneを2回している。どちらか片方で作業させる |

**cloneした場所が分からない場合**

```bash
cd ~
ls
```

> 💬 **「git-lec っていうフォルダ、見えますか？ 見えなかったら Desktop の中かもしれません。」**

```bash
cd ~/Desktop
ls
```

**最終手段**

> 💬 **「見つからなければ、もう一度cloneしてしまいましょう。**
> **同じものが手に入るだけなので、何も損しません。」**

```bash
cd ~
git clone https://github.com/guousuides/git-lec.git
cd git-lec
pwd
```

---

### 🔴 E. detached HEAD になった

**症状**
```
You are in 'detached HEAD' state.
```
または `git status` の1行目が `HEAD detached at 3a4b5c6`

**原因**：`git checkout <コミットID>` を打った / タブ補完で変なものを選んだ

> 💬 **「大丈夫です。今、ブランチじゃなくて『過去のある1点』に立っている状態です。**
> **タイムマシンで過去に来ちゃっただけで、何も壊れていません。**
> **これを打つと、元のブランチに戻れます。」**

```bash
git switch -
```

> `-` は「直前にいたブランチ」という意味です。

**それでもダメな場合**（ブランチ名を直接指定）

```bash
git switch feat/taro-yamada-profile
```

**detached HEAD の状態でcommitしてしまった場合**

> 💬 **「そのコミット、消えていません。ちゃんと拾えます。」**

```bash
git log --oneline -1          # コミットIDを控える（例: 9f8e7d6）
git switch feat/taro-yamada-profile
git cherry-pick 9f8e7d6
```

> 💬 **「これで、さっき作ったコミットが正しいブランチに移りました。」**

---

### 🔴 F. 日本語ファイル名が文字化けする

**症状**：`git status` で日本語ファイル名がこう表示される
```
	"members/\343\201\237\343\202\215\343\201\206.md"
```

**原因**：Gitがマルチバイト文字をエスケープ表示する既定設定。

> 💬 **「壊れていません。表示の設定の問題です。これを打つと直ります。」**

```bash
git config --global core.quotepath false
```

**Windowsで、より根本的に文字化けする場合**（コミットメッセージが化ける等）

```bash
git config --global core.autocrlf true
git config --global i18n.commitEncoding utf-8
git config --global i18n.logOutputEncoding utf-8
```

Git Bash 側の設定：

> 💬 **「Git Bashの画面を右クリック → Options → Text →**
> **Character set が UTF-8 になっているか見てください。」**

**そもそもの予防策**

> 💬 **「ファイル名は英数字にしてください。**
> **今日作るファイルは自分のGitHub IDなので、日本語は使いません。」**

⚠️ **`members/` に日本語ファイル名を作られると、Actionsのチェックで落ちます。**
STEP 4 で「ファイル名は自分のGitHub ID」を強調してください。

---

### 🔴 G. エディタが開いて操作不能（Vim）

**症状**：`git commit` の後、画面が変な表示になって何を打っても反応しない

**原因**：`-m "メッセージ"` を書き忘れ、Vimが起動している

> 💬 **「大丈夫です、壊れていません。エディタが開いているだけです。**
> **Escキーを押してください。**
> **次に、コロン、q、ビックリマーク、と打ってEnterです。」**

```
Esc
:q!
Enter
```

> 💬 **「戻れましたね。今度は -m を付けて打ちましょう。」**

**恒久対策**（時間があれば）

```bash
git config --global core.editor "code --wait"
```

---

### 🔴 H. 画面が固まった（pager）

**症状**：`git log` や `git diff` の後、`:` だけが表示されて動かない

> 💬 **「壊れていません。長い文章を表示中なだけです。**
> **`q` キーを1回押してください。戻ります。」**

**恒久対策**

```bash
git config --global pager.log false
git config --global pager.diff false
```

---

### 🟡 I. push が rejected される

**症状**
```
! [rejected]        main -> main (fetch first)
error: failed to push some refs
```

> 💬 **「GitHubの方に、あなたが持っていない変更があります。**
> **先にそれを取り込んでから送ります。」**

```bash
git pull --rebase
git push
```

> ⚠️ **`--force` を提案しないでください。** 他人の作業が消えます。
> 受講者が自分で `--force` を打とうとしていたら止めてください。

コンフリクトが出た場合は [docs/05](docs/05_extra_conflict_revert.md) の手順へ。

---

### 🟡 J. `git add` したファイルが `git diff` で見えない

> 💬 **「消えていません。ステージに移動しただけです。**
> **`--staged` を付けると見えます。」**

```bash
git diff --staged
```

**これは説明のチャンスです。** 4領域モデルの ① と ② の違いが体感できます。

---

### 🟡 K. `code` コマンドが使えない

**症状**
```
bash: code: command not found
```

**対処（Mac）**

> 💬 **「VS Codeを起動して、command + Shift + P を押してください。**
> **`shell command` と入力すると、**
> **`Install 'code' command in PATH` が出るので選んでください。**
> **その後、ターミナルを開き直します。」**

**時間がない場合の回避**

> 💬 **「Finder（エクスプローラー）で git-lec/members を開いて、**
> **ファイルをダブルクリックしても同じです。そっちで行きましょう。」**

---

### 🟡 L. `cp` コマンドが分からない / 失敗する

**症状**
```
cp: members/_TEMPLATE.md: No such file or directory
```

**原因**：`git-lec` の外にいる

```bash
pwd          # /git-lec で終わっているか
ls members/  # _TEMPLATE.md が見えるか
```

**GUIでの回避**

> 💬 **「VS Codeの左のファイル一覧で、_TEMPLATE.md を右クリックしてコピー、**
> **members フォルダを右クリックして貼り付け、**
> **できたファイルを右クリックで Rename、で同じことができます。」**

---

### 🟡 M. Actionsのチェックが赤くなった

**受講者が動揺します。最優先で声をかけてください。**

> 💬 **「大丈夫です。それはテストが落ちたんじゃなくて、**
> **『ファイル名をこう直すといいですよ』って教えてくれているだけです。**
> **壊れていません。詳細を開いて、一緒に見ましょう。」**

チェックの詳細（Details）に**直し方のコマンドがそのまま書いてあります。**

**ファイル名を直す**

```bash
git mv members/いまの名前.md members/正しい名前.md
git commit -m "fix: ファイル名を修正"
git push
```

> pushすると自動で再チェックされます。

---

### 🔴 N. `.env` やAPIキーをcommitしてしまった

**Actionsが検出して落ちます。**

> 💬 **「よく気づきました。落ち着いてください。まだ main には入っていません。**
> **でも、順番が大事です。**
> **まず、そのAPIキーを無効化してください。ファイルを消すより先です。」**

**対処の順番（これを守らせる）**

1. **キーを無効化**（OpenAI / Anthropic / AWS のコンソールで Revoke）
2. ファイルをリポジトリから外す
3. `.gitignore` に追加
4. 報告する

```bash
git rm --cached .env
echo ".env" >> .gitignore
git add .gitignore
git commit -m "chore: .env を除外"
git push
```

> 💬 **「GitHubから消しても、漏れたキーは有効なままです。**
> **だから、無効化が最優先なんです。**
> **これ、誰でも一度はやります。報告してくれてありがとうございます。」**

詳細 → [docs/06_safety.md](docs/06_safety.md)

---

### 🟡 O. 「何を書けばいいか分からない」（STEP 4で固まる）

**技術ではなく心理的な詰まりです。意外と多いので想定しておいてください。**

> 💬 **「全部埋めなくて大丈夫です。**
> **『よろしくお願いします』の1行だけでも成立します。**
> **members/cypher-cto.md にサンプルがあるので、真似してください。**
> **後からいくらでも編集できます。今日は出すことが目的です。」**

---

### ⚪ P. 完全に詰んだ時の最終手段

**どうにもならない受講者が出たら、迷わずこれを使ってください。**

> 💬 **「一回、まっさらからやり直しましょう。**
> **何も損しません。5分で追いつけます。」**

```bash
cd ~
rm -rf git-lec
git clone https://github.com/guousuides/git-lec.git
cd git-lec
git switch -c feat/<ID>-profile
```

> ⚠️ `rm -rf` を受講者に打たせる時は、**必ず講師が手元を見ながら**にしてください。
> パスを間違えると別のものが消えます。

**さらに詰んだ場合：GUI版に丸ごと乗り換える**

> 💬 **「VS Codeでやりましょう。マウスだけで全部できます。」**
> → [docs/08_gui_version.md](docs/08_gui_version.md)

**それでもダメなら：GitHub Web UIだけで完結させる（最終手段）**

1. https://github.com/guousuides/git-lec/tree/main/members を開く
2. **Add file → Create new file**
3. ファイル名に `<ID>.md` を入力、内容を書く
4. 下部で **Create a new branch for this commit** を選択
5. **Propose new file** → PR作成

**ブラウザだけで、cloneもpushもせずにPRが作れます。**
**草も生えます。** 全員をゴールさせることを優先してください。

> 💬 **「これも立派なGitHubの使い方です。恥ずかしいことは何もありません。**
> **実際、ドキュメントの誤字修正なんかは、私もこれでやっています。」**

---

## 番外編1（コンフリクト）を実施する場合

**別枠10〜15分**が必要です。30分の中には収まりません。

- 受講者向け手順 → [docs/05_extra_conflict_revert.md](docs/05_extra_conflict_revert.md)
- **仕込み手順 → [conflict-playground/instructor_setup.md](conflict-playground/instructor_setup.md)**

### 仕込みのタイミングが重要です

受講者が編集**する前**に `git pull` させ、**その後で**講師が `main` を更新します。
詳細は [instructor_setup.md の「注意点」](conflict-playground/instructor_setup.md#-注意点) を必読。

**前日に仕込む運用も可能です。** その場合は受講者に STEP 1 の `git pull` を飛ばさせてください。

### 全体が混乱した時

> 💬 **「一旦、全員これを打ってください。元に戻ります。」**

```bash
git merge --abort
git switch main
git pull
```

**何も失われません。** これを最初に伝えておくと、受講者が怖がりません。

---

## 番外編2（AI）を実施する場合

**別枠8〜10分。**

### 実施の絶対条件

> **本編（STEP 1〜8）を全員が完了していること。**

未完了の人がいる状態でAI編に入ると、
「じゃあ最初からAIでよかったのでは」という**最悪の誤読**が生まれます。

### ライブデモの構成

1. **指示例1（状況説明）** — 安全。失敗しても被害なし。**まずこれから**
2. **指示例2（コミット）** — **承認プロンプトで必ず一度止める**
3. **指示例3（PR作成）** — 時間があれば

### 🎯 デモ中に必ず言うこと

**承認プロンプトが出た瞬間に、指差しながら：**

> 💬 **「見てください。ここに出ているのは、**
> **さっきみなさんが手で打った `git add` と `git commit` です。**
> **全く同じものです。**
>
> **そして今、『実行していいですか』と聞かれています。**
> **みなさんは今、この画面を見て『何が起きようとしているか』が読めます。**
> **それが、今日30分やったことの価値です。」**

### デモが失敗した場合

**慌てず、素材に切り替えてください。**

→ `docs/images/` のGIF/スクショ
→ 素材も無い場合は [docs/07 の口頭説明用テキスト](docs/07_extra_ai_git.md#素材も無い場合の口頭説明用テキスト) を読み上げる

> 💬 **「今ちょうどいい例が出ましたね。AIも失敗します。**
> **だから人間が見ている必要があるんです。」**

**デモの失敗を、そのままメッセージに変換できます。** 慌てないでください。

---

## 講座後にやること

- [ ] 全員のPRがmergeされたか確認
- [ ] mergeされていないPRにコメントを付ける（放置しない）
- [ ] 草が生えなかった受講者を個別フォロー
- [ ] Issueテンプレの「詰まったところ」の回答を集計 → **資料改善に使う**
- [ ] `conflict-playground/guestbook.md` を初期状態にリセット（次回のため）
- [ ] 使い終わったCollaborator権限の扱いを決める（残しても実害はありません）

### 受講者への事後フォロー文（コピペ用）

```
お疲れさまでした！

今日やったこと（clone → branch → commit → push → PR → merge）は、
実務のエンジニアが毎日やっている流れと完全に同じです。

【ぜひやってみてほしいこと】
1. members/<自分のID>.md を編集して、2つ目のPRを出す
   → 1回目より圧倒的に速いはずです
2. 番外編を読む
   - コンフリクト解消: docs/05_extra_conflict_revert.md
   - AIエージェント:   docs/07_extra_ai_git.md

草が生えていない人は docs/02_kusa.md のチェックリストを見てください。
いちばん多い原因は git config のメールアドレス不一致です。

質問はいつでも Issue か Discord #git-lec へどうぞ。
Issueを立てるのも草になります 🌱
```

---

## 参考：受講者が最も詰まる箇所ランキング

**ここに人員と時間を配分してください。**

| 順位 | 箇所 | 対策 |
|---|---|---|
| 1 | **push時の認証・権限（403）** | 事前の招待承認確認を徹底。当日その場で招待できる準備 |
| 2 | **カレントディレクトリの喪失** | clone後の `pwd` 確認を全員でやる |
| 3 | **`git config` のメール不一致** | 開始3分の事前課題チェックで炙り出す |
| 4 | **自分のIDへの置換忘れ** | コマンドを出すたびに「IDは自分のものに」と言う |
| 5 | **STEP 4 で何を書くか悩む** | サンプルを見せる。「1行でOK」と言う |
| 6 | **Vimからの脱出** | commitの前に予告しておく（Esc → `:q!`） |

---

**関連資料**
[README.md](README.md) ｜ [docs/](docs/) ｜ [slides/README.md](slides/README.md) ｜ [conflict-playground/instructor_setup.md](conflict-playground/instructor_setup.md)
