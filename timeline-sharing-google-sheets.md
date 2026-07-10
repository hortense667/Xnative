## 年表の共有方法（Google Sheets編）

> [!WARNING]
> このガイドの内容は参考情報として残していますが、**Google Sheets（GAS）データソースは現在サポート対象外**です。  
> 既存データは `sheet_to_json_coverter.html` でJSONへ変換し、`ローカルJSON（PC上）` または `GitHub JSON` で運用してください。

この方式は、**少人数のグループで年表を共同管理**するのに向いています。  
編集はスプレッドシート中心で、学習コストが低いのが利点です。

> 注意：このページの作者（=このソフトの作者/メンテナ）は、個別の環境差やGoogleアカウント設定まで踏み込んだ**十分なサポートができない可能性**があります。  
> うまくいかない場合に備え、チーム内にGoogle Sheetsに詳しい人がいる体制（または検証担当）をおすすめします。

### 向いているケース
- 小〜中規模の仲間内で運用したい
- 編集をスプレッドシートで完結させたい
- GitHubの操作に不慣れな人が多い

---

## 基本の流れ

1. Google Sheetsで年表データを管理（**管理者が公開しているテンプレをコピーするのが安全**）  
2. アプリで **Google Sheets（GAS経由）** を選択  
3. **「同期」** でシート内容を読み込む  

---

## 初期設定（最初の1回だけ）

### 0. まず「管理者が公開しているシート」をコピーして使う（推奨・安全）
Google Sheetsを使ったことがない人ほど、**ゼロから新規作成するより、テンプレをコピーして始めるのが安全**です。  
理由は、**タブ（シート）名や列構成が正しくないと、同期が失敗したり、意図しない読み込みになる**ためです。
また、管理者の元シートを直接編集すると、他の人の利用にも影響しうるため、**かならず「コピー」して自分のシートで作業**してください。

- **テンプレ例**: `https://docs.google.com/spreadsheets/d/1cagyMr1rfUm96iefqlLhVA8fhIY5znU75HCtARmF7_Y/edit`

手順（ブラウザ版のGoogle Sheets想定）:
1. 上のテンプレURLを開く（Googleにログインしていない場合はログインします）
2. メニューの **「ファイル」→「コピーを作成」** を選ぶ
3. コピーの名前（年表の名称）と保存場所（マイドライブ等）を決めて作成

> 重要：コピー後は、タブ名（`events` / `genres` / `eraSettings` / `metadata`）を**変更しない**でください。  
> タブの名称などが正しくないといけないため、最初はテンプレのまま運用し、必要なら「内容（行）」だけを編集するのが安全です。

### 0.5. コピー後に「リンクを知っている人は編集可能」に必ず変更する（超重要）
コピーした直後のシートは、**自分だけが編集できる設定**になっていることが多いです。  
このままだと、URLを共有しても**他の人が編集できず運用が止まる**ので、かならず共有設定を変更します。

1. 右上の **「共有」** ボタンを押す
2. 「一般的なアクセス」（または「アクセス権を一般公開/リンク共有」）を開く
3. **「リンクを知っている全員」**（またはチームの運用に合わせた範囲）に変更
4. 権限を **「編集者」** に変更して保存

> 強調：年表の名称を適切に書き換えたら（=コピーの名前を付け直したら）、**かならず**「URLを知っている人は編集可能」に設定してください。  
> ここを忘れるのがいちばん多い“つまずき”です。

### 1. 必要な情報を用意
管理者またはチームで以下を準備します。
- **GAS API URL**（例: `https://script.google.com/macros/s/XXXXX/exec`）
- **Spreadsheet ID** またはシートURL
- タブ名（既定は以下）
  - `events`
  - `genres`
  - `eraSettings`
  - `metadata`

### 2. アプリに設定を入力
1. アプリで「設定」を開く  
2. **データソース**で `Google Sheets（GAS経由）` を選択  
3. 以下を入力して **設定を保存**
   - `GAS API URL`
   - `Spreadsheet ID or Sheet URL`
   - タブ名（基本はテンプレ準拠。**むやみに変更しない**）

### 3. 初回同期
1. **「Google Sheetsと同期」** を押す  
2. シートの内容が年表に反映される

---

## 更新のやり方（ふだんの運用）

### 方法A：シートを直接編集する（基本）
1. Google Sheets上で内容を追加・編集・削除  
2. アプリで **「同期」** を押す  
3. 年表に最新内容が反映される

### 方法B：アプリから編集してシートに貼り付ける
1. 年表画面で項目を編集/追加し **保存**  
2. 対応するシートが自動で開く  
3. 入力した内容はクリップボードに入るので  
   シートに **貼り付け** て確定する

---

## 共有の仕方

