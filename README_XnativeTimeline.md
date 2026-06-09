# XnativeTimeline 1.0 / エックスネイティブタイムライン 1.0

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。
This document includes both a Japanese and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリは **XnativeTimeline 用のデータ**（JSON）のみを収録しています。アプリ本体のコードは別管理です。関連ソフトウェアであるJSONのファイル変換ツールのJavaScriptは収録しています。

### 最初に（おすすめの始め方）
- まずは「既にある年表を体験したい」人は、メイン年表に GitHub JSON を使うのが簡単です（owner/repo/filePath をURLで指定）。
- 「自分で年表を作ってみたい」人は、Google Sheets（GAS経由）がおすすめです。スプレッドシートを用意してURLに `sheetApi/sheetId` 等を載せれば、すぐ共有できます。
- 共有・共同編集の詳しい手順は、以下のドキュメントを参照してください。
  - GitHubで育てる（オープンな共同編集）: `timeline-sharing-github.md`
  - Google Sheetsで運用する（少人数・低学習コスト）: `timeline-sharing-google-sheets.md`
- Google Sheetsで管理していた年表を、GitHubで管理する **JSON形式** に移行したい場合は、変換ツール `sheet_to_json_coverter.html`（Sheets→JSON変換）を用意しています。逆に、GitHubで管理していた年表をGoogle Sheetsで管理する **JSON形式** に移行したい場合は、そのためのtsvファイルに変換ツール `json_to_tsv_coverter.html`（JSON→tsv変換）を用意しています。

### 主な機能

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。さまざまな分野の歴史を、それぞれの年表形式で管理し、個人の体験と照らし合わせることができます。分野ごとの年表を組み合わせて見ることができることを特徴としています。

- **年表の視覚的表示**: 0年代から2050年代までの年表を縦スクロールで表示（デフォルト）
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **AI検索**: ヘッダーの「AI検索」から自然文検索（現在選択中ジャンルのみ）
- **データ連携/リロード**:
  - GitHub JSON との連携（読み込み・リロード）
  - Google Sheets（GAS経由）からの読み込みに対応（下記「データソースとURLパラメーター」参照）
- **CSV対応**: データの一括インポート
- **参照年表機能**: 複数の年表データを同時に表示・比較可能
- **フキダシ（吹き出し）**: 右側エリアをShift+クリックして注釈を配置。三角テールはクリック位置を先端にし、バブルの辺から自然に接続。スタイル（色・文字サイズ・太字）変更やドラッグ移動、スナップショット保存/復元に対応。テイルの表示/非表示切り替え、画像表示機能（#URL形式）、リンク（@URL形式＝末尾に空白1文字が必要）、改行対応。
- **範囲ガイド（コの字形）**:右側エリアでCtrl+Shift+クリックで、範囲ガイド（コの字形）を設置（〇年～〇年の範囲の視覚ガイド用）。縦棒の中央をドラッグで移動。縦棒の右側ドラッグで太さ変更。上下ドラッグで高さ変更。上/下の三角足をドラッグして左右に伸縮（上下連動）。右クリックで色設定、Rで反転、△で足の表示/非表示。
- **ホバー表示文字サイズ設定**: ラベル表示エリアにマウスをホバーした際の文字サイズ（年、ラベル名、重要度、注釈）を個別に設定可能。
- **オリジナルの年表作成**： GitHub、およびGoogle Sheetsを使って誰でもオリジナル年表を作って運用することができます。

### データセット

現在用意されているデータセットの例：

1. **timeline_popculture_02.json** - 日本のポップカルチャー年表
   - アニメ、マンガ、ゲーム、音楽などのポップカルチャーイベント
   
2. **timeline_digital_02.json** - デジタルの歴史年表
   - コンピュータ、インターネット、デジタル技術の歴史
   
3. **timeline_background_02.json** - 時代背景の歴史年表
   - 参照年表として他の年表と併用するための年表
   
4. **timeline_ai_02.json** - AIの歴史年表
   - AIの歴史
   
