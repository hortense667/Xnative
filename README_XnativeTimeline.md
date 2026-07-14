# XnativeTimeline 1.0 / エックスネイティブタイムライン 1.0

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。
This document includes both a Japanese and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリは **XnativeTimeline 用のデータ**（JSON）のみを収録しています。アプリ本体のコードは別管理です。関連ソフトウェアであるJSONのファイル変換ツールのJavaScriptは収録しています。短縮リンクは作者ごとの **`xnative-timeline`** リポジトリにある **`xnative_link_map.json`**（`?gh=...&t=...`）を使います（旧 `?xid=...` は廃止）。

### 最初に（おすすめの始め方）
- まずは「既にある年表を体験したい」人は、メイン年表に GitHub JSON を使うのが簡単です（owner/repo/filePath をURLで指定）。
- 「自分で年表を作ってみたい」人は、まずローカルJSON（PC上）で作成し、仕上がったらGitHub JSONへ反映する方法がおすすめです。
- 共有・共同編集の詳しい手順は、以下のドキュメントを参照してください。
  - GitHubで育てる（オープンな共同編集）: `timeline-sharing-github.md`
  - ローカルで作ってからGitHub公開する（初心者向け）: `timeline-local-to-github-guide.md`
  - ローカル→GitHub公開の1〜2ページ版（最短手順）: `timeline-local-to-github-quickstart.md`
- Google Sheetsで管理していた年表を、GitHubで管理する **JSON形式** に移行したい場合は、変換ツール `sheet_to_json_coverter.html`（Sheets→JSON変換）を用意しています。

### 主な機能

ネイティブマップは、年表データを視覚的に表示・編集できるWebアプリケーションです。さまざまな分野の歴史を、それぞれの年表形式で管理し、個人の体験と照らし合わせることができます。分野ごとの年表を組み合わせて見ることができることを特徴としています。

- **年表の視覚的表示**: 0年代から2050年代までの年表を縦スクロールで表示（デフォルト）
- **多言語対応**: 日本語/英語の切り替えが可能
- **データ編集**: 項目の追加、編集、削除、並び替え
- **検索機能**: ラベルやジャンルによる検索
- **AI検索**: ヘッダーの「AI検索」から自然文検索（現在選択中ジャンルのみ）
- **データ連携/リロード**:
  - GitHub JSON との連携（読み込み・リロード）
  - ローカルJSON（PC上）の読み込み・保存に対応
- **CSV対応**: データの一括インポート
- **参照年表機能**: 複数の年表データを同時に表示・比較可能
- **フキダシ（吹き出し）**: 右側エリアをShift+クリックして注釈を配置。三角テールはクリック位置を先端にし、バブルの辺から自然に接続。スタイル（色・文字サイズ・太字）変更やドラッグ移動、スナップショット保存/復元に対応。テイルの表示/非表示切り替え、画像表示機能（#URL形式）、リンク（@URL形式＝末尾に空白1文字が必要）、改行対応。
- **範囲ガイド（コの字形）**:右側エリアでCtrl+Shift+クリックで、範囲ガイド（コの字形）を設置（〇年～〇年の範囲の視覚ガイド用）。縦棒の中央をドラッグで移動。縦棒の右側ドラッグで太さ変更。上下ドラッグで高さ変更。上/下の三角足をドラッグして左右に伸縮（上下連動）。右クリックで色設定、Rで反転、△で足の表示/非表示。
- **ホバー表示文字サイズ設定**: ラベル表示エリアにマウスをホバーした際の文字サイズ（年、ラベル名、重要度、注釈）を個別に設定可能。
- **オリジナルの年表作成**： ローカルJSONとGitHub JSONを使って誰でもオリジナル年表を作って運用できます。

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
  - ※ GitHub JSONデータソースでは、`snapshot` は GitHub の `owner/repo` の `main/data/` から読み込みます（Cloudflare/Netlify の配置先ではありません）。ローカルJSONデータソースではURL指定のスナップショット復元はできません。


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
- `webLinkBehavior` 未指定時は、Wikipedia URL・`#https://...` はホバーでウェブプレビュー、`@https://...` は画像プレビュー、それ以外はクリックで新しいタブを開く。`open_tab` はすべてクリックで新しいタブを開く
- 検索結果の青い項目をクリックで注釈をポップアップ表示
- 検索結果の青い項目をダブルクリックで編集モーダルを開く（editmode=ON の場合のみ）
- 検索ボックスに「*」を入力すると、選択されている分野のすべての項目を表示

