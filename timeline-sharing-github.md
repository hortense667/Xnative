## 年表の共有発展方法（GitHub編）

この方式は、年表データをオープンソースとして育てることが目的です。  
操作性が高く、履歴が残り、他者の提案をレビューして統合できます。

### 向いているケース
- 公開年表をみんなで育てたい
- 変更履歴や差分をきちんと残したい
- PR（Pull Request）でレビューしながら統合したい

### 役割イメージ
- **管理者**: 公式の年表リポジトリを管理し、PRをレビュー・統合します
- **貢献者（あなた）**: 自分のフォークで編集し、PRで提案します

---

## はじめての人向け：最短ルート（手取り足取り）

## GitHubが本当にはじめての人向け：アカウント作成〜PRまで（超ていねい版）

この章は「GitHubって何？」「フォーク？PR？」という状態から、ブラウザ操作だけで年表へ貢献できるようにする手順です。  
（※管理者から“公式リポジトリのURL”と“年表ファイルのパス（filePath）”が共有されている前提です）

---

### A. GitHubアカウントの作り方（最初の1回だけ）

1. GitHubのサイトを開く（検索で「GitHub sign up」でもOK）
2. **Sign up**（サインアップ）を押す
3. 指示に従って登録する  
   - メールアドレス
   - パスワード
   - ユーザー名（あとで `owner` に入れる名前）
4. メール認証が来たら、メールの案内に従って認証する

**ポイント**
- ユーザー名（username）は後から変えられますが、まずは短く分かりやすいものがおすすめです

---

### B. リポジトリの作り方（「自分の年表を管理したい人」向け）

※あなたが「公式年表に提案する（フォーク→PR）」だけなら、基本的にこの手順は不要です。  
「自分の年表を自分のリポジトリで管理したい」場合に使います。

1. GitHubにログイン
2. 右上の **＋** → **New repository** をクリック
3. 入力する
   - **Repository name**: 例 `my-timeline`
   - **Public / Private**: 迷ったら Public（共有しやすい）
4. **Create repository** を押す
5. 初期ファイルを置く（例）
   - 公式リポジトリの年表JSONを参考にして、同名のJSONを作る  
   - もしくは、管理者から指示されたテンプレJSONを置く

---

### C. Personal Access Token（classic）の作り方（最初の1回だけ）

**これは“アプリがGitHubへ書き込むための鍵”です。パスワードと同じ扱いで、絶対に他人に渡さないでください。**

1. GitHubにログイン
2. 右上のプロフィール画像 → **Settings**
3. 左メニュー下の **Developer settings**
4. **Personal access tokens** → **Tokens (classic)**
5. **Generate new token** → **Generate new token (classic)**
6. 入力する
   - **Note**: 例 `xnative timeline`
   - **Expiration**: 迷ったら `90 days`（期限が来たら作り直し）
   - **Select scopes**（権限）:
     - Publicリポジトリだけなら **`public_repo`**
     - Privateも扱うなら **`repo`**
7. **Generate token** を押す
8. 表示されたトークン文字列をコピーして安全に保管  
   - 画面を閉じると **二度と同じ文字列は見られません**

**よくあるミス**
- 権限（scope）を付け忘れる → 同期が失敗します
- トークンをどこかに貼って公開する → 事故になります（即失効推奨）

---

### D. フォークのやり方（公式年表に貢献する最初の一歩）

フォークは「公式の年表リポジトリを、自分のGitHubに“コピー”する」ことです。  
あなたはまず自分のコピーに編集を反映し、あとで公式に提案（PR）します。

1. 管理者から共有された **公式リポジトリ** を開く
2. 右上の **Fork** をクリック
3. Owner（フォーク先）を自分にして作成
4. フォークが完了すると、URLがあなたのユーザー名のものになります  
   - 例: `github.com/あなた/リポジトリ名`

---

### E. アプリに設定を入れる（自分のフォークへ同期できる状態にする）

1. アプリで「設定」を開く
2. **データソース**で `GitHub JSON` を選択
3. 以下を入力して **設定を保存**
   - `owner`: あなたのGitHubユーザー名（フォーク先のOwner）
   - `repo`: フォークしたリポジトリ名
   - `filePath`: 管理者から指定された年表JSONのパス（例: `timeline_initial.json`）
   - `accessToken`: さきほど作ったToken（classic）

**ここまでできたら準備OK**です。あとは編集→同期で、あなたのフォークが更新されます。

---

### F. フォーク側へ更新する（編集→同期）