5. **timeline_akihabara_02.json** - 秋葉原の歴史年表
   - 秋葉原の歴史
   
6. **timeline_gadget_02.json** - デジタルガジェットの歴史年表
   - デジタルガジェットの歴史
   
※ユーザーは独自のデータセットを作ることができ公開することもできます。「自分で新たに年表を作りたい人へ」の項目をご覧ください。


### 基本的な使い方

#### 動画による説明
　https://youtu.be/Ymsez9vMJa4

#### 年表ソフトの起動

年表データの閲覧ソフトウェアは、以下のいずれかから起動することができます。

- Cloudflare ： https://xnative.pages.dev/?editmode=ON
- Netlify ： https://xnative.netlify.app/?editmode=ON

※適切な年表が設定されないとエラーとなります。すぐに触りたい人は以下のチュートリアルを開いてみてください。

- サンプル
　https://xnative.pages.dev/?editmode=ON&snapshot=snapshot-tutorial.json
  - ※ `snapshot` は GitHub の `owner/repo` の `main/data/` から読み込みます（Cloudflare/Netlify の配置先ではありません）。


#### 年表の表示と操作
- 0年代から2050年代まで縦スクロールで閲覧（デフォルト）
- 左側のカラムに年とイベントが表示
- 右側のエリアでドラッグ操作が可能

#### 項目の編集
- ジャンル表記のルール：`[]` は AND 条件、`{}` は「時代区分（genre_era=true）」を意味します。
- 「時代区分設定」画面に「すべての時代区分を登録」ボタンを追加。メイン年表のうち genre_era=true のジャンルが付いた項目を一括登録できます（登録時に表示・塗りON）。
- 起動/リロード時は参照年表をクリアした状態で開始します（参照年表は読み取り専用）。

注意（重要）:
- 編集モーダルは縦に長い場合があります。必ず下部にある「保存」ボタンを押して反映してください（保存しないと内容は反映されません）。
- 編集モーダルと詳細一覧は、ヘッダー（上部の何もない領域）をドラッグして位置を移動できます。
- 右側のグラフエリアをクリックすると、開いている詳細一覧/編集モーダルが閉じます。
- 項目をクリックして編集モーダルを開く
- ラベル、年、ジャンル、重要度、URL、注釈を編集可能
- 詳細一覧で項目の追加・削除・並び替え

#### 検索とフィルター
- 検索ボックスでラベルやジャンルを検索
- ジャンル選択で表示項目を絞り込み
- 重要度別のフィルター機能
- 検索結果の青い項目にマウスオーバーでウェブ画面を開く（URLが設定されている場合）
- 検索結果の青い項目をクリックで注釈をポップアップ表示
- 検索結果の青い項目をダブルクリックで編集モーダルを開く（editmode=ON の場合のみ）
- 検索ボックスに「*」を入力すると、選択されている分野のすべての項目を表示

#### AI検索
- ヘッダーの「AI検索」ボタンから自然文で検索できます（例: 「鉄腕アトムと同じ作者の作品をリストアップして」）。
- 検索対象は **現在選択中ジャンルのみ** です。`主年表限` がONの場合、参照年表は対象外です。
- 入力欄では上下キーで過去の入力履歴を呼び出せます。
- 結果は通常検索と同様に青いラベルとして表示されます。
- 入力量が設定上限を超える場合は、API呼び出し前にエラー表示します。
- モデル/上限は「設定」画面の「AI検索設定」で変更できます（初期値: `gemini-2.5-flash-lite`）。

#### フキダシ（吹き出し）
- Shift+クリックで右側エリアにフキダシを作成
- クリック点＝三角先端。接合位置は辺の中央±1/3範囲で自動調整（角丸は避ける）
- バブル／テールはドラッグ可能。右クリックで色テーマ・A-/A+・B（太字）・テイル切り替えを設定（表示モード）
- 削除アイコンでバブル・三角・継ぎ目カバーも一括削除
- 余白は左右対称（上下13px／左右16px）
- テイルの表示/非表示切り替え
- 画像表示（#URL形式）