#### X コメント連動（詳細一覧）
- **𝕏** … X 投稿画面（定型文＋ハッシュタグ＋`gh`/`t` 短縮 URL）
- **🔍** … X で当該項目のコメントを検索・一覧（新しいタブ）
- **ラベルクリック** … 注釈と URL 一覧の項目詳細パネル
- **`?gh=...&t=...`** … 作者の `xnative-timeline` 上のマップで展開して起動（`?xid=...` は非対応。[ユーザーガイド](users_guide.md)）

#### スマホ・タッチ向け（閲覧中心）
- 768px 以下またはタッチ端末でヘッダーをコンパクト化（検索＋≡メニュー）
- 詳細一覧・項目詳細・ウェブプレビューをボトムシート表示
- ホバーによる地球プレビューは無効化、**タップ** で開く
- 本格的な編集は PC 推奨（初回に案内表示）

#### ウェブプレビュー（地球マーク）
- 詳細一覧の地球マーク、または検索結果の青い項目にマウスオーバー（約1秒）／地球マークをクリックで固定
- metadata 未指定時: Wikipedia URL・`#https://...` は **🌐** でプレビュー、`@https://...` は **🌐** で画像プレビュー、それ以外は **↗️** でクリック時に新しいタブ
- 年表 metadata の `webLinkBehavior` で挙動を切替可能
  - `hover`: **🌐**、ホバーでプレビュー
  - `open_tab`: **↗️**、ホバーなし、クリックで新しいタブ
- **↗️ の検査**: ↗️ のアイコンまたは検索結果を **Shift+クリック**すると、新しいタブを開かずに🌐クリックと同じ固定プレビューを表示。`#` 接頭辞を付けるべきか確認できます
- **埋め込み可**（Wikipedia 等）: パネル内 iframe で表示
- **埋め込み不可**（nippon.com、note.com、多くの公式サイト等）: ぼかし背景＋「新しいタブで開きますか？」と **「はい」** ボタン。ヘッダーの「新しいタブとして開く」も利用可
- **画像URL**: `@https://example.com/image.png` 形式で画像プレビュー（Amazon専用の `URL&画像URL` 形式は廃止）
- 事前判定: 年表 JSON の `metadata.embedBlocklist` または `timeline_xxx_embed.json`（`tools/check-embed-urls.mjs` で生成）を読み込み、リスト載り URL は iframe を試さず案内表示
- リストが無い URL は iframe 試行後、失敗時に同案内へフォールバック

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
- **セーブ（全体反映）**: ロードで作ったマージ結果を、主年表全体としてGitHubへ反映（バッチ反映）
- **リロード（メイン年表）**:
  - GitHub JSON: 「リロード」で最新データを再読み込み
  - ローカルJSON（PC上）: 「表示中の全項目をクリアしてローカルから読み込み」で再読み込み
- **編集の反映（GitHub JSON）**:
  - アクセストークンあり: 「保存」「削除」「閉じる（並び替え）」でGitHubのJSONに反映
  - アクセストークンなし: 変更内容はCSVとして書き出し（GitHubには反映されません）
    - 出力名: `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{件数}items.csv`
- **参照年表**: 複数の年表データを同時に表示・比較（読み取り専用）
  - GitHub raw から取得（設定済みのアクセストークンがある場合、取得失敗時は GitHub API へフォールバック）
  - 参照年表のみ短時間キャッシュ（同一セッション内・最大約15分）。メイン年表の最新取得には影響しません
- **スナップショット**: 現在の状態（データ、フキダシ、設定、開いているウェブ画面パネル）を保存・復元。気軽に自分の年表を作り始めることができます
- **画像表示**: 画像URLの先頭に `@` を付けると、ウェブプレビュー内に画像が表示されます

### 埋め込み不可 URL の事前チェック（年表作者向け）

地球マークのプレビューは iframe 埋め込みに依存しますが、多くのサイトは `X-Frame-Options` 等で拒否されます。ブラウザ上では他サイトの HTTP ヘッダーを読めない（CORS）ため、**Node スクリプトで事前調査し JSON に載せる**運用を推奨します。

```bash
node tools/check-embed-urls.mjs timeline_xxx.json timeline_xxx_embed.json --update-metadata
```

| 出力 | 内容 |
|------|------|
| `timeline_xxx_embed.json` | `blockedUrls`, `blockedHostPatterns`, 調査ログ |
| `--update-metadata` | 年表 JSON の `metadata.embedBlocklist` にも同内容を書き込み |