1. 年表上で **追加 / 編集 / 削除** を行う
2. 変更内容が確認できたら **「GitHubと同期」** を押す  
   - これで「あなたのフォーク」に更新が反映されます

---

### G. Pull Request（プルリク）の出し方（公式へ提案する）

PRは「この変更、公式にも取り込んでください」という提案です。

1. GitHubで **自分のフォーク** を開く
2. 画面上部に「Compare & pull request」や「Contribute」ボタンが出ていればそれを押す  
   - 出ていない場合は **Pull requests** タブ → **New pull request**
3. 画面で「どこからどこへ提案するか」を確認  
   - base repository: 公式（管理者のリポジトリ）
   - head repository: あなたのフォーク
4. タイトルと説明を書く（例）
   - 何を追加/修正したか
   - 参考URL（根拠）があれば添付
   - 迷う点があれば「ここ自信ないです」と書いてOK
5. **Create pull request** を押して送信
6. 管理者がレビューして、OKなら公式に取り込まれます（Merge）

---

### 0. 事前に用意するもの
- GitHubアカウント
- パスワードではなく **Personal Access Token（classic）**  
  - Publicリポジトリなら `public_repo` でOK  
  - Privateリポジトリなら `repo` が必要

### 1. 公式リポジトリをフォークする
1. 管理者から共有されたリポジトリURLを開く  
2. 右上の **Fork** ボタンをクリック  
3. 自分のGitHubアカウントにコピーが作成される

### 2. アプリ側の設定（自分のフォークに向ける）
1. アプリで「設定」を開く
2. **データソース**で `GitHub JSON` を選択
3. 以下を入力して **設定を保存**
   - `owner`: あなたのGitHubユーザー名
   - `repo`: フォークしたリポジトリ名
   - `filePath`: 年表JSONのパス  
     - 例: `timeline_initial.json`  
     - 管理者から指定がある場合はその値を使う
   - `accessToken`: 作成したPersonal Access Token

### 3. 年表を編集する
1. 年表上で **追加 / 編集 / 削除** を行う
2. 変更内容が確認できたら **「GitHubと同期」** を押す  
   - これで「あなたのフォーク」に更新が反映される

### 4. Pull Request（PR）を作成する
1. GitHubで自分のフォークを開く
2. `Contribute` → `Open pull request` を選ぶ
3. 変更内容・意図を文章で書いて送信
4. 管理者がレビューし、問題なければ統合される

---

## もっと安全に進めるコツ

### 変更を小さく分ける
- 1回のPRは小さめに（例: 10〜30件程度）
- 目的が明確な単位にするとレビューが早い

### 競合を避ける
- 編集前に最新データを取り込む  
  - アプリの **「GitHubと同期」** を先に押す
- 競合が出たら、管理者に相談するのが早い

---

## よくあるつまずき

### 1. 変更が反映されない
- `owner` / `repo` / `filePath` を再確認  
- トークンに必要な権限があるか確認

### 2. 間違った年表を更新してしまう
- **URLのパラメータ**や設定の値を必ず確認  
- 編集前に「タイトル」や「説明」も見ると安全

### 3. トークンが無効
- 期限切れの可能性があるので再発行
- トークンは **絶対に公開しない**

---

## 補足：トークンを使わない編集方法

トークンがない場合、アプリの「同期」は **CSVのダウンロード** になります。  
このCSVを管理者に渡して統合してもらう運用も可能です。  
出力名は `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{件数}items.csv` 形式です。

---

## English Version

## How to Share & Grow a Timeline (GitHub)

This workflow is for growing timeline data as an open-source project.  
You get good operability, a clear change history, and a reviewable collaboration process via Pull Requests.

### Recommended when
- You want to grow a public timeline together
- You want to keep proper history and diffs
- You want to merge contributions through PR reviews

### Roles
- **Maintainer**: manages the official timeline repository and reviews/merges PRs
- **Contributor (you)**: edits on your fork and proposes changes via PR

---

## For first-timers: Browser-only, step-by-step (very detailed)

This section is written for people starting from “What is GitHub?” and “What is a fork/PR?”.  
Assumption: the maintainer shared the **official repository URL** and the **timeline JSON file path (`filePath`)**.

---

### A. Create a GitHub account (one-time)
1. Open GitHub (search “GitHub sign up” is fine)
2. Click **Sign up**
3. Register following the instructions
   - Email address
   - Password
   - Username (this is what you will set as `owner` later)
4. Complete email verification

**Tip**
- You can change your username later, but starting with something short and clear is recommended.

---