#### 範囲ガイド（コの字形）
- Ctrl+Shift+右クリックで、右側エリアに範囲ガイド（コの字形）を設置
- 縦棒の中央ドラッグで移動、縦棒右側ドラッグで太さ変更、上下ドラッグで高さ変更
- 上/下の三角足をドラッグして左右に伸縮（上下連動）
- 右クリックで色設定、Rで反転、△で足の表示/非表示

#### データの管理
- **ロード**: CSV/TSVファイルからデータを一括インポート（設定 → データ管理）
- **リロード（メイン年表）**:
  - GitHub JSON: 「リロード」で最新データを再読み込み
  - Google Sheets（GAS）: 「リロード」でシートから再読み込み（表示更新）
- **編集の反映（GitHub JSON）**:
  - アクセストークンあり: 「保存」「削除」「閉じる（並び替え）」でGitHubのJSONに反映
  - アクセストークンなし: 変更内容はCSVとして書き出し（GitHubには反映されません）
- **参照年表**: 複数の年表データを同時に表示・比較（読み取り専用）
- **スナップショット**: 現在の状態（データ、フキダシ、設定、開いているウェブ画面パネル）を保存・復元。気軽に自分の年表を作り始めることができます
- **Amazon画像表示**: AmazonのURLの後に「&」を付けて画像URLを追加することで、ウェブ画面に表紙画像が表示されます

### 年表の活用例

1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグ
2. **生年を合わせる**: 水色の斜め線の左端の丸を生年に合わせる
3. **年齢表示**: 上部に年齢が表示される

### 自分で新たに年表を作りたい人へ

**GitHubユーザーなら誰でも管理者になれます！**

GitHubアカウントを持つユーザーが自分のリポジトリで年表データを管理できる分散型システムです。独自の年表を作成・管理したい場合は、[ユーザーガイド](users_guide.md)をご覧ください。

**気軽に始める方法**:
1. 既存のデータをロードして編集
2. スナップショット保存で現在の状態を保存
3. スナップショット復元でいつでも元の状態に戻す
4. 気に入った状態になったらGitHubに反映して公開

### データソースとURLパラメーター（共有用）

第三者に設定不要で見せたい場合は、URLにパラメーターを付与して共有することができます。設定画面の内容は適宜URLに反映されるのでそれをコピーすることで第三者に渡すことができます。

- メイン年表（GitHub JSON）
  - datasrc=github
  - owner, repo, filePath
  - 例: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json`

- メイン年表（Google Sheets / GAS）
  - datasrc=sheet
  - sheetApi, sheetId, ev, gn, er, md（タブ名）
  - 例:  
    `?datasrc=sheet&sheetApi=https://script.google.com/macros/s/XXX/exec&sheetId=1AbC...&ev=events&gn=genres&er=eraSettings&md=metadata`

- 参照年表（GitHub/Sheets 混在可）
  - refTimelines=JSON配列（URLエンコード）
  - 各要素（GitHub型）: `{ "sourceType":"github", "owner":"user", "repo":"repo", "filePath":"file.json", "minImportance":2 }`
  - 各要素（Sheets型）: `{ "sourceType":"sheet", "gasApi":"https://.../exec", "sheetId":"xxxxx", "ev":"events", "gn":"genres", "er":"eraSettings", "md":"metadata", "minImportance":2 }`
  - 例（エンコード前）:
    ```
    refTimelines=[{"sourceType":"github","owner":"user1","repo":"repo1","filePath":"file1.json","minImportance":2},
                  {"sourceType":"sheet","gasApi":"https://script.google.com/macros/s/XXX/exec","sheetId":"1AbC...","ev":"events","gn":"genres","er":"eraSettings","md":"metadata","minImportance":3}]
    ```