- 年表読み込み時に `embedBlocklist` と同名 `_embed.json` を自動取り込み、地球マーク操作時に `isLikelyFrameBlocked()` で判定
- `_embed.json` が無くても動作（既知ドメイン＋ iframe 失敗検知）
- URL 追加・変更後はスクリプトを再実行してください

詳細は [ユーザーガイド](users_guide.md) の「ウェブプレビュー」「年表作者向け：埋め込み不可 URL の事前チェック」を参照。

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

- メイン年表（ローカルJSON / PC上）
  - datasrc=local
  - URL例（データソース指定のみ）: `?datasrc=local`
  - 実データは設定画面の「表示中の全項目をクリアしてローカルから読み込み」でファイルを選択して読み込みます
  - **URL だけではファイル名の指定・自動読み込みはできません**（ブラウザのセキュリティ上、PC上のパスへ勝手にアクセスできないため）
  - 設定 → データソースに **「読み込み／保存先の年表JSON」** として、直近に読み込んだ／保存したファイル名が表示されます（バージョン違いの取り違え防止用）

- 参照年表（GitHubのみ）
  - refTimelines=JSON配列（URLエンコード）
  - 各要素（GitHub型）: `{ "sourceType":"github", "owner":"user", "repo":"repo", "filePath":"file.json", "minImportance":2 }`
  - 例（エンコード前）:
    ```
    refTimelines=[{"sourceType":"github","owner":"user1","repo":"repo1","filePath":"file1.json","minImportance":2}]
    ```
  - 参照年表を多数まとめて読み込むと GitHub のレート制限（HTTP 429）に当たることがあります。設定にアクセストークンを入れると API フォールバックが有効になります。参照年表の本数を減らすことも有効です

- スナップショット復元（GitHub data フォルダ）
  - GitHub JSONデータソースで、`snapshot` または `snapshotpath` に JSON ファイル名（`data/` 相対）を指定
  - 既定の取得先: メイン年表と同じ `owner/repo`
  - 別リポジトリ指定: `snapshotowner`, `snapshotrepo`
  - Cloudflare Pages / Netlify に同名ファイルを置いても参照されません（GitHubの `main/data/` が参照先）
  - 例（同一リポジトリ）: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshot=snapshot-tutorial.json`
  - 例（別リポジトリ）: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshotowner=foo&snapshotrepo=bar&snapshotpath=snapshots/demo.json`
  - `snapshotURL` / `snapshotUrl` / `data` は廃止

メイン年表の種別に応じて、不要なパラメーター（GitHub系/Local系/旧Sheets系）はURLから自動的に取り除かれます（設定→「設定を保存」時に付与/整理）。

#### 短縮共有リンク（gh + t）

長い URL の代わりに **`gh`（GitHub ID）** と **`t`（短い年表キー）** で年表を開けます。

- 例: `https://xnative.netlify.app/xnative051.html?gh=hortense667&t=jimbocho03-y1910&lk=…`
- 起動時に **`{gh}/xnative-timeline`** の **`xnative_link_map.json`**（`main`）を参照し、展開してから読み込みます
- 作者は GitHub に **`xnative-timeline`** リポを作り、直下にマップを置きます。年表キーは短く（例: `jimbocho03`）
- 旧形式 **`?xid=...`** は現在サポートしていません

**`xnative_link_map.json` の `params`**:
- `&` で連結した通常のクエリ文字列（`?` 不要）
- `owner` 省略時は `gh`、`repo` 省略時は **`xnative-timeline`**
- `t=jimbocho03-y1910` 形式なら `y` は **自動付与**

**年表 metadata（任意）**: `xHashtag`, `xLinkId`（マップのキーと揃える）, `shareBaseUrl`, `webLinkBehavior`。`shareBaseUrl` 未設定時は現在開いているページのURL（origin + pathname）が使われます。`webLinkBehavior: open_tab` はすべてのURLを新しいタブで開きます。詳細は [ユーザーガイド](users_guide.md) を参照。

#### 補足：Google Sheets → GitHub JSON への移行
Google Sheetsで運用していた年表を、GitHub上で管理・共同編集できるJSON（アプリのGitHubデータ形式）へ変換するために、`sheet_to_json_coverter.html` を同梱しています。

### Google Sheetsサポートについて

Google Sheets（GAS）データソースは、現在サポート対象外です。  
既存のSheetsデータは `sheet_to_json_coverter.html` を使って JSON へ移行し、  
`ローカルJSON（PC上）` または `GitHub JSON` で運用してください。

