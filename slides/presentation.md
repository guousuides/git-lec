---
marp: true
theme: default
paginate: true
size: 16:9
header: 'Cypher GitHub入門講座（初級編・30分）'
footer: '© Cypher — AI & Data Science Community'
style: |
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&family=Noto+Sans+JP:wght@400;500;700;900&family=JetBrains+Mono:wght@400;700&display=swap');

  section {
    font-family: 'Noto Sans JP', 'Inter', sans-serif;
    font-size: 24px;
    padding: 35px 55px;
    background-color: #0d1117;
    color: #c9d1d9;
    letter-spacing: -0.01em;
  }
  h1 {
    font-family: 'Inter', 'Noto Sans JP', sans-serif;
    color: #58a6ff;
    font-size: 38px;
    font-weight: 800;
    margin-bottom: 15px;
    line-height: 1.25;
  }
  h2 {
    color: #79c0ff;
    font-size: 28px;
    font-weight: 700;
    border-bottom: 2px solid #21262d;
    padding-bottom: 6px;
    margin-top: 0;
    margin-bottom: 16px;
  }
  h3 {
    color: #e6edf3;
    font-size: 22px;
    font-weight: 600;
    margin-bottom: 10px;
  }
  p, li {
    line-height: 1.55;
    margin-bottom: 8px;
  }
  strong {
    color: #ffa657;
    font-weight: 700;
  }
  em {
    color: #7ee787;
    font-style: normal;
    font-weight: 700;
  }
  code {
    font-family: 'JetBrains Mono', Consolas, monospace;
    background-color: #161b22;
    color: #f0883e;
    padding: 2px 8px;
    border-radius: 6px;
    font-size: 0.88em;
    border: 1px solid #30363d;
  }
  pre {
    background-color: #161b22 !important;
    border: 1px solid #30363d;
    border-radius: 8px;
    padding: 12px 18px !important;
    margin: 10px 0;
  }
  pre code {
    background: none;
    color: #79c0ff;
    padding: 0;
    border: none;
    font-size: 0.82em;
    line-height: 1.45;
  }
  blockquote {
    background: #161b22;
    border-left: 5px solid #238636;
    padding: 10px 16px;
    border-radius: 0 8px 8px 0;
    margin: 12px 0;
    color: #e6edf3;
    font-size: 0.95em;
  }
  table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.88em;
    margin: 12px 0;
  }
  th {
    background-color: #161b22;
    color: #58a6ff;
    border: 1px solid #30363d;
    padding: 8px 14px;
    text-align: left;
  }
  td {
    border: 1px solid #30363d;
    padding: 8px 14px;
    background-color: #0d1117;
  }
  .lead-title {
    font-size: 46px;
    color: #58a6ff;
    font-weight: 900;
    line-height: 1.2;
    margin-bottom: 12px;
  }
  .subtitle {
    font-size: 26px;
    color: #8b949e;
    font-weight: 500;
    margin-bottom: 30px;
  }
  .tag {
    display: inline-block;
    padding: 2px 10px;
    border-radius: 12px;
    font-size: 0.72em;
    font-weight: 700;
    margin-right: 6px;
    vertical-align: middle;
  }
  .tag-cli { background: #1f6feb; color: #ffffff; }
  .tag-gui { background: #238636; color: #ffffff; }
  .tag-concept { background: #8957e5; color: #ffffff; }
  .tag-time { background: #d29922; color: #000000; }
  .tag-warn { background: #da3633; color: #ffffff; }
  .card-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 16px;
    margin-top: 10px;
  }
  .card {
    background: #161b22;
    border: 1px solid #30363d;
    border-radius: 8px;
    padding: 14px 18px;
  }
  .card-highlight {
    background: #161b22;
    border: 1px solid #238636;
    border-radius: 8px;
    padding: 14px 18px;
  }
  .step-num {
    display: inline-block;
    width: 28px;
    height: 28px;
    background: #1f6feb;
    color: white;
    border-radius: 50%;
    text-align: center;
    line-height: 28px;
    font-size: 0.8em;
    font-weight: bold;
    margin-right: 8px;
  }
---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _header: '' -->

<div style="text-align: center; margin-top: 40px;">
  <span class="tag tag-time">30分で完走</span>
  <span class="tag tag-concept">完全未経験歓迎</span>

  <div class="lead-title" style="margin-top: 15px;">GitHub入門講座</div>
  <div class="subtitle">〜 はじめてのPull Request & 草を生やそう 〜</div>

  <div style="color: #8b949e; font-size: 20px; margin-top: 30px;">
    学生AI/データサイエンスコミュニティ <strong>Cypher</strong>
  </div>
</div>

---

## この30分のゴール

<div class="card-highlight" style="margin-top: 20px; font-size: 1.15em; text-align: center; padding: 25px;">
  <span style="font-size: 1.4em;">🌿</span><br>
  <strong>あなたのPull Requestがmergeされ、<br>GitHubのプロフィールに「草」が1つ生えている。</strong>
</div>

<div class="card-grid" style="margin-top: 20px;">
  <div class="card">
    <h3>🌱 草（くさ）とは？</h3>
    GitHubで開発活動（コミットなど）をした日にプロフィールに付く<strong>緑のマス目</strong>のこと。
  </div>
  <div class="card">
    <h3>📬 Pull Request（PR）とは？</h3>
    「自分の変更を本番に取り込んでください！」という<strong>公式のお願い投稿</strong>のこと。
  </div>
</div>

---

## 最初に、いちばん大事な約束

<div class="card-highlight" style="border-color: #388bfd; padding: 20px; margin-top: 10px;">
  <h3 style="color: #58a6ff; font-size: 1.3em; margin: 0 0 10px 0;">🛡️ あなたのPCもリポジトリも壊れません</h3>
  <p style="margin: 0;">Gitは「歴史を記録する道具」です。<strong>失敗してもいつでも過去に戻せます。</strong></p>
</div>

<div style="margin-top: 20px;">

- ❌ **エラーが出た？** ➡️ <em>正常です！</em> 講師も毎日10回はエラーを出します。
- ❓ **分からなくなった？** ➡️ <em>即、手を挙げてください！</em> TAと講師が助けます。
- 🖥️ **黒い画面が怖い？** ➡️ 大丈夫、今日打つコマンドは<strong>数行だけ</strong>です。

</div>

> 💡 エラーメッセージは「あなたを怒る文章」ではなく**「次へのヒント」**です。

---

## 今日のタイムスケジュール（30分）

| 時間 | パート | 内容 |
|---|---|---|
| **00–03分** | 導入 | ゴール確認・事前課題セルフチェック |
| **03–07分** | Part 1 | ターミナルってなに？ `pwd` / `cd` / `ls` |
| **07–12分** | Part 2 | Git vs GitHub & 荷物でわかる4領域モデル |
| **12–24分** | **Part 3** | **【ハンズオン】自己紹介を作ってPRを出そう！** |
| **24–27分** | Part 4 | プロフィールの草を確認 & 生えない罠の対策 |
| **27–30分** | Part 5 | まとめ & AI時代におけるGitの付き合い方 |

> 💻 **GUI派の方へ**：全手順をVS Codeのマウス操作で行う手順書もあります！

---

## 事前課題 クイックチェック

手元のターミナル（Windowsは Git Bash）で確認してみましょう！

| # | 確認項目 | 打つコマンド | 期待される結果 |
|---|---|---|---|
| 1 | Gitが入っている | `git --version` | `git version 2.xx.x` |
| 2 | 名前が登録されている | `git config --global user.name` | あなたのGitHub ID |
| 3 | メールが登録されている | `git config --global user.email` | GitHubの登録メール |
| 4 | GitHubログイン済み | `gh auth status` | `✓ Logged in to github.com` |

> ⚠️ まだの項目がある人、赤字のエラーが出た人は**すぐに手を挙げてください**！

---

<!-- _class: lead -->
<!-- _header: '' -->

<span class="tag tag-time">Part 1 (03–07分)</span>
<div class="lead-title" style="margin-top: 10px;">ターミナルってなに？</div>
<div class="subtitle">黒い画面は「文字でおしゃべりする道具」</div>

---

## ターミナル（黒い画面）の正体

普段のマウス操作と、やっていることは**まったく同じ**です！

<div class="card-grid" style="margin-top: 15px;">
  <div class="card">
    <h3 style="color: #79c0ff;">🖱️ GUI（マウス操作）</h3>
    <ul>
      <li>フォルダをダブルクリックして開く</li>
      <li>右クリック ➡️ 「新規作成」</li>
      <li>目で見て直感的に動かせる</li>
    </ul>
  </div>
  <div class="card">
    <h3 style="color: #ffa657;">⌨️ CUI / ターミナル</h3>
    <ul>
      <li><code>cd folder</code> と指示して移動する</li>
      <li><code>touch file</code> と指示して作る</li>
      <li><strong>自動化やAIとの連携が得意！</strong></li>
    </ul>
  </div>
</div>

> **たとえ**：GUIが「お店で指差し注文」なら、ターミナルは「LINEでテキスト注文」。

---

## ターミナルで一番大事なこと：「今どこにいるか」

ターミナルは**「今いる場所（カレントディレクトリ）」**を基準にして動きます。

<div class="card-highlight" style="margin: 15px 0;">
  <strong>カレントディレクトリ</strong>（Current Directory）＝ ターミナルが今開いているフォルダのこと
</div>

```
/Users/taro/
  ├── Desktop/      ← デスクトップ
  ├── Downloads/    ← ダウンロード
  └── Documents/    ← 書類
```

- 今 `Desktop` にいるのか？ それとも `Downloads` にいるのか？
- **場所を見失ったら、まず「今どこ？」を確認する**のが鉄則です！

---

## 覚えるコマンドは3つだけ！

<div class="card-grid">
  <div class="card">
    <h3><code>pwd</code>（今どこ？）</h3>
    <strong>P</strong>rint <strong>W</strong>orking <strong>D</strong>irectory<br>
    今いるフォルダの場所（パス）を画面に表示します。
  </div>
  <div class="card">
    <h3><code>ls</code>（何がある？）</h3>
    <strong>L</strong>i<strong>s</strong>t<br>
    今いるフォルダの中にあるファイルやフォルダの一覧を表示します。
  </div>
</div>

<div class="card" style="margin-top: 15px;">
  <h3><code>cd フォルダ名</code>（そこへ移動！）</h3>
  <strong>C</strong>hange <strong>D</strong>irectory<br>
  指定したフォルダの中に移動します。（例：<code>cd Desktop</code> でデスクトップへ移動）<br>
  ※ <code>cd ..</code>（ドット2つ）で「1つ上の階層に戻る」
</div>

---

## ターミナル ミニ体験

実際に打ってみましょう！（1行打ったらEnterキー）

```bash
pwd
```
```
/Users/taro   # (あなたの現在地が表示されます)
```

```bash
ls
```
```
Desktop  Documents  Downloads   # (フォルダの一覧が出ます)
```

```bash
cd Desktop
pwd
```
```
/Users/taro/Desktop   # (デスクトップに移動できました！)
```

---

<!-- _class: lead -->
<!-- _header: '' -->

<span class="tag tag-time">Part 2 (07–12分)</span>
<div class="lead-title" style="margin-top: 10px;">Git vs GitHub & 4領域モデル</div>
<div class="subtitle">荷物の発送で仕組みを一発理解する</div>

---

## Git と GitHub は「別物」です

名前は似ていますが、役割がまったく違います！

|  | Git（ギット） | GitHub（ギットハブ） |
|---|---|---|
| **正体** | あなたのPCに入る**アプリ・道具** | ネット上の**Webサービス** |
| **場所** | 手元のパソコンの中 | クラウド（インターネット） |
| **役割** | ファイルの変更履歴を**記録**する | 履歴を**共有**してみんなで開発する |
| **ネット** | **不要**（オフラインで動く！） | 必要 |

> **たとえ**：Git = <strong>カメラ（撮影する道具）</strong> ｜ GitHub = <strong>Instagram（写真を投稿・共有する場所）</strong>

---

## Gitの「4領域モデル」

Gitの世界には **4つの場所** があります。変更はここを順番に移動します。

```
 [① 作業場]  ──── git add ────▶  [② ステージ]
 (Working Tree)                  (Staging Area)
      │                                │
      │                                ▼ git commit
      │                         [③ 手元の保存箱]
      │                         (Local Repository)
      │                                │
      │                                ▼ git push
      └───────── git pull ────── [④ GitHubの保存箱]
                                (Remote Repository)
```

**①〜③はあなたのPCの中。④だけがインターネット上です。**

---

## 荷物の発送でたとえる「4領域」

<div class="card-grid">
  <div class="card">
    <span class="step-num">1</span><strong>作業場（Working Tree）</strong><br>
    部屋で荷物を広げて作業している状態。<br>
    <em>（ファイルを編集しただけ）</em>
  </div>
  <div class="card">
    <span class="step-num">2</span><strong>ステージ（Staging Area）</strong><br>
    「送る物」を選んでダンボールに入れた状態。<br>
    <em>（<code>git add</code> で選別）</em>
  </div>
  <div class="card">
    <span class="step-num">3</span><strong>ローカル（Local Repository）</strong><br>
    ダンボールにガムテープを貼り、封をした状態。<br>
    <em>（<code>git commit</code> で手元に記録確定）</em>
  </div>
  <div class="card">
    <span class="step-num">4</span><strong>リモート（GitHub）</strong><br>
    郵便局に持っていき、相手に届いた状態！<br>
    <em>（<code>git push</code> で世界へ公開）</em>
  </div>
</div>

---

## よくある疑問：「なぜステージがあるの？」

「ファイルを編集したら、そのまま保存（commit）じゃダメなの？」

<div class="card" style="margin-top: 15px;">
  <h3 style="color: #79c0ff;">💡 理由：関係ない変更を混ぜないため！</h3>
  <p>例えば、同時に3つのファイルを編集したとします：</p>
  <ul>
    <li><code>login.py</code>（ログイン機能の追加） ➡️ <strong>今回のコミットに含めたい！</strong></li>
    <li><code>test_memo.txt</code>（個人的な落書きメモ） ➡️ <strong>人に見せたくない…</strong></li>
  </ul>
  <p style="margin-top: 10px;">
    <code>git add login.py</code> とすることで、<strong>「送りたい物だけ」を綺麗に選んで箱詰め</strong>できます。
  </p>
</div>

---

<!-- _class: lead -->
<!-- _header: '' -->

<span class="tag tag-time">Part 3 (12–24分)</span>
<div class="lead-title" style="margin-top: 10px;">ハンズオン本編！</div>
<div class="subtitle">自己紹介ファイルを作って Pull Request を出そう</div>

---

## これからやるハンズオンの流れ（GitHub Flow）

実務のエンジニアが毎日やっている**「王道の開発手順」**を体験します！

<div style="font-size: 0.9em; margin-top: 15px;">

1. 📥 **clone** ➡️ プロジェクトを自分のPCに持ってくる
2. 🌿 **branch** ➡️ 自分専用の作業ブランチ（枝）を作る
3. 📝 **編集** ➡️ `members/あなたのID.md` を作成して自己紹介を書く
4. 📦 **add** ➡️ 変更をステージ（発送箱）に入れる
5. 🔒 **commit** ➡️ 変更を手元の記録として確定する
6. 🚀 **push** ➡️ GitHubに送り届ける
7. 📬 **PR作成** ➡️ 「取り込んでください！」とPRを出す
8. 🎉 **Merge** ➡️ 講師が承認して合体！

</div>

---

## Step 1. リポジトリを手元に持ってくる

<span class="tag tag-cli">CLI</span> `Desktop` に移動して、リポジトリを丸ごと複製（clone）します。

```bash
cd Desktop
git clone https://github.com/guousuides/git-lec.git
```

<span class="tag tag-gui">VS Code</span> 「クローン」ボタンを押し、上のURLを貼り付けます。

<div class="card" style="margin-top: 10px;">
  <strong>期待される結果：</strong> デスクトップに <code>git-lec</code> フォルダが新しく作られます！
</div>

```bash
cd git-lec
```
> ⚠️ **超重要**：必ず `cd git-lec` でフォルダの中に入ってください！

---

## Step 2. 自分専用の作業ブランチを作る

みんなで同じ本番（`main`）を直接いじると事故が起きます。<br>
安全のため**「自分専用の枝分かれ（ブランチ）」**を作って作業します。

<span class="tag tag-cli">CLI</span> 自分のID名でブランチを作成して切り替えます：

```bash
git switch -c add-member-あなたのID
```
*(例：`git switch -c add-member-taro-yamada`)*

<span class="tag tag-gui">VS Code</span> 左下の `main` をクリック ➡️ 「新しい分岐の作成」

<div class="card" style="margin-top: 10px;">
  <strong>期待される結果：</strong> <code>Switched to a new branch 'add-member-...'</code> と出ればOK！
</div>

---

## Step 3. 自己紹介ファイルを作る

`members/` フォルダの中に、**`あなたのGitHub ID.md`** を作成します！

<div class="card-grid">
  <div class="card">
    <h3 style="color: #79c0ff;">📁 ファイルの場所</h3>
    <code>members/taro-yamada.md</code><br>
    <em>（※拡張子は <code>.md</code> です）</em>
  </div>
  <div class="card">
    <h3 style="color: #7ee787;">✍️ 中に書く内容（自由）</h3>
    <pre><code># 自己紹介

- **名前**: 山田 太郎
- **所属**: ○○大学 / Cypher
- **一言**: GitHubマスターになります！</code></pre>
  </div>
</div>

> 💡 VS Codeのエクスプローラーから `members` フォルダを右クリックして「新規ファイル」で作ると簡単です！

---

## Step 4. 今の状態を確認する

今、Gitから見てファイルがどうなっているか確認してみましょう！

```bash
git status
```

<div class="card" style="margin-top: 10px;">
  <pre><code>Untracked files:
  (use "git add &lt;file&gt;..." to include in what will be committed)
	members/taro-yamada.md   # ← 赤文字で表示されます！</code></pre>
</div>

- **赤文字（Untracked）** ＝ 「部屋に新しい物があるけど、まだ発送箱（ステージ）には入っていませんよ」という合図です。

---

## Step 5. 発送箱に入れる（add）

作成した自己紹介ファイルを、ステージ（発送箱）に乗せます。

<span class="tag tag-cli">CLI</span> 
```bash
git add members/あなたのID.md
```
*(または `git add .` で今のフォルダの全変更をステージ)*

<span class="tag tag-gui">VS Code</span> ソース管理パネルで、ファイル名の横の **「+」ボタン** をクリック

もう一度 `git status` を打ってみましょう：
<div class="card">
  <pre><code>Changes to be committed:
	new file:   members/taro-yamada.md   # ← 緑文字に変わった！</code></pre>
</div>

---

## Step 6. 記録を確定して封をする（commit）

「何を変更したか」のメッセージを添えて、手元に記録します。

<span class="tag tag-cli">CLI</span>
```bash
git commit -m "docs: add taro-yamada to members"
```

<span class="tag tag-gui">VS Code</span> メッセージ欄に `docs: add ...` と入力して **「コミット」** ボタン

<div class="card" style="margin-top: 10px;">
  <pre><code>[add-member-taro-yamada a1b2c3d] docs: add taro-yamada to members
 1 file changed, 5 insertions(+)
 create mode 100644 members/taro-yamada.md</code></pre>
  <em>これで「PC内の保存箱」にしっかり記録されました！🎉</em>
</div>

---

## Step 7. GitHubへ送り出す（push）

手元に作った記録を、インターネット上のGitHubへアップロードします！

<span class="tag tag-cli">CLI</span>
```bash
git push -u origin add-member-あなたのID
```

<span class="tag tag-gui">VS Code</span> **「ブランチの発行」** または **「変更の同期」** ボタン

<div class="card" style="margin-top: 10px;">
  <pre><code>To https://github.com/guousuides/git-lec.git
 * [new branch]      add-member-taro-yamada -> add-member-taro-yamada
Branch 'add-member-taro-yamada' set up to track remote branch.</code></pre>
  <em>GitHubにあなたのブランチが届きました！🚀</em>
</div>

---

## Step 8. Pull Request（PR）を作成する

GitHubの画面（ブラウザ）を開きましょう！

1. リポジトリ（ `https://github.com/guousuides/git-lec` ）を開く
2. 上部に黄色いバー **「Compare & pull request」** ボタンが出るのでクリック！

```
  ┌────────────────────────────────────────────────────────────┐
  │ 🌿 add-member-taro-yamada had recent pushes 1 minute ago   │
  │ [ Compare & pull request ]                                 │
  └────────────────────────────────────────────────────────────┘
```

> ※ボタンが出ない場合：「Pull requests」タブ ➡️ 「New pull request」 ➡️ 自分のブランチを選択

---

## Step 9. PRの内容を書いて送信！

<div class="card-grid">
  <div class="card">
    <h3 style="color: #79c0ff;">1. タイトル</h3>
    <code>docs: add taro-yamada to members</code><br>
    のように分かりやすく書きます。
  </div>
  <div class="card">
    <h3 style="color: #79c0ff;">2. 本文</h3>
    テンプレのチェックボックスを埋めます：<br>
    <code>- [x] 自己紹介を作成した</code>
  </div>
</div>

<div style="text-align: center; margin-top: 25px;">
  緑色の <strong>「Create pull request」</strong> をクリック！ ➡️ <span style="font-size: 1.2em;">📬 送信完了！</span>
</div>

---

## Step 10. レビュー & Merge！🎉

<div class="card-highlight" style="text-align: center; padding: 25px;">
  <h2 style="color: #7ee787; border: none; margin-bottom: 10px;">👨‍🏫 講師がその場で全員のPRをMerge（合体）します！</h2>
  <p style="font-size: 1.1em; margin: 0;">
    GitHub上のPR画面が <strong>「Merged (紫色のアイコン)」</strong> に変わる瞬間を見届けましょう！
  </p>
</div>

<div style="margin-top: 20px; text-align: center;">
  紫色の <code>Merged</code> マークがついたら、<strong>あなたの一連の作業は大成功です！</strong> 🎊
</div>

---

<!-- _class: lead -->
<!-- _header: '' -->

<span class="tag tag-time">Part 4 (24–27分)</span>
<div class="lead-title" style="margin-top: 10px;">草を確認しよう！</div>
<div class="subtitle">プロフィールに緑色のマス目はついたかな？</div>

---

## 自分のプロフィールを見に行こう！

ブラウザで自分のプロフィールページを開いてみましょう：
**`https://github.com/あなたのID`**

<div class="card-highlight" style="margin-top: 20px; text-align: center; padding: 20px;">
  <span style="font-size: 2em;">🟩 🟩 🟩 🟩 🟩</span><br>
  <strong style="font-size: 1.2em; color: #7ee787;">今日のマス目に色がついて「草」が生えています！</strong>
</div>

> 「草が生える」＝ あなたが世界に向けてオープンな開発活動を一歩踏み出した証拠です！

---

## 🚨 もし草が生えていなかったら？「3大罠」

「PRはマージされたのに草が生えていない！」という場合のチェックリスト：

<div class="card-grid">
  <div class="card">
    <h3 style="color: #ff7b72;">罠① メールアドレスの不一致（90%はこれ）</h3>
    <code>git config user.email</code> のメアドと、GitHubに登録されているメアドが1文字でも違うと草になりません。
  </div>
  <div class="card">
    <h3 style="color: #ff7b72;">罠② まだマージされていない</h3>
    ブランチにコミットしただけでは草になりません。<code>main</code> にマージされて初めて反映されます。
  </div>
</div>

<div class="card" style="margin-top: 15px;">
  <h3 style="color: #ff7b72;">罠③ 自分のFork（コピーリポジトリ）で作業してしまった</h3>
  Fork先のコミットは、元のリポジトリにPRを出してマージされるまで草カウントされません。
</div>

---

## 罠①（メアド不一致）の治し方

ターミナルで設定を修正し、GitHub側にもメールを追加すれば解決します！

```bash
# 1. 今の設定を確認
git config --global user.email

# 2. GitHubに登録しているメアドに上書き設定
git config --global user.email "your-correct-email@example.com"
```

> 💡 GitHubの [Settings] ➡️ [Emails] に、PC側で設定していたメールアドレスを追加登録することでも、過去のコミットが自分のものとして紐づけられて草が生えます！

---

<!-- _class: lead -->
<!-- _header: '' -->

<span class="tag tag-time">Part 5 (27–30分)</span>
<div class="lead-title" style="margin-top: 10px;">まとめ & AI時代のGit</div>
<div class="subtitle">AIがコマンドを打つ時代に、人間は何をするのか？</div>

---

## 今日できるようになったこと 🎓

たった30分で、実務のエンジニアと同じスキルを習得しました！

<div class="card" style="margin-top: 15px;">

- ✅ **ターミナルの基本**（`pwd`, `cd`, `ls` で現在地を迷わない）
- ✅ **Gitの4領域モデル**（作業場 ➡️ ステージ ➡️ ローカル ➡️ リモート）
- ✅ **GitHub Flowの実践**（clone ➡️ branch ➡️ commit ➡️ push ➡️ PR）
- ✅ **草を生やす仕組み**（メール認証・マージ条件）

</div>

---

## 番外編1：コンフリクト（衝突）と元に戻す方法

同じファイルの同じ行を2人が同時に編集すると**「コンフリクト（衝突）」**が起きます。

<div class="card-grid" style="margin-top: 15px;">
  <div class="card">
    <h3>⚔️ コンフリクトは怖くない</h3>
    Gitが「どっちを採用する？」と親切に聞いてくれている状態です。VS Codeならボタン1つで選べます。
  </div>
  <div class="card">
    <h3>⏪ やり直す道具（revert）</h3>
    間違えてマージした時は <code>git revert</code> で「打ち消すコミット」を作れば安全に戻せます。
  </div>
</div>

> 詳しくは 📄 `docs/05_extra_conflict_revert.md` と `conflict-playground/` をチェック！

---

## 番外編2：AIエージェント時代のGit操作

現代は、Claude Code や GitHub Copilot などのAIが<br>
**自然言語の指示だけで `add` / `commit` / `push` / `PR作成` まで自動実行**できる時代です。

<div class="card-highlight" style="margin-top: 15px;">
  <p style="margin: 0; color: #58a6ff; font-weight: bold;">
    💬 人間「自己紹介を追加してPRを作っておいて」<br>
    🤖 AI 「変更をステージングし、コミットしてPR #12 を作成しました！」
  </p>
</div>

「じゃあ、人間がGitを勉強する意味はなくなったの？」<br>
➡️ **逆です。これまで以上にGitの理解が必要になっています。**

---

## なぜAI時代に「4領域」と「diff」を学ぶのか？

<div class="card-grid" style="margin-top: 15px;">
  <div class="card">
    <h3 style="color: #ff7b72;">⚠️ AIも間違える</h3>
    <ul>
      <li>パスワードや <code>.env</code> をコミットしてしまう</li>
      <li>消してはいけないコードを消してしまう</li>
      <li>勝手に <code>push --force</code> してしまう</li>
    </ul>
  </div>
  <div class="card">
    <h3 style="color: #7ee787;">🛡️ 人間の最後の責任</h3>
    <ul>
      <li>AIが出した<strong>差分（diff）を自分の目で読む</strong></li>
      <li>「今どの領域に何があるか」を把握する</li>
      <li>問題がないことを確認して<strong>承認（Approve）</strong>する</li>
    </ul>
  </div>
</div>

<div class="card-highlight" style="margin-top: 15px; text-align: center;">
  <strong>「AIに任せる範囲が増えるほど、何が起きたかを読み解く力が武器になる」</strong>
</div>

---

## これからのおすすめアクション

<div class="card-grid">
  <div class="card">
    <span class="step-num">1</span><strong>もう1回PRを出してみる</strong><br>
    <code>members/あなたのID.md</code> を編集して、趣味や特技を追記してPRを出してみよう！2回目は驚くほどスムーズです。
  </div>
  <div class="card">
    <span class="step-num">2</span><strong>自分のリポジトリを作る</strong><br>
    大学のレポートやプログラミングの学習記録をGitHubで管理してみよう！
  </div>
</div>

<div class="card" style="margin-top: 15px;">
  <span class="step-num">3</span><strong>Cypherのプロジェクトに参加する</strong><br>
  コミュニティの開発プロジェクトで、仲間と一緒にチーム開発を実践しよう！
</div>

---

## 質問・困ったときのサポート

今日の講座が終わった後も、いつでも質問大歓迎です！

<div class="card-grid" style="margin-top: 15px;">
  <div class="card">
    <h3>💬 Cypher Discord</h3>
    <code>#git-lec</code> チャンネルでいつでもメンションしてください！
  </div>
  <div class="card">
    <h3>🐙 GitHub Issues</h3>
    このリポジトリの「Issues」から質問を立てるのも大歓迎！立派な練習になります。
  </div>
</div>

---

<!-- _class: lead -->
<!-- _header: '' -->

<div style="text-align: center; margin-top: 40px;">
  <div class="lead-title" style="font-size: 52px; color: #7ee787;">Happy Hacking! 🌿</div>
  <div class="subtitle" style="font-size: 28px; color: #c9d1d9; margin-top: 20px;">
    GitHubの世界へようこそ！
  </div>

  <div style="color: #8b949e; font-size: 20px; margin-top: 40px;">
    学生AI/データサイエンスコミュニティ <strong>Cypher</strong>
  </div>
</div>