- スナップショット復元（GitHub data フォルダ）
  - `snapshot` または `snapshotpath` に JSON ファイル名（`data/` 相対）を指定
  - 既定の取得先: メイン年表と同じ `owner/repo`
  - 別リポジトリ指定: `snapshotowner`, `snapshotrepo`
  - Cloudflare Pages / Netlify に同名ファイルを置いても参照されません（`main/data/` が参照先）
  - 例（同一リポジトリ）: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshot=snapshot-tutorial.json`
  - 例（別リポジトリ）: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshotowner=foo&snapshotrepo=bar&snapshotpath=snapshots/demo.json`
  - `snapshotURL` / `snapshotUrl` / `data` は廃止

メイン年表の種別に応じて、不要なパラメーター（GitHub系/Sheets系）はURLから自動的に取り除かれます（設定→「設定を保存」時に付与/整理）。

#### 補足：Google Sheets → GitHub JSON への移行
Google Sheetsで運用していた年表を、GitHub上で管理・共同編集できるJSON（アプリのGitHubデータ形式）へ変換するために、`sheet_to_json_coverter.html` を同梱しています。

### Google Sheets（GAS）で用意するシート構成

Google Sheetsによる年表の例

　https://docs.google.com/spreadsheets/d/1cagyMr1rfUm96iefqlLhVA8fhIY5znU75HCtARmF7_Y/edit

タブ名は基本値 `events / genres / eraSettings / metadata` を推奨（URLで変更可能）。

- events（年表本体）
  - 必須ヘッダー: `label, label_en, startYear`
  - 任意ヘッダー: `endYear, genre, imp, url, url_en, note, note_en, image`
  - 値の形式:
    - genre: パイプ区切り（例: `ANI|JAPAN|TVP`）
    - imp: 1～5 の整数
    - url/url_en: 単一またはパイプ区切りで複数可
  - フロント側が保存時にTSVをクリップボードへ置くときの並び（参考）:
    `label  label_en  startYear  endYear  genre(pipe)  imp  url  url_en  note  note_en  image`

- genres（ジャンル定義）
  - ヘッダー: `code, label, label_en, conjunction`
  - `conjunction` は AND結合に使う補助（true/false）。ジャンルコードは events.genre と対応します。

- eraSettings（時代区分）
  - ヘッダー: `name, startYear, endYear, color, opacity, enabled, fillEnabled`
  - `enabled`/`fillEnabled`: true/false。視覚背景の表示と塗りのオン/オフ。

- metadata（メタ情報）
  - ヘッダー（例）:
    - タイトル/説明: `title_ja, title_en, description_ja, description_en`
    - 作成者/連絡先: `initialCreator, contributors(パイプ), contact_admin_name, contact_admin_email, contact_admin_x, contact_admin_org`
    - その他: `createdAt, version, language(パイプ), copyright, license, licenseUrl, notes`

### Google Sheets（GAS）モード時の動作
- 詳細一覧の「鉛筆」: 編集モーダルを開き、保存時にTSV形式をクリップボードへコピー → 対応するSheetsが自動的に開くので、当該項目のセントウコラムで自身でクリップボードからの貼り付けを行ってください。
- 詳細一覧の「ゴミ箱」: ダイアログや画面上削除は行わず、該当セル位置に移動（シートを開く）手作業で当該行を削除してください。
- 左カラムの空き領域クリック: その年に近い行のセルへ移動（新規追加用）手作業で当該行を追加してください。
- 「リロード」: GAS APIから再読み込みして画面を更新

### 編集可否（editmode）
- URLに `?editmode=ON` がない場合:
  - 詳細一覧の「鉛筆」「ゴミ箱」「追加」はグレーアウト（操作不可）
  - 左カラム空白クリックでも編集モーダルは開かない（Sheetsモードでも移動しない）

### 設定画面の参照年表UI（GitHub/Sheets 両対応）
- 「参照年表（GitHub）」と「参照年表（Sheets）」を分けて入力
- それぞれに「参照年表を追加」ボタン
- 保存すると `refTimelines` にJSONとして保存され、URLにも `refTimelines` が付与されます