### 編集可否（editmode）
- URLに `?editmode=ON` がない場合:
  - 詳細一覧の「鉛筆」「ゴミ箱」は **非表示**（「追加」ボタンは従来どおり無効表示）
  - 左カラム空白クリックでも編集モーダルは開かない

### 設定画面の参照年表UI
- 参照年表は GitHub JSON のみ設定できます
- 保存すると `refTimelines` にJSONとして保存され、URLにも `refTimelines` が付与されます
- 参照年表の読み込みは raw 取得を試み、失敗時（429 など）は設定済みトークンで GitHub API にフォールバックします。参照年表のみ短時間キャッシュされます

### ローカルJSON運用時のファイル名表示
- 設定 → データソース（ローカルJSON選択時）に **読み込み／保存先の年表JSON** を表示
- 「表示中の全項目をクリアしてローカルから読み込み」で選んだファイル名、または「セーブ（ローカル保存）」で指定したファイル名が記録されます
- データのフル読み込み時は検索状態をリセットします（読み込み直後に意図しない一覧検索が走らないようにするため）

### 免責事項
- このソフトによる年表の内容については、一切保証いたしません。
ｰ このソフトの使用によって利用者が被った損害については、一切保証いたしません。
- このソフトウェアに不具合があった場合もすみやかに対応できるとは限りません。デモンストレーションなどで必ず動作させたい場合は、JavaScriptで動作していますので、自身のコンピューター上でオープンしたままであれば動作します。

### 技術仕様

- **フロントエンド**: HTML5, CSS3, JavaScript (ES6+)
- **データ形式**: JSON, CSV, TSV
- **外部連携**: GitHub API
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

This repository contains only **data (JSON) for XnativeTimeline**. The application code is managed separately. JavaScript utilities for converting JSON/TSV/Sheets data are included. Short links use each author's `xnative-timeline` map (`xnative_link_map.json`) with `?gh=...&t=...` (legacy `?xid=...` is no longer supported).

### First Steps (recommended)
- Want to try existing timelines? Use the main timeline from GitHub JSON (specify owner/repo/filePath via URL).
- Want to build your own? Start in Local JSON (on your PC), then reflect finalized data to GitHub JSON.
Detailed sharing/operation guides:
  - Grow with GitHub (open collaboration): `timeline-sharing-github.md`
  - Build locally then publish to GitHub: `timeline-local-to-github-guide.md`
  - Quick 1-2 page version: `timeline-local-to-github-quickstart.md`
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
  - Local JSON (on your PC) load & save
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
- Without `webLinkBehavior`, Wikipedia and `#https://...` URLs preview on hover, `@https://...` URLs preview as images, and other URLs open in a new tab on click. `open_tab` makes every URL open in a new tab.
- Detail list: **𝕏** (post to X), **🔍** (X search in new tab), clickable label (note + URLs panel), **🌐** preview. Pencil/trash **hidden** unless `?editmode=ON`.
- Short links: `?gh=...&t=...` via author `xnative-timeline` map (legacy `?xid=...` remains supported during transition).
- Mobile/touch: compact header (search + ≡), bottom sheets for panels, tap instead of hover for 🌐 preview; PC editing recommended.

#### Web preview (globe icon)
- Hover (~1 s) or click the globe icon in the detail list; same for blue search hits
- Without metadata: Wikipedia and `#https://...` use **🌐** preview, `@https://...` uses **🌐** image preview, and other URLs use **↗️** to open a new tab.
- Per-timeline behavior can be switched via metadata `webLinkBehavior`
  - `hover`: **🌐**, hover preview
  - `open_tab`: **↗️**, no hover preview, click opens a new tab
- **Inspecting ↗️ URLs**: Shift+click a ↗️ icon or search result to show the same pinned preview as 🌐 without opening a new tab. This helps decide whether to prefix the URL with `#`.
- **Embeddable** (e.g. Wikipedia): shown in panel iframe
- **Non-embeddable** (many official/commercial sites, note.com, etc.): blurred background + “Open in a new tab?” with **Yes** button; header **Open in New Tab** also works
- **Images**: preview with `@https://example.com/image.png`; the Amazon-specific `URL&imageURL` format is removed
- Pre-check: loads `metadata.embedBlocklist` and optional `timeline_xxx_embed.json` (from `tools/check-embed-urls.mjs`); listed URLs skip iframe
- Unlisted URLs try iframe first, then fall back to the same message

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
  - Local JSON (on your PC): use “Clear all displayed labels and load from Local” to reload.
