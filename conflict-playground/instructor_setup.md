# 講師用：コンフリクト教材の仕込み手順

**受講者は読む必要はありません。** 講師が講座前（または番外編1の直前）に実施します。

対応する受講者向け資料 → [docs/05_extra_conflict_revert.md](../docs/05_extra_conflict_revert.md)

---

## 仕組み

受講者にコンフリクトを起こさせるには、**`main` 側に「同じ行を変更したコミット」が既に存在している**必要があります。

```
main:      A ─── B ─── C(講師が同じ行を変更)
                  \
受講者:            └─── D(受講者が同じ行を変更)

受講者が git pull origin main すると → C と D が衝突 → 💥 CONFLICT
```

つまり、**講師が先に `guestbook.md` の「今日のひとこと」の行を書き換えて `main` にmergeしておく**だけです。

---

## 仕込み手順（所要2分）

### 1. リポジトリを最新にする

```bash
cd ~/git-lec
git switch main
git pull
```

**期待する出力**
```
Already up to date.
```

### 2. 仕込み用ブランチを切る

```bash
git switch -c chore/conflict-seed-$(date +%Y%m%d)
```

**期待する出力**
```
Switched to a new branch 'chore/conflict-seed-20260814'
```

> Windows の Git Bash でも `date +%Y%m%d` は使えます。
> 手打ちしたい場合は `git switch -c chore/conflict-seed-20260814` のように直接書いてください。

### 3. 衝突対象の行を書き換える

```bash
code conflict-playground/guestbook.md
```

以下の行を探して：

```markdown
今日のひとこと: （ここを書き換えてください）
```

**「講師側の内容」に書き換えます。** 受講者が書きそうな内容と**明確に違う**方が、
diffを見せる時に分かりやすいです。

推奨する文言：

```markdown
今日のひとこと: コンフリクトは事故ではなく、Gitの安全装置です
```

> 💡 **この行だけを変更してください。** 他の行を変えると、衝突箇所が増えて説明が複雑になります。

保存します。

### 4. 変更内容を確認する

```bash
git diff
```

**期待する出力**
```diff
--- a/conflict-playground/guestbook.md
+++ b/conflict-playground/guestbook.md
@@ -12,7 +12,7 @@
 <!-- CONFLICT-LINE-START: ... -->
-今日のひとこと: （ここを書き換えてください）
+今日のひとこと: コンフリクトは事故ではなく、Gitの安全装置です
 <!-- CONFLICT-LINE-END -->
```

**1行だけの変更**になっていることを確認してください。

### 5. commit → push

```bash
git add conflict-playground/guestbook.md
git commit -m "chore: 衝突練習用に guestbook のひとことを更新"
git push -u origin chore/conflict-seed-20260814
```

### 6. PRを作ってmergeする

```bash
gh pr create --title "chore: 衝突練習用に guestbook のひとことを更新" \
  --body "番外編1（コンフリクト解消）の教材仕込みです。受講者はこの変更と衝突します。" \
  --base main
```

```bash
gh pr merge --merge --delete-branch
```

> ブラウザで作ってmergeしても構いません。

### 7. 仕込みが効いているか確認する

```bash
git switch main
git pull
git log --oneline -3
```

**期待する出力**
```
9f8e7d6 (HEAD -> main, origin/main) Merge pull request #14 from guousuides/chore/conflict-seed-20260814
3a4b5c6 chore: 衝突練習用に guestbook のひとことを更新
1a2b3c4 docs: ハンズオン資料を追加
```

**`main` に自分の変更が入っていればOKです。**

---

## リハーサル：本当に衝突するか確認する

**本番前に、受講者役として1回試すことを強く推奨します。**

```bash
git switch -c test/conflict-rehearsal
```

`guestbook.md` の同じ行を、**講師とは違う内容**に書き換えて：

```bash
git add conflict-playground/guestbook.md
git commit -m "test: リハーサル"
git pull origin main
```

**期待する出力**
```
CONFLICT (content): Merge conflict in conflict-playground/guestbook.md
Automatic merge failed; fix conflicts and then commit the result.
```

**`CONFLICT` が出れば仕込み成功です。**

後片付け：

```bash
git merge --abort
git switch main
git branch -D test/conflict-rehearsal
```

---

## ⚠️ 注意点

### 受講者が `git pull` を先にしてしまうと衝突しない

受講者が**編集する前に** `git pull` して講師の変更を取り込んでしまうと、衝突が起きません。

**受講者向け資料（[docs/05](../docs/05_extra_conflict_revert.md)）の STEP 1 では
「`main` を pull してからブランチを切る」順序にしてあります。**

これは意図的です。受講者は「講師の最新の状態」から作業を始め、
**その後に講師がもう1回変更を入れる**、という想定です。

そのため：

> **仕込み（この手順）は、受講者が STEP 1 の `git pull` を実行した「後」に行ってください。**
>
> つまり **番外編1のセッション開始直前**、受講者に STEP 1〜3 を実行させてから、
> 講師が手順1〜6を実施するのが最も確実です。

**タイムライン**

| 時刻 | 講師 | 受講者 |
|---|---|---|
| T+0 | 「まず main を pull してブランチを切ってください」 | STEP 1〜3 を実行 |
| T+1分 | **この手順1〜6を実施**（2分で終わる） | STEP 2 のファイル編集をしている |
| T+3分 | 「では `git pull origin main` してください」 | STEP 4 → 💥 CONFLICT |

### 事前に仕込んでおきたい場合

セッション直前の仕込みが不安であれば、**前日までに仕込んでおき、
受講者に STEP 1 の `git pull` を実行させない**という運用も可能です。

その場合、[docs/05](../docs/05_extra_conflict_revert.md) の STEP 1 の
`git pull` を飛ばすようアナウンスしてください。
（clone直後の受講者は、そもそも仕込み後の状態を持っていないため衝突します）

**どちらの運用にするか、事前に決めておいてください。**

### 複数回の講座で使い回す場合

`guestbook.md` の「今日のひとこと」の行は、**毎回リセットする必要があります。**

```bash
git switch main
git pull
git switch -c chore/reset-guestbook
```

`guestbook.md` の該当行を、初期状態に戻します：

```markdown
今日のひとこと: （ここを書き換えてください）
```

```bash
git add conflict-playground/guestbook.md
git commit -m "chore: guestbook を初期状態にリセット"
git push -u origin chore/reset-guestbook
gh pr create --fill && gh pr merge --merge --delete-branch
```

---

## トラブル時のリカバリ

| 症状 | 原因 | 対処 |
|---|---|---|
| 受講者に `CONFLICT` が出ない | 仕込みのタイミングが早すぎた（受講者が既に取り込み済み） | 講師がもう一度、別の内容で手順1〜6を実施 |
| 受講者が `Already up to date.` と言う | `git pull origin main` ではなく `git pull` を実行している | ブランチが違う。`git pull origin main` を再実行させる |
| 受講者が記号を消し忘れてcommitした | よくあります | `git revert` で戻すか、そのまま直してもう1コミットさせる（実務でもこう直します） |
| 全体が収拾つかなくなった | — | 全員に `git merge --abort` → `git switch main` → `git pull` をアナウンス。**何も失われません** |

---

**関連** → [facilitator_guide.md](../facilitator_guide.md)（時間配分・トラブルQ&A）