### 免責事項
- このソフトによる年表の内容については、一切保証いたしません。
ｰ このソフトの使用によって利用者が被った損害については、一切保証いたしません。
- このソフトウェアに不具合があった場合もすみやかに対応できるとは限りません。デモンストレーションなどで必ず動作させたい場合は、JavaScriptで動作していますので、自身のコンピューター上でオープンしたままであれば動作します。

### 技術仕様

- **フロントエンド**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式**: JSON, CSV, TSV
- **外部連携**: GitHub API
- **外部連携（追加）**: Google Apps Script（GAS）Web API（Google Sheets読み込み）
- **外部連携（追加）**: `/api/ai-search`（Cloudflare Pages Functions / Netlify Functions）
- **対応ブラウザ**: Modern browsers (Chrome, Firefox, Safari, Edge)

## ライセンス
- データ: 原則 **CC BY 4.0**。一部の短い説明文がソースの共有条件に該当すると判断した場合、当該項目のみ **CC BY-SA 4.0** として `CREDIT.md` に明記します。
- 詳細: `LICENSE_DATA.txt`, `CREDIT.md` を参照

## サポート / Support
問題やご要望、**年表の内容訂正**は GitHub Issues へ:  
https://github.com/hortense667/xnative/issues

Use these labels:
- `data-correction`（内容訂正）
- `feature-request`（機能提案）
- `bug`（不具合）

セキュリティ上の懸念は `SECURITY.md` をご確認ください。

---

## English Version

This repository contains only **data (JSON) for XnativeTimeline**. The application code is managed separately. JavaScript utilities for converting JSON/TSV/Sheets data are included.

### First Steps (recommended)
- Want to try existing timelines? Use the main timeline from GitHub JSON (specify owner/repo/filePath via URL).
- Want to build your own? Google Sheets (via GAS) is the easiest: prepare a sheet and pass `sheetApi/sheetId` in the URL to share quickly.
- Detailed sharing/operation guides:
  - Grow with GitHub (open collaboration): `timeline-sharing-github.md`
  - Operate with Google Sheets (small teams/low learning cost): `timeline-sharing-google-sheets.md`
- Converters:
  - Sheets → JSON for GitHub: `sheet_to_json_coverter.html`
  - JSON → TSV for Sheets: `json_to_tsv_coverter.html`

### Main Features
- **Visual timeline**: Vertical view from the 0s to the 2050s (default)
- **Multilingual**: Japanese / English toggle
- **Editing**: Add / edit / delete / reorder items
- **Search**: By label or genre
- **AI search**: Natural-language search from the `AI Search` button (current selected genres only)
- **Reload / integrations**:
  - GitHub JSON load & reload
  - Google Sheets (via GAS) load (see “Data source and URL parameters”)