- **Apply edits (GitHub JSON)**:
  - With access token: “Save”, “Delete”, “Close (reorder)” update GitHub JSON.
  - Without token: changes are exported as CSV (not reflected to GitHub).
    - Filename: `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{count}items.csv`
- **Reference timelines**: multiple timelines shown/read-only.
- **Snapshot**: Save/restore state (data, speech bubbles, settings, open web preview panels) for easy personal timeline creation.
- **Images**: Prefix an image URL with `@` to show it in web preview.

### Embed-block pre-check (for timeline authors)

Globe preview uses iframes; many sites block embedding. Browsers cannot read cross-origin `X-Frame-Options` headers, so pre-generate a blocklist with Node:

```bash
node tools/check-embed-urls.mjs timeline_xxx.json timeline_xxx_embed.json --update-metadata
```

Writes `timeline_xxx_embed.json` and optionally `metadata.embedBlocklist`. Loaded automatically when the timeline JSON is opened. Works without `_embed.json` (domain hints + iframe failure fallback). Re-run after URL changes. See [users_guide.md](users_guide.md).

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
- Main timeline (Local JSON / on your PC): `datasrc=local`  
  Example: `?datasrc=local`  
  You must pick the file via “Clear all displayed labels and load from Local” in Settings. **URL cannot specify the filename or auto-load** (browser security).  
  Settings → Data Source shows **Loaded / saved timeline JSON** (last file from load or local save).
- Reference timelines (GitHub only): `refTimelines` = URL-encoded JSON array  
  - GitHub: `{ "sourceType":"github", "owner":"user", "repo":"repo", "filePath":"file.json", "minImportance":2 }`  
  - On raw fetch failure (e.g. HTTP 429), falls back to GitHub API when an access token is configured. Reference timelines are cached briefly (~15 min); main timeline fetching is unaffected.
- Snapshot restore (from GitHub `data/` folder):  
  - Specify `snapshot` or `snapshotpath` as JSON path relative to `data/`  
  - Default source repo: same as the main timeline `owner/repo`  
  - Different repo: add `snapshotowner` and `snapshotrepo`  
  - Files deployed only to Cloudflare Pages / Netlify are not used for `snapshot` lookup (`main/data/` on GitHub is the source)  
  - Same-repo example: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshot=snapshot-tutorial.json`  
  - Cross-repo example: `?datasrc=github&owner=hortense667&repo=xnative&filePath=timeline_popculture_02.json&snapshotowner=foo&snapshotrepo=bar&snapshotpath=snapshots/demo.json`  
  - `snapshotURL` / `snapshotUrl` / `data` are deprecated  
Unneeded params for the chosen main data source are stripped automatically when saving settings.

#### Short share links (gh + t)

Use **`gh`** (GitHub ID) + **`t`** (short timeline key) instead of long URLs.

- Example: `https://xnative.netlify.app/xnative051.html?gh=hortense667&t=jimbocho03-y1910&lk=…`
- Resolves via **`xnative_link_map.json`** in **`{gh}/xnative-timeline`** (`main`)
- Authors create a repo named **`xnative-timeline`** and place the map at the root; keep timeline keys short
- Legacy **`?xid=...`** is no longer supported

**`params` in the map**: `&`-joined query string (no leading `?`); omit `owner` to use `gh`, omit `repo` to use **`xnative-timeline`**. `t=jimbocho03-y1910` auto-appends `y`. Optional metadata: `xHashtag`, `xLinkId`, `shareBaseUrl` (if omitted, current page origin+pathname is used), `webLinkBehavior` (`open_tab` opens every URL in a new tab). See [users_guide.md](users_guide.md).

### About Google Sheets support
Google Sheets (GAS) data source is currently unsupported.
Use `sheet_to_json_coverter.html` to migrate existing sheet data into JSON,
then operate with Local JSON or GitHub JSON.

### Edit mode
- Without `?editmode=ON`:
  - Detail list pencil and trash are **hidden** (Add button remains disabled-style).
  - Clicking blank left column does not open edit modal.

### Reference timeline UI
- Configure GitHub JSON references.
- Saved as JSON in `refTimelines` and added to URL.

### Disclaimers
- No guarantees about timeline contents or damages.
- Bugs may not be fixed immediately; for critical demos, keep the page open locally.

### Technical Specifications
- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Data Format**: JSON, CSV, TSV
- **External integrations**: GitHub API
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