### チーム内で共有する
- スプレッドシートを **共有設定** でメンバーに開放  
- 編集権限がある人が更新し、他の人は同期して反映
- 初期設定の「**リンクを知っている人は編集可能**」を採用する場合、**URLを知っている人は誰でも編集できる**状態になります。取り扱い（共有範囲）に注意してください。

### URLで設定を渡す（任意）
以下の形式でURLを共有すると、開くだけで設定が入ります。

```
?datasrc=sheet&sheetApi=GAS_API_URL&sheetId=SPREADSHEET_ID&ev=events&gn=genres&er=eraSettings&md=metadata
```

---

## よくあるつまずき

### 1. 同期で読み込めない
- GAS API URL / Spreadsheet ID の再確認  
- シートの共有権限が適切か確認

### 2. 編集が反映されない
- 変更後に **「同期」** を押しているか確認  
- タブ名が一致しているか確認

---

## English Version

## How to Share a Timeline (Google Sheets)

This workflow is suitable for **small groups** managing a timeline together.  
Editing is spreadsheet-centered and has a low learning curve.

> Note: The author/maintainer of this software may not be able to provide full support for every environment difference or Google account setting.  
> It’s recommended to have someone in your team who is comfortable with Google Sheets (or a dedicated tester).

### Recommended when
- You want to operate within a small-to-mid sized group
- You want to keep editing inside Google Sheets
- Many members are not comfortable with GitHub

---

## Basic flow
1. Manage timeline data in Google Sheets (**safest: copy the maintainer’s template**)  
2. In the app, select **Google Sheets (via GAS)**  
3. Click **Sync** to load the sheet into the app  

---

## Initial setup (one-time)

### 0. Copy the maintainer’s template sheet first (recommended)
If you are new to Google Sheets, starting from scratch is riskier.  
If tab (sheet) names or columns are wrong, sync may fail or load unintended data.

Also, do **not** edit the maintainer’s original sheet directly—always **make a copy** and work on your own sheet.

- **Template example**: `https://docs.google.com/spreadsheets/d/1cagyMr1rfUm96iefqlLhVA8fhIY5znU75HCtARmF7_Y/edit`

Steps (browser version of Google Sheets):
1. Open the template URL (log in if needed)
2. Menu **File → Make a copy**
3. Choose a name (timeline name) and a location (e.g. My Drive)

> Important: After copying, do **not** rename the tabs: `events` / `genres` / `eraSettings` / `metadata`.  
> Keep the template structure and only edit the contents (rows) unless you know what you’re doing.

### 0.5. After copying, change sharing to “Anyone with the link can edit” (very important)
Right after copying, the sheet is often editable **only by you**.  
If you share the URL in that state, others cannot edit and collaboration stops.

1. Click **Share** (top-right)
2. Open “General access” (or link sharing section)
3. Change to **Anyone with the link** (or your team’s desired scope)
4. Set role to **Editor** and save

> This is the most common pitfall. After you rename the copied sheet (timeline name), make sure you set “Anyone with the link can edit”.

### 1. Prepare required information
The maintainer or your team prepares:
- **GAS API URL** (example: `https://script.google.com/macros/s/XXXXX/exec`)
- **Spreadsheet ID** (or the sheet URL)
- Tab names (defaults)
  - `events`
  - `genres`
  - `eraSettings`
  - `metadata`

### 2. Enter settings in the app
1. Open **Settings** in the app  
2. Data source: `Google Sheets (via GAS)`  
3. Enter and **Save**
   - `GAS API URL`
   - `Spreadsheet ID or Sheet URL`
   - Tab names (follow the template; **don’t change casually**)

### 3. First sync
1. Click **Sync with Google Sheets**  
2. The sheet contents are reflected in the timeline

---

## How to update (daily operation)

### Method A: Edit the sheet directly (default)
1. Add / edit / delete rows in Google Sheets  
2. Click **Sync** in the app  
3. The latest contents appear in the timeline

### Method B: Edit in the app and paste into the sheet
1. Edit/add items in the app and **Save**  
2. The corresponding sheet opens automatically  
3. The app copies content to your clipboard → **paste** it into the sheet to confirm

---

## How to share

### Share within the team
- Open the spreadsheet to members via **sharing settings**  
- Editors update the sheet; others sync to reflect changes
- If you choose “Anyone with the link can edit”, anyone who knows the URL can edit. Handle the link carefully.

### Share settings via URL parameters (optional)
If you share a URL in the following format, opening it will prefill settings:

```
?datasrc=sheet&sheetApi=GAS_API_URL&sheetId=SPREADSHEET_ID&ev=events&gn=genres&er=eraSettings&md=metadata
```

---

## Common pitfalls

### 1. Sync cannot load data
- Re-check GAS API URL / Spreadsheet ID  
- Check whether sheet sharing permissions are correct

### 2. Edits are not reflected
- Confirm you clicked **Sync** after editing  
- Confirm tab names match