- **CSV/TSV**: Bulk import
- **Reference timelines**: Show and compare multiple timelines together
- **Speech bubbles**: Shift+click in the right area to add. Tail connects naturally from edge to click point. Style (color/font size/bold) change, drag move, snapshot save/restore, tail toggle, image display (#URL), link (@URL + trailing space), line breaks.
- **Range guide (bracket)**: Ctrl+Shift+click in right area to place a bracket for visualizing year ranges. Drag center to move, right side for thickness, top/bottom for height, triangle feet drag to stretch, right-click for colors, `R` to reverse, △ to show/hide feet.
- **Hover font sizes**: Set per field (year/label/importance/note).
- **Anyone with GitHub can admin** their own timeline data (distributed model).

### Datasets (examples)
1. **timeline_popculture_02.json** – Japanese pop-culture history (anime/manga/games/music, etc.)
2. **timeline_digital_02.json** – Digital history (computers, internet, tech)
3. **timeline_background_02.json** – Background history (for overlay/reference)
4. **timeline_ai_02.json** – AI history
5. **timeline_akihabara_02.json** – Akihabara history
6. **timeline_gadget_02.json** – Digital gadget history
You can create and publish your own datasets. See “Create your own timeline.”

### Basic Usage
#### Video
https://youtu.be/Ymsez9vMJa4

#### Launch the app
- Cloudflare: https://xnative.pages.dev/?editmode=ON
- Netlify: https://xnative.netlify.app/?editmode=ON
- Quick try: tutorial https://xnative.pages.dev/?snapshot=snapshot-tutorial.json
  - Note: `snapshot` is loaded from GitHub `owner/repo` `main/data/` (not from Cloudflare/Netlify deployed files).

#### Viewing & interaction
- Vertical scroll 0s–2050s (default)
- Years/events on the left, drag actions on the right

#### Editing
- Genre notation: `[]` = AND condition, `{}` = era (genre_era=true).
- “Era settings” has “Register all eras” to bulk-register main-timeline items whose genres have genre_era=true (display/fill ON).
- On startup/reload, reference timelines are cleared (read-only).
- Important:
  - Edit modal can be tall—always click “Save” at bottom.
  - Drag headers of modal/detail list to move them.
  - Clicking the right graph area closes open modals/detail lists.

#### Search & filter
- Search box for labels/genres; `*` shows all in selected fields.
- Filter by genre and importance.
- Hover blue search hits to open web preview (if URL set); click for note popup; double-click to open edit modal (edit mode only).

#### AI Search
- Run natural-language search from the `AI Search` button in the header.
- Scope is **current selected genres only**. When `Main only` is ON, reference timelines are excluded.
- Use Up/Down keys in the input to recall query history.
- Results are shown as blue labels (same style as normal search).
- If estimated input exceeds configured limits, an error is shown before API call.
- Model/token limits are configurable in Settings → AI Search (default: `gemini-2.5-flash-lite`).

#### Speech bubbles
- Shift+click in right area to create.
- Click point = tail tip; connection auto-adjusts near edge center (avoids rounded corners).
- Drag bubble/tail; right-click (view mode) for color themes, A-/A+, B (bold), tail toggle.
- Delete icon removes bubble, triangle, seam.
- Symmetric padding (13px vertical / 16px horizontal).
- Supports tail toggle, images (#URL), links (@URL + space), line breaks.

#### Range guide (bracket)
- Ctrl+Shift+right-click in right area to create.
- Drag center to move; right side to change thickness; top/bottom to change height.
- Drag triangle feet to stretch (linked); right-click for colors; `R` to reverse; △ to show/hide feet.

#### Data management
- **Load**: Bulk import CSV/TSV (Settings → Data management).
- **Reload (main timeline)**:
  - GitHub JSON: “Reload” fetches the latest data.
  - Google Sheets (GAS): “Reload” fetches from the sheet (display refresh).
- **Apply edits (GitHub JSON)**:
  - With access token: “Save”, “Delete”, “Close (reorder)” update GitHub JSON.
  - Without token: changes are exported as CSV (not reflected to GitHub).
- **Reference timelines**: multiple timelines shown/read-only.
- **Snapshot**: Save/restore state (data, speech bubbles, settings, open web preview panels) for easy personal timeline creation.
- **Amazon images**: Append an image URL after `&` on an Amazon URL to show a cover image in web preview.

### Timeline usage examples
1) Align event years: drag blue circles up/down in drag lane  
2) Align birth year: align circle at left end of blue diagonal to birth year  
3) Age display: shown at top  

### Create your own timeline
**Any GitHub user can become an administrator!**  
Distributed system: manage your data in your own repo. See [User Guide](users_guide.md).

**Easy start**
1. Load existing data and edit  
2. Save a snapshot  
3. Restore anytime with snapshot  
4. Publish by reflecting to GitHub  

### Data source & URL parameters (for sharing)
- Main timeline (GitHub JSON): `datasrc=github`, `owner`, `repo`, `filePath`  
  Example: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json`
- Main timeline (Google Sheets / GAS): `datasrc=sheet`, `sheetApi`, `sheetId`, `ev`, `gn`, `er`, `md`  
  Example: `?datasrc=sheet&sheetApi=https://script.google.com/macros/s/XXX/exec&sheetId=1AbC...&ev=events&gn=genres&er=eraSettings&md=metadata`