### B. Create a repository (only if you manage your own timeline)
If you only contribute to the official timeline (fork → PR), you usually do **not** need this.  
Use this when you want to host/manage your own timeline in your own repository.

1. Log in to GitHub
2. Top-right **+** → **New repository**
3. Fill in
   - **Repository name**: e.g. `my-timeline`
   - **Public / Private**: choose Public if unsure
4. Click **Create repository**
5. Add the initial file (examples)
   - Create a timeline JSON based on the official repository’s format
   - Or place a template JSON the maintainer provided

---

### C. Create a Personal Access Token (classic) (one-time)

**This is the “key” that lets the app write to GitHub. Treat it like a password and never share it.**

1. Log in to GitHub
2. Profile icon → **Settings**
3. Left menu → **Developer settings**
4. **Personal access tokens** → **Tokens (classic)**
5. **Generate new token** → **Generate new token (classic)**
6. Set
   - **Note**: e.g. `xnative timeline`
   - **Expiration**: e.g. `90 days` (recreate when expired)
   - **Scopes**
     - Public repos only: **`public_repo`**
     - Private repos too: **`repo`**
7. Click **Generate token**
8. Copy and store the token safely
   - After you leave the page, you cannot see the same token string again.

**Common mistakes**
- Forgetting scopes → sync fails
- Pasting the token somewhere public → security incident (revoke immediately)

---

### D. Fork the official repository (first step to contribute)
A fork is your personal “copy” of the official repository on GitHub.  
You edit your fork first, then propose changes back to the official repo via a PR.

1. Open the **official repository** shared by the maintainer
2. Click **Fork**
3. Set the fork **Owner** to yourself and create it
4. After completion, the URL becomes yours
   - Example: `github.com/your-username/repository-name`

---

### E. Configure the app (point it to your fork)
1. Open **Settings** in the app
2. Choose **Data source**: `GitHub JSON`
3. Enter and **Save**
   - `owner`: your GitHub username (fork owner)
   - `repo`: your fork repository name
   - `filePath`: timeline JSON path specified by the maintainer (e.g. `timeline_initial.json`)
   - `accessToken`: the token you created above

Once this is set, you can edit and sync to update your fork.

---

### F. Update your fork (edit → sync)
1. Add / edit / delete items in the timeline
2. When ready, click **Sync with GitHub**
   - This updates **your fork**.

---

### G. Create a Pull Request (propose changes to the official repo)
A PR is a proposal: “Please merge these changes into the official timeline.”

1. Open **your fork** on GitHub
2. If you see **Compare & pull request** (or **Contribute**), click it  
   - Otherwise: **Pull requests** tab → **New pull request**
3. Confirm the direction
   - base repository: official repository (maintainer)
   - head repository: your fork
4. Write title/description (examples)
   - what you changed/added
   - reference URLs (sources), if any
   - if unsure, you can say “I’m not fully confident about this part”
5. Click **Create pull request**
6. The maintainer reviews it and merges if accepted

---

## Short “minimum route” checklist
### 0. Prepare
- GitHub account
- **Personal Access Token (classic)** (not your password)
  - Public repo: `public_repo`
  - Private repo: `repo`

### 1. Fork the official repository
1. Open the official repository URL
2. Click **Fork**
3. A copy is created under your GitHub account

### 2. App settings (point to your fork)
1. Open **Settings**
2. Data source: `GitHub JSON`
3. Save `owner`, `repo`, `filePath`, `accessToken`

### 3. Edit
1. Add / edit / delete items
2. Click **Sync with GitHub** to update your fork

### 4. Create PR
1. Open your fork on GitHub
2. `Contribute` → `Open pull request`
3. Describe what/why and submit
4. Maintainer reviews and merges

---

## Safer collaboration tips
### Keep PRs small
- Make each PR smaller (e.g. 10–30 items)
- Clear purpose → faster reviews

### Avoid conflicts
- Before editing, pull the latest data
  - Click **Sync with GitHub** first
- If you hit conflicts, ask the maintainer early

---

## Common pitfalls
### 1. Changes are not reflected
- Re-check `owner` / `repo` / `filePath`
- Check token scopes

### 2. You updated the wrong timeline
- Always verify the **URL parameters** and settings
- Before editing, also check the timeline title/description to be safe

### 3. Token is invalid
- It may be expired → create a new one
- Never publish tokens

---

## Note: editing without a token
Without a token, the app “Sync” becomes **CSV download**.  
You can give that CSV to the maintainer and ask them to integrate it.  
Filename format: `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{count}items.csv`.