- Reference timelines (GitHub/Sheets mix): `refTimelines` = URL-encoded JSON array  
  - GitHub: `{ "sourceType":"github", "owner":"user", "repo":"repo", "filePath":"file.json", "minImportance":2 }`  
  - Sheets: `{ "sourceType":"sheet", "gasApi":"https://.../exec", "sheetId":"xxxxx", "ev":"events", "gn":"genres", "er":"eraSettings", "md":"metadata", "minImportance":2 }`
- Snapshot restore (from GitHub `data/` folder):  
  - Specify `snapshot` or `snapshotpath` as JSON path relative to `data/`  
  - Default source repo: same as the main timeline `owner/repo`  
  - Different repo: add `snapshotowner` and `snapshotrepo`  
  - Files deployed only to Cloudflare Pages / Netlify are not used for `snapshot` lookup (`main/data/` on GitHub is the source)  
  - Same-repo example: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshot=snapshot-tutorial.json`  
  - Cross-repo example: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshotowner=foo&snapshotrepo=bar&snapshotpath=snapshots/demo.json`  
  - `snapshotURL` / `snapshotUrl` / `data` are deprecated  
Unneeded params for the chosen main data source are stripped automatically when saving settings.

### Google Sheets (GAS) sheet structure
- `events`: required headers `label, label_en, startYear`; optional `endYear, genre, imp, url, url_en, note, note_en, image`.  
  - genre: pipe-delimited (e.g., `ANI|JAPAN|TVP`); imp: 1–5; url/url_en: single or pipe-delimited.  
  - Clipboard TSV order (reference): `label label_en startYear endYear genre(pipe) imp url url_en note note_en image`
- `genres`: headers `code, label, label_en, conjunction` (`conjunction` for AND helper).
- `eraSettings`: headers `name, startYear, endYear, color, opacity, enabled, fillEnabled`.
- `metadata`: e.g., `title_ja, title_en, description_ja, description_en, initialCreator, contributors(pipe), contact_admin_name/email/x/org, createdAt, version, language(pipe), copyright, license, licenseUrl, notes`.

### Google Sheets (GAS) mode behavior
- Detail list “pencil”: opens edit modal; on save, TSV is copied to clipboard and the sheet is opened—paste manually into the target row.
- Detail list “trash”: jumps to the sheet cell for manual deletion (no inline delete).
- Left-column empty click: jumps to nearby row for manual add in the sheet.
- “Reload”: reload from GAS API and refresh display.

### Edit mode
- Without `?editmode=ON`:
  - Detail list pencil/trash/add are disabled.
  - Clicking blank left column does not open edit modal (Sheets mode also does not move).

### Reference timeline UI (GitHub/Sheets)
- Separate inputs for GitHub and Sheets reference timelines; “Add reference timeline” buttons for each.
- Saved as JSON in `refTimelines` and added to URL.

### Disclaimers
- No guarantees about timeline contents or damages.
- Bugs may not be fixed immediately; for critical demos, keep the page open locally.

### Technical Specifications
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Data Format**: JSON, CSV, TSV
- **External integrations**: GitHub API; Google Apps Script (GAS) Web API (for Sheets)
- **External integration (added)**: `/api/ai-search` (Cloudflare Pages Functions / Netlify Functions)
- **Supported browsers**: Modern browsers (Chrome, Firefox, Safari, Edge)

## License
- Data: Generally **CC BY 4.0**. If short descriptions must follow source share-alike, that item is marked **CC BY-SA 4.0** in `CREDIT.md`.
- Details: see `LICENSE_DATA.txt`, `CREDIT.md`

## Support
Submit issues/requests/**timeline content corrections** to GitHub Issues:  
https://github.com/hortense667/xnative/issues

Labels:
- `data-correction` (content correction)
- `feature-request`
- `bug`

For security concerns, see `SECURITY.md`.
