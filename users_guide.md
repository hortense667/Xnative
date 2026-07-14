# Xnative/Timeline ユーザーガイド / Xnative/Timeline User Guide

**このドキュメントには日本語版と英語版が含まれています。英語版は後半にあります。This document includes both a Japanese version and an English version. The English version is in the latter part.**

## 日本語版

このリポジトリはデータ（JSON）専用です。アプリは別リポジトリ/ホスティングで提供されます。

### はじめに

ネイティブタイムラインは、年表データを視覚的に表示・編集できるWebアプリケーションです。ポップカルチャーやデジタル技術の歴史を年表形式で管理し、個人の体験と照らし合わせることができます。

**GitHubユーザーなら誰でも管理者になれる分散型システム**として設計されており、自分のリポジトリで独自の年表データを管理できます。

### 参照年表機能について
### フキダシ（吹き出し）詳細ガイド

#### 概要
右側のグラフエリアに注釈を配置できるフキダシ機能です。先端（ポインタ）はクリック位置になり、三角テールが自動で最適な辺から接続されます。角丸部分からは出ず、接合位置は辺の中央±1/3の範囲に制限されます。

#### 作成・編集・削除
- 作成: Shift+クリック → 右側エリアをクリック
- 編集: 表示モードで鉛筆アイコンをクリック
- 削除: ゴミ箱アイコン（バブル本体・三角テール・継ぎ目カバーを同時に削除）
- 移動: バブルはドラッグで移動、三角はテールをドラッグして先端座標を変更

#### スタイル設定（表示モードのみ）
- 右クリックメニューから以下を変更
  - 色テーマ（数種）
  - 文字サイズ（A-/A+ 連続押し可、下限8px・上限なし）
  - 太字（B トグル）
  - テイル表示/非表示（△ボタン）

#### 表示の調整
- 内側余白は左右対称（上下13px・左右16px）
- 三角テールとバブルの継ぎ目は自動で馴染むよう処理（背景色のシーム＋枠線揃え）

#### スナップショット
- スナップショット保存/復元に対応（位置・テキスト・スタイル・先端座標）
- 復元後、GitHubが新しければ反映をブロックする仕組みに準拠
- 開いているウェブ画面パネルも保存・復元されます（位置、表示中のURL、言語設定など）
- **ローカルJSONデータソース**: 「スナップショット保存」はPCへJSONをダウンロードし、「スナップショット復元」はPCからJSONを選択します。`?snapshot=...` / `?snapshotpath=...` によるURL復元はできません。
- **GitHub JSONデータソース**: 「スナップショット保存」は同じ `owner/repo` の `data/` フォルダへ保存し、「スナップショット復元」は同フォルダの一覧から選んで復元します。保存には対象リポジトリへの書き込み権限を持つアクセストークンが必要です。
- GitHub JSONでURLから復元する場合は `?snapshot=xxx.json` または `?snapshotpath=xxx.json` を使用します。取得先は `data/` フォルダで、既定はメイン年表と同じリポジトリ（`owner/repo`）です。
- 別リポジトリからURL復元する場合は `snapshotowner` / `snapshotrepo` を指定します。
- `snapshotURL` / `snapshotUrl` / `data` パラメータは廃止

#### 画像表示機能
- テキストに「#https://example.com/image.png」の形式で画像URLを記述すると画像を表示
- 「#https://example.com/image.png キャプション」の形式でキャプションも表示可能
- 画像はドラッグ移動・角からのリサイズ（アスペクト比維持）に対応
- 画像のマージンは最小限（フキダシの枠線のみ）
- キャプションはフキダシの文字色・サイズ設定を継承

#### 改行対応
- フキダシ内のテキストで改行が有効
- 入力時の改行が表示時も反映される

### 範囲ガイド（コの字形）

右側のグラフエリアに「範囲ガイド（コの字形）」を配置できます（範囲の視覚ガイド用）。

#### 作成
- Ctrl+Shift+右クリック → 右側エリアに設置

#### 操作
- 移動: 縦棒の中央をドラッグ
- 太さ変更: 縦棒の右側をドラッグ
- 高さ変更: 縦棒の上/下をドラッグ
- 足（上/下）: 三角足をドラッグして左右に伸縮（上下連動）

#### スタイル
- 右クリックで色テーマ
- Rで反転
- △で足の表示/非表示


#### 参照年表の読み込み（GitHub）

- 参照年表は GitHub 上の JSON を読み取り専用でマージ表示します
- 起動時・設定保存時などに、設定された参照年表を順に取得します
- **メイン年表**は従来どおり毎回最新を取得します。**参照年表のみ**短時間キャッシュ（最大約15分）し、同じファイルの再取得を抑えます
- raw 取得が失敗した場合（HTTP 429 など）、設定済みの **GitHub アクセストークン** があれば GitHub API（contents）へフォールバックします
- 参照年表を多数同時に設定するとレート制限に当たりやすいです。本数を減らす、またはトークンを設定してください

#### 参照年表とは
参照年表機能は、メインの年表データに加えて、複数の年表データを同時に表示・比較できる機能です。参照年表のデータは読み取り専用で、編集や削除はできません。

#### 参照年表の設定方法
1. **設定画面で参照年表ファイルパスを指定**
   - 「設定」→「参照年表ファイルパス」に、カンマ区切りで最大10個のJSONファイルパスを入力
   - 例：`timeline_popculture_japan_01.json, timeline_ai_01.json`

2. **URLパラメータで直接指定**
   - URLに `refTimelines`（JSON配列）を追加（重要度も含めて指定可能）
   - 例：
     ```
     nativetimeline201.html?owner=hortense667&repo=nativetimeline&filePath=timeline_digital_japan_01.json&refTimelines=%5B%7B%22owner%22%3A%22hortense667%22%2C%22repo%22%3A%22nativetimeline%22%2C%22filePath%22%3A%22timeline_backglound_01.json%22%2C%22minImportance%22%3A2%7D%5D
     ```

#### 参照年表の特徴
- **読み取り専用**: 編集・削除は不可（鉛筆アイコンとゴミ箱アイコンがグレーアウト）
- **独立したジャンル管理**: 各参照年表ごとにジャンルのオン/オフを制御
- **視覚的区別**: 参照年表の項目は青色で表示
- **検索対象**: ジャンルがオンになっている参照年表の項目も検索対象に含まれる

#### 参照年表の編集方法
参照年表の内容を編集したい場合は、ブラウザの別タブでそのファイルをメインのファイルパスとして開いて編集してください。

例：
- メインタブ：`timeline_digital_japan_01.json` + 参照：`timeline_popculture_japan_01.json`
- 編集タブ：`timeline_popculture_japan_01.json` をメインとして開いて編集

### 目的別の使い方

#### 1. 見たり操作するだけの人（閲覧者）

**スマホ・タブレット**:
- 画面幅が狭いときは **閲覧中心** のレイアウトになります（年表の横スクロール、検索、項目詳細の確認）
- ヘッダーは **検索＋≡メニュー** を常時表示。ジャンル・重要度・リロード・設定などは **≡** から展開
- 詳細一覧・項目詳細・地球（🌐）プレビューは **下から出るボトムシート** 形式
- ホバー（マウスオーバー）前提の操作は使わず、**タップ** で開きます（🌐 はタップでプレビュー）
- 編集（✏️🗑️）は `?editmode=ON` のときのみ。本格的な編集は **PC推奨**

**対象**: データの追加や編集はしないが、ロードにより一時的な追加はできる

**基本的な操作**:
- 年表の表示とスクロール
- 検索機能の利用
- ジャンル・重要度フィルター
- 年表の活用（イベント年・生年の合わせ）

**データの一時的な追加**:
- 「ロード」機能でCSVファイルからデータを読み込み
- 編集・追加・削除は可能（通常モードではGitHub保存対象、トークンなしはCSV出力）
- ローカルだけで保持したい場合は、データソースを「ローカルJSON（PC上）」に設定

**ウェブ画面の表示**:
- `webLinkBehavior` が未指定なら、Wikipedia URL・先頭が `#` のURL・先頭が `@` の画像URLは 🌐 でプレビューし、それ以外は ↗️ で新しいタブを開きます。
- `webLinkBehavior=open_tab` を指定すると、すべてのURLが ↗️ になり、ホバーせずクリックで新しいタブを開きます。
- 検索結果の青い項目は、ダブルクリックで編集画面（編集モードON時）を開けます

#### 2. いまある年表の編集に参加する人（コラボレーター）

**対象**: アクセストークンはないが編集後のCSV出力データを提供できる人

**注意**: 現状、この機能への十分な対応はできていませんが、機能としては存在します。

**基本的な操作**:
- 閲覧者の操作に加えて、項目の編集・追加・削除
- アクセストークンがない状態で編集を保存するとCSVが出力される
  - 出力名: `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{件数}items.csv`
- エクスポートしたデータを管理者に提供

**制限事項**:
- リモートデータを直接更新することはできない
- 編集内容はローカルにのみ保存される
- 他のユーザーとのリアルタイム同期は不可

#### 3. 自分で新たに年表を作りたい人（ローカル管理者）

**対象**: GitHubを使わず、PC上のJSONファイルだけで運用したい人

**用途**: 簡単な年表をプレゼンや分析に使うなどに適する

**基本的な操作**:
- 閲覧者・コラボレーターの操作すべて
- 設定でデータソースを「ローカルJSON（PC上）」に設定
- 「表示中の全項目をクリアしてローカルから読み込み」で `timeline_*.json` を開く
- 設定 → データソースに **読み込み／保存先の年表JSON** が表示される（直近に読み込んだ／保存したファイル名。バージョン違いの確認用）
- 編集画面の「保存」や詳細一覧の並び替え確定（閉じる）で、ローカルJSONを保存
- ヘッダーの「保存」ボタンでもローカルJSONを保存
- 初回保存時に保存先を選択し、以降は同じファイルへ上書き保存（対応ブラウザ）
- ローカルでの完全なデータ管理

**URL について（ローカルJSON）**:
- `?datasrc=local` でローカルモードであることだけ指定できます
- **ファイル名や PC 上のパスは URL では指定できず、自動読み込みもできません**（ブラウザのセキュリティ制限）
- どの JSON を編集中かは、上記の設定画面の表示で確認してください

**推奨ワークフロー**:
1. 設定でデータソースを「ローカルJSON（PC上）」に設定
2. ローカルJSON（`timeline_*.json`）を読み込み
3. 必要に応じて編集・追加・削除・並べ替え
4. 編集保存時またはヘッダーの「保存」でJSONを更新
5. 必要に応じて「スナップショット保存」で作業状態を保存
6. 継続時は同じローカルJSONを再度読み込む

#### 4. 自分で作った年表を公開したい人（GitHub管理者）

**対象**: GitHubにデータを置いて公開したい人

**必要な準備**:
- GitHubアカウント
- Personal Access Token
- リポジトリの作成

### 共有・共同編集の手順（最新版ドキュメント）
GitHub / ローカルJSON の「共有方法・初期設定・運用のコツ」は、更新しやすいよう別ドキュメントに切り出しています。まずはこちらを参照してください。

- GitHubで年表を育てる（フォーク→同期→PR、トークン作成など）: `timeline-sharing-github.md`
- ローカルで作ってからGitHub公開する（初心者向け）: `timeline-local-to-github-guide.md`
- ローカル→GitHub公開の1〜2ページ版（最短手順）: `timeline-local-to-github-quickstart.md`

#### 補足：Google Sheets → GitHub JSON への移行
Google Sheetsで管理していた年表を、GitHubで管理するJSON形式へ変換するためのツールとして `sheet_to_json_coverter.html` が用意されています（Sheets→JSON変換）。
現在、Google Sheets（GAS）データソースはサポート対象外です。移行後はローカルJSONまたはGitHub JSONで運用してください。

### 推奨運用方針

#### データ管理の方針

1. **定期的なバックアップ**
   - GitHubのバックアップ機能を活用
   - 重要な編集前は必ず「スナップショット保存」を実行
   - 定期的に「保存」「削除」「閉じる（並び替え）」でGitHubに反映

2. **バッチ反映と日常編集の使い分け**
   - CSV/TSVを大量投入した後は、**「ロード → セーブ（全体反映）」**で主年表全体をまとめて反映
   - 日常の小さな修正は、項目ごとの「保存」「削除」「閉じる（並び替え確定）」を利用
   - 「セーブ（全体反映）」は主年表全体に効く強い操作として扱う

3. **バージョン管理**
   - 大きな変更前はGitHubでコミットメッセージを記録
   - 必要に応じてタグやブランチを活用

4. **共同編集の管理**
   - 複数人で編集する場合は事前にルールを決める
   - 編集前に必ず「リロード」で最新データを取得
   - 編集後は必ず「保存」「削除」「閉じる（並び替え）」で変更を反映
   - 編集前は「スナップショット保存」でバックアップを取る

#### 公開の方針

1. **データの品質管理**
   - 定期的にデータの整合性をチェック
   - 不適切な内容がないか確認

2. **更新頻度**
   - 定期的な更新を心がける
   - 重要なイベントは迅速に追加

3. **コミュニティとの連携**
   - IssuesやPull Requestを活用
   - ユーザーフィードバックを積極的に取り入れる

### データ形式の詳細

#### CSV形式（ロード用）

**基本形式**:
```
開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en;timeLabel
```

`timeLabel` は任意です。指定すると、画面上で `［timeLabel］ラベル` として表示されます。

**例**:
```
1946;;ENIAC;ENIAC;HAR;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer;
1983;;任天堂ファミコン;Nintendo Famicom;GAM;5;https://ja.wikipedia.org/wiki/ファミリーコンピュータ;https://en.wikipedia.org/wiki/Nintendo_Entertainment_System;家庭用ゲーム機の革命;Home console revolution;80年代前半
```

**ジャンル定義**:
```
genre;CODE;LABEL;label_en;conjunction
```

**例**:
```
genre;ANI;アニメ;Animation;
genre;GAM;ゲーム;Game;
genre;JAPAN;日本;Japan;true
```

#### JSON形式（GitHub年表データ）

GitHub年表データのJSONは以下の構造です：

```json
{
  "metadata": {
    "title": { "ja": "ポップカルチャー年表", "en": "POP Culture Timeline" },
    "description": {
      "ja": "この年表は…",
      "en": "This timeline …"
    },
    "initialCreator": "Satoshi Endo",
    "contributors": ["Satoshi Endo", "Hortense Endo"],
    "contact": {
      "administrator": {
        "name": "Satoshi Endo",
        "email": "zzz@65536.net",
        "x": "https://x.com/hortense667",
        "organization": "ZEN University"
      }
    },
    "createdAt": "2025-10-01",
    "version": "1.0",
    "language": ["ja","en"],
    "copyright": "© 2025 Satoshi Endo",
    "license": "CC BY 4.0",
    "licenseUrl": "https://creativecommons.org/licenses/by/4.0/",
    "notes": "Updates from contributors are welcome …"
  },
  "events": {
    "1946": [
      {
        "label": "ENIAC",
        "label_en": "ENIAC",
        "genre": "HAR",
        "importance": 5,
        "url": "https://ja.wikipedia.org/wiki/ENIAC",
        "url_en": "https://en.wikipedia.org/wiki/ENIAC",
        "note": "初の大規模電子計算機",
        "note_en": "First large-scale electronic computer"
      }
    ]
  },
  "genres": {
    "ANI": { "label": "アニメ", "label_en": "Animation" },
    "GAM": { "label": "ゲーム", "label_en": "Game" }
  }
}
```

**注意**: 参照年表は読み取り専用のため、ここでのデータ反映対象にはなりません。

### トラブルシューティング

#### うまくいかないときのチェック項目

**参照年表が表示されない場合**：
1. ファイルパスが正しく設定されているか確認
2. 設定変更後は必ず「保存」ボタンを押しているか
3. ファイルがGitHubリポジトリに存在するか確認
4. ファイルパスにスペースや特殊文字が含まれていないか確認
5. エラーに `GitHub raw file error: 429` と出る場合：参照年表の本数を減らす、しばらく待って再試行、設定にアクセストークンを入れて API フォールバックを有効にする

**データのフル読み込み後に検索が意図せず走る場合**：
- GitHub／ローカルからの「全項目クリアして読み込み」では、検索欄と検索結果をリセットします
- ジャンル変更などの再描画時のみ、検索欄に文字が残っていれば検索結果を更新します

**GitHubへの保存が失敗する場合**：
1. アクセストークンが正しく設定されているか
2. リポジトリの所有者名とリポジトリ名が正しいか
3. ファイルパスが正しいか
4. ネットワーク接続が正常か

**データが更新されない場合**：
1. ブラウザのキャッシュをクリア
2. 「表示中の全ラベルをクリアしてGitHubから読み込み」を実行
3. 設定を一度リセットして再設定

**AI検索でエラーになる場合**:
1. `/api/ai-search` が有効なデプロイ先（Cloudflare/Netlify）で動作しているか確認
2. サーバー側に `GEMINI_API_KEY` または `OPENAI_API_KEY` が設定されているか確認
3. 「設定」のモデル名が有効か確認
4. トークン上限や Safety Margin を見直す

#### ローカルストレージ容量メンテナンス（Cloudflare/Netlify運用）

長期間運用すると、ブラウザの `localStorage` に旧データや過去の名前空間データが残り、まれに `QuotaExceededError`（容量超過）で編集系操作に影響することがあります。

- まずは DevTools Console で使用量を確認:
  - `inspectXnativeStorageUsage()`
  - `listXnativeNamespaces()`
- 旧名前空間の削除候補を確認（削除はしない）:
  - `cleanupOldXnativeNamespaces()`
- 旧名前空間を実際に削除:
  - `cleanupOldXnativeNamespaces({ dryRun: false, confirmToken: "DELETE" })`
- 必要時のみ、巨大キーの候補を確認/削除:
  - 確認: `cleanupLargestXnativeKeys({ topN: 10, minKiB: 256 })`
  - 削除: `cleanupLargestXnativeKeys({ dryRun: false, confirmToken: "DELETE", topN: 10, minKiB: 256 })`

運用目安:
- 定期実行は必須ではありません（通常は不要）
- 編集画面が開かない、保存が不安定、`QuotaExceededError` が出る場合に実施
- 実施後は `inspectXnativeStorageUsage()` で容量が下がったことを確認

#### ブラウザのリロードと「表示中の全ラベルをクリアしてGitHubから読み込み」の違い

**ブラウザのリロード**：
- ページ全体を再読み込み
- ローカルストレージの設定は保持される
- 参照年表の設定も保持される
- 編集内容は失われる（未保存の場合）

**「表示中の全ラベルをクリアしてGitHubから読み込み」**（ローカル読み込みも同様）：
- ローカルデータを完全にクリア
- GitHubから最新データを再読み込み（ローカル時はファイル選択）
- 参照年表も再読み込み
- 編集フラグや削除記録もクリア
- 検索欄・検索結果もリセット
- より確実に最新状態にリセット

### 基本的な操作の詳細

#### 年表の表示と操作

**年表の表示**:
- 0年代から2050年代まで縦スクロールで閲覧（デフォルト）
- 左側のカラムに年とイベントが表示
- 右側のエリアでドラッグ操作が可能

**スクロール操作**:
- マウスホイールまたはスクロールバーで上下にスクロール
- キーボードの上下矢印キーでも操作可能

#### 項目の編集

**項目の編集**:
1. 編集したい項目をクリック
2. 編集モーダルが開く
3. 以下の項目を編集可能：
   - ラベル（日本語・英語）
   - 開始年・終了年
   - ジャンル
   - 重要度（1-5）
   - URL（日本語・英語）
   - 注釈（日本語・英語）
4. 「保存」ボタンで変更を確定

注意（重要）:
- 編集モーダルは縦に長い場合があります。必ず一番下までスクロールして「保存」ボタンを押してください。押さない場合、変更は反映されません。
- 編集モーダルと詳細一覧は、上部の何もない部分をドラッグして位置を移動できます。
- 右側のグラフエリア（タイムライン部）をクリックすると、開いている詳細一覧/編集モーダルが閉じます。

**項目の追加**:
1. 詳細一覧で「追加」ボタンをクリック
2. 新しい項目の情報を入力
3. 「保存」ボタンで追加

**項目の削除**:
1. 編集モーダルで「削除」ボタンをクリック
2. 確認ダイアログで「OK」を選択

#### 検索機能

**ラベル検索**:
- 検索ボックスにキーワードを入力
- 選択中のジャンルのみが検索対象
- ラベル（日本語/英語）のどちらに一致してもヒット
- リアルタイムで検索結果が更新

**詳細検索**:
- 「詳細」チェックボックスをオンにして検索
- 注釈（日本語/英語）も検索対象に含めて検索可能

**検索結果の操作**:
- 詳細一覧と同じURL規則です。🌐 のURLはマウスオーバーでプレビュー、↗️ のURLはクリックで新しいタブを開きます。
- 検索結果の青い項目をクリックすると、その項目の注釈がポップアップ表示されます（英語モードのときは英語の注釈、日本語モードのときは日本語の注釈を表示）
- 再度クリックするか、マウスが項目から外れると注釈ポップアップが閉じます

**ワイルドカード検索**:
- 検索ボックスに「*」を入力して検索すると、現在選択されている分野（ジャンル）のすべての項目が検索結果として表示されます
- 重要度フィルターが設定されている場合は、その条件も適用されます

#### ジャンルフィルター

**ジャンル選択**:
1. 「ジャンル選択」ボタンをクリック
2. ジャンル一覧から選択
3. 複数選択可能（AND条件）

**ジャンルの種類**:
- ANI: アニメ
- MAN: マンガ
- GAM: ゲーム
- MUS: 音楽
- MOV: 映画
- TV: テレビ
- HAR: ハードウェア
- SOFT: ソフトウェア
- その他多数

#### 重要度フィルター

**重要度の設定**:
- 1: 参考程度
- 2: やや重要
- 3: 重要
- 4: かなり重要
- 5: 最重要

**フィルター操作**:
- 「重要度」ボタンで重要度別にフィルター
- 複数選択可能

#### 詳細一覧

**詳細一覧の表示**:
1. 「詳細」ボタンをクリック
2. 年別の詳細一覧が表示
3. 各項目の詳細情報を確認

**項目の並び替え**:
- ドラッグ&ドロップで順序変更
- 「ドラッグで一覧の順序を変更できます」の表示

**編集モード（`?editmode=ON`）との関係**:
- `editmode=ON` のときのみ、詳細一覧に **鉛筆（✏️）・ゴミ箱（🗑️）・追加** が表示されます
- `editmode` が無い（閲覧モード）のときは、これらのボタンは **表示されません**（グレーアウトではなく非表示）
- 参照年表の項目は、編集モードでも編集・削除不可

**X（旧Twitter）コメント連動**（詳細一覧の各項目）:
- **🔗** … **共有・検索パネル**を開く（リンクコピー、X投稿、X検索）
- **ラベル（青字）をクリック** … **項目詳細パネル** を開く（注釈と URL の一覧）
- **🌐 / ↗️** … ウェブ表示（下記「ウェブプレビュー」参照。`open_tab` 時は ↗️）
- 手動で **Xコメントマーク** を付けた項目には、ラベル横に **𝕏** バッジが表示されます（編集画面のチェックボックス）

**共有・検索パネル**（🔗 クリック）:
- **コメントを共有** … **Xにコメントを投稿** で X の投稿画面を開く（ラベル ＋ `#XnativeTimeline` ＋ URL）
- 修正・追加の提案は、投稿時に `#EditReq` または `#AddReq` をハッシュタグに追加（専用ボタンはありません。パネル内の案内文を参照）
- **この項目のX投稿を見る** … X の検索画面を新しいタブで開く（公開投稿の検索は **Xのみ**）
- **X以外への共有** … **項目ラベル** ＋ 共有 URL をコピーして Facebook・LINE 等へ貼り付け
- パネル内の「ハッシュタグのルール」に運用ルールを記載

**項目詳細パネル**（ラベルクリック、または X 投稿 URL から起動したとき）:
- 詳細一覧の横に、**注釈**（`note` / `note_en`）と **URL リンク一覧** を表示
- 共有 URL（`?gh=...&t=...`）からアクセスした場合: 年表を開き **該当年の詳細一覧** を表示。URL に含まれる **項目ラベル**（`lk`）でその年の中を検索し、一致があれば項目詳細パネルも開く。**一致がなければ項目詳細パネルは開かない**（X 検索の iframe 埋め込みは行いません）

#### 短縮共有リンク（gh + t）と作者リポの xnative_link_map.json

X 投稿などで URL を短くするため、**GitHub ID（`gh`）** と **短い年表キー（`t`）** を使います。

**利用者向け（クリックしたとき）**:
1. `https://xnative.netlify.app/xnative051.html?gh=hortense667&t=jimbocho03-y1910&lk=a1b2c3d4` のようにアクセス
2. アプリ起動時に GitHub **`{gh}/xnative-timeline`** リポジトリの **`xnative_link_map.json`**（`main`）を取得
3. `t`（例: `jimbocho03-y1910`）を **`y`（年）** と `filePath` などに展開し、**`lk` はそのまま引き継ぐ**
4. 読み込み後、**その年の中でラベル照合**し、見つかれば項目詳細パネルを開く

**年表作者向け（推奨フロー）**:
1. GitHub に **`xnative-timeline`** という名前のリポジトリを作る（名前は固定）
2. リポジトリ直下に `xnative_link_map.json` を置く
3. 年表 JSON は同リポでも、別リポでも可（`params` で `repo` / `filePath` を指定）
4. 年表キーは **短く**（英小文字・数字・ハイフン推奨。例: `jimbocho03`, `ai02`）

```json
{
  "schemaVersion": 1,
  "entries": {
    "jimbocho03": {
      "params": "filePath=timeline_jimbocho_03.json",
      "label": "神田神保町年表 0.2"
    },
    "ai02": {
      "params": "repo=my-data&filePath=timelines/ai.json",
      "label": "AI史（別リポの例）"
    }
  }
}
```

**`params` の書き方**:
- 通常のクエリ文字列と同じ。**`&` で複数パラメータを連結**（先頭の `?` は不要）
- `owner` を省略すると URL の `gh` が使われます。`repo` を省略すると **`xnative-timeline`** が使われます
- `refTimelines` など JSON を含む値は **1 回 URL エンコード**して書きます

**共有 URL の形**:

| パターン | 例 | 説明 |
|----------|----|------|
| 推奨 | `?gh=alice&t=jimbocho03-y1910&lk=…` | GitHub ID + 短い年表キー。`-y{年}` で `y` を自動付与 |
| 旧形式（非対応） | `?xid=jimbocho03-y1910&lk=…` | 現在はサポートしていません |

**年表 JSON の metadata（X 連動用・任意）**:

| フィールド | 例 | 用途 |
|-----------|-----|------|
| `xHashtag` | `"Jimbocho03"` | X 検索用の補助タグ（共有投稿本文の既定ハッシュタグは `#XnativeTimeline`） |
| `xLinkId` | `"jimbocho03"` | 年表キー（`t` のベース。`xnative_link_map.json` のキーと揃える） |
| `shareBaseUrl` | `"https://xnative.netlify.app/xnative051.html"` | X 投稿に載せる短縮リンクのベース URL（未設定時は現在開いているページの origin+pathname） |
| `webLinkBehavior` | `"open_tab"` | ウェブ表示モード。`open_tab` はすべて ↗️/クリックで新しいタブ。`hover` を明示すると従来どおり 🌐/ホバープレビュー。未指定時は下記URL規則。 |

投稿時の識別子例: コメント `#XnativeTimeline`、修正の提案 `#XnativeTimeline #EditReq`、追加の提案 `#XnativeTimeline #AddReq`（提案系タグは「Xにコメントを投稿」から開いた画面で手動追加）。項目は **ラベル** と共有 **URL**（年＋ラベルをエンコード）で特定します。同一年内でラベルが重複する場合は先頭の項目に一致します。

**運用**: 作者は自分の **`xnative-timeline`** リポの `main` に `xnative_link_map.json` を push してください。アプリは raw.githubusercontent.com から取得します。

**ウェブ画面の表示**:
- `webLinkBehavior=open_tab` では、すべてのアイコンが ↗️ になり、クリック時に新しいタブで開きます
- `webLinkBehavior` 未指定時は、Wikipedia URL と先頭が `#` のURLは 🌐（ホバーでプレビュー）、先頭が `@` の画像URLは 🌐（画像表示）、それ以外は ↗️（クリックで新しいタブ）です
- `hover` を明示すると、従来どおりすべて 🌐（ホバープレビュー）です
- Amazon専用の `URL&画像URL` 形式は廃止しました。画像は `@https://example.com/image.png` のように先頭へ `@` を付けて指定します
- 検索結果の青い項目も同じ規則です
- **↗️ の検査用プレビュー**: ↗️ のアイコンまたは検索結果を **Shift+クリック**すると、新しいタブを開かず、🌐クリックと同じ固定プレビューを表示します。`#` を付けて常時プレビューにするか判断するために使えます。

#### ウェブプレビュー（地球マーク）

**開き方**:
- `hover` モード: 詳細一覧の地球マーク（🌐）、または検索結果の青い項目にマウスオーバー（約1秒）でプレビューパネルを表示。地球マーククリックで固定
- `open_tab` モード: 詳細一覧の ↗️ と検索結果クリックで新しいタブを開く。例外として **Shift+クリック**は固定プレビューを表示します
- パネル上部の「新しいタブとして開く」「他のURLに切り替える」「閉じる」が使えます（`| ` 区切りで複数URL、`url` / `url_en` の切替に対応）

**埋め込み可のサイト**（Wikipedia など）:
- パネル内の iframe にページを表示します

**埋め込み不可のサイト**（多くの商用サイト、自治体サイト、note.com など）:
- iframe では開けないため、次を表示します
  - ブラウザ風の背景（アドレスバー・ぼかしたページイメージ）
  - メッセージ：「このサイトは新しいタブで閲覧できます。新しいタブで開きますか？」
  - **「はい」** ボタン（クリックで新しいタブを開く）
- ヘッダーの「新しいタブとして開く」ボタンからも同じ URL を開けます

**画像URL**:
- `@https://example.com/image.png` のように先頭へ `@` を付けると、iframeではなく画像をプレビューパネルに表示します

**判定の仕組み（利用者向けの要点）**:
- 年表 JSON に埋め込み不可リスト（`metadata.embedBlocklist` または同名の `timeline_xxx_embed.json`）がある場合、地球マークを押した時点で上記の案内を表示します（iframe を試しません）
- リストが無い URL は従来どおり iframe で試行し、失敗した場合も同様の案内に切り替わります

#### 年表作者向け：埋め込み不可 URL の事前チェック

年表の URL を編集したあと、埋め込み可否を一括調査してリスト化できます。

```bash
node tools/check-embed-urls.mjs timeline_xxx.json timeline_xxx_embed.json --update-metadata
```

- `timeline_xxx_embed.json` … 調査結果（`blockedUrls` / `blockedHostPatterns`）
- `--update-metadata` … 年表 JSON の `metadata.embedBlocklist` にも書き込み
- 調査方法：`X-Frame-Options` と CSP の `frame-ancestors` を HEAD リクエストで確認（Node 上で実行。ブラウザ単体では CORS のため同じ判定ができません）
- `_embed.json` が無くてもアプリは動作します（既知ドメインの簡易判定と iframe 失敗検知がフォールバック）

**配置**: 年表 JSON と同じフォルダに `_embed.json` を置くと、読み込み時に自動で取り込まれます。

#### 年表の活用例

**使い方の例（任天堂ファミコン）**:
1. **イベント年を合わせる**: ドラッグ専用レーンの水色の丸を上下にドラッグして、左カラムのラベル「83 任天堂ファミコン」と同じ高さに揃える。縦軸の内側に「1983年」と表示される。
2. **生年を合わせる**: 水色の斜め線の左端（縦軸と交わる位置）近くの水色の丸を上下にドラッグして、生年（例：1965年生）に合わせる。上部には「18歳」と表示される。

**同じ操作は赤い丸（赤色ライン）でも行える。右上の小さな丸ボタンで各ラインの表示をオン/オフできる。**

#### 多言語対応

**言語切り替え**:
- 右上の「EN」ボタンで英語表示に切り替え
- URLに `?lang=en` を追加して英語表示でアクセス
- 日本語に戻す場合は「JA」ボタンをクリック

**多言語データ**:
- 日本語と英語の両方の情報を保持
- 表示時は選択された言語に応じて適切なフィールドが優先表示

### 障害対策とオフライン利用

#### サービス障害への対応

ネイティブタイムラインは、CloudflareやGitHub（データを保管・公開している）、DNSなどの外部サービスに依存しています。これらのサービスに障害が発生した場合の対策について説明します。

#### 事前準備：HTMLファイルの保存

**確実にデモを行いたい場合の事前準備**:

1. **HTMLファイルの保存**
   - 通常のアクセスが可能な状態で、ページ上で右クリック
   - 「名前を付けて保存」を選択
   - HTMLファイルとして保存（例：`nativetimeline_backup.html`）

2. **保存のタイミング**
   - 重要なプレゼンテーションやデモの前
   - 定期的なバックアップとして
   - 最新のデータが反映された状態で保存

#### オフライン利用方法

**障害発生時の利用手順**:

1. **保存したHTMLファイルを開く**
   - 保存したHTMLファイルをダブルクリック
   - ブラウザで直接開く

2. **設定の調整**
   - 「設定」ボタンをクリック
   - **アクセストークンを空にする**（重要）
   - その他の設定は必要に応じて調整

3. **データの読み込み**
   - 「ロード」機能で事前に準備したCSVファイルを読み込み
   - または、保存時点のデータで利用

#### 注意事項と制限

**重要な注意点**:

1. **反映の不整合**
   - オフライン利用は便宜的な使い方です
   - 復旧のタイミングで反映に不整合が生じる可能性があります
   - アクセストークンは必ず空にして使用してください

2. **データの整合性**
   - オフラインで編集した内容は、サービス復旧後に手動で反映する必要があります
   - 複数人での編集がある場合は、競合が発生する可能性があります

3. **著作権について**
   - HTMLファイルはダウンロード可能ですが、著作権によって保護されています
   - 個人利用・教育目的での利用に限定してください
   - 商用利用や再配布は禁止されています

#### 推奨される運用方針

1. **定期的なバックアップ**
   - 重要なイベント前には必ずHTMLファイルを保存
   - 月1回程度の定期バックアップを推奨

2. **データの二重保存**
   - HTMLファイルの保存
   - CSVファイルでのデータエクスポート
   - 両方の方法でデータを保護

3. **障害時の連絡先**
   - サービス障害が発生した場合は、GitHubのIssuesで報告
   - 緊急時は管理者への直接連絡も検討

## ライセンス
- データ: 原則 CC BY 4.0。項目単位で CC BY-SA 4.0 の例外がある場合は `CREDIT.md` に明記します。
- 詳細は `LICENSE_DATA.txt` を参照。

## コミュニティとの連携
- **Issues と Pull Request を活用**してください。
- Issues 作成時はテンプレートから該当（内容訂正 / 機能提案 / 不具合報告）を選び、  
  **再現手順・スクリーンショット・参照URL** を添付いただけると助かります。
- フィードバック導線：
  - 一般: https://github.com/hortense667/nativetimeline/issues
  - セキュリティ: `SECURITY.md` の手順に従ってください。

---

## English Version

This repository is for data (JSON) only. The application is provided in a separate repository/hosting.

### Introduction

NativeTimeline is a web application that allows you to visually display and edit timeline data. You can manage the history of pop culture and digital technology in a timeline format and compare it with personal experiences.

Designed as a **distributed system where any GitHub user can become an administrator**, you can manage your own timeline data in your repository.

### About Reference Timeline Feature
### Speech Bubble Detailed Guide

#### Overview
A speech bubble feature that allows you to place annotations in the right graph area. The tip (pointer) becomes the click position, and the triangle tail automatically connects from the optimal edge. It doesn't extend from rounded corners, and the connection position is restricted to within ±1/3 of the edge center.

#### Create, Edit, Delete
- Create: Turn on the speech bubble add icon in header, or Shift+click → Click in right area
- Edit: Click pencil icon in display mode
- Delete: Trash icon (simultaneously deletes bubble body, triangle tail, and seam cover)
- Move: Drag bubble to move, drag tail to change tip coordinates

#### Style Settings (Display Mode Only)
- Change the following from right-click menu:
  - Color theme (multiple options)
  - Font size (A-/A+ continuous press possible, minimum 8px, no maximum)
  - Bold (B toggle)
  - Tail display/hide (△ button)

#### Display Adjustment
- Internal padding is symmetrical (13px top/bottom, 16px left/right)
- Triangle tail and bubble seam are automatically blended (background color seam + border alignment)

#### Snapshots
- Supports snapshot save/restore (position, text, style, tip coordinates)
- After restoration, complies with mechanism to block synchronization if GitHub is newer
- To restore via URL, use `?snapshot=xxx.json` or `?snapshotpath=xxx.json`
- Source is the `data/` folder. By default, it uses the same repository as the main timeline (`owner/repo`)
- To load from another repository, specify `snapshotowner` and `snapshotrepo`
- `snapshotURL` / `snapshotUrl` / `data` parameters are deprecated

#### Image Display Feature
- Display images by writing image URL in text format "#https://example.com/image.png"
- Caption can also be displayed in format "#https://example.com/image.png Caption"
- Images support drag movement and resize from corners (maintains aspect ratio)
- Image margins are minimal (bubble border only)
- Captions inherit speech bubble text color and size settings

#### Line Break Support
- Line breaks are effective in speech bubble text
- Line breaks during input are reflected in display

### Range Guide (Bracket Shape)

You can place a "range guide (bracket shape)" in the right graph area (for visual range guidance).

#### Create
- Ctrl+Shift+Right-click → place in the right area

#### Interactions
- Move: drag the middle of the vertical bar
- Thickness: drag the right edge of the vertical bar
- Height: drag the top/bottom of the vertical bar
- Feet (top/bottom): drag to resize horizontally (linked)

#### Style
- Right-click for color presets
- R to reverse
- △ to show/hide feet

#### What is Reference Timeline
The reference timeline feature allows you to display and compare multiple timeline data simultaneously in addition to the main timeline data. Reference timeline data is read-only and cannot be edited or deleted.

#### How to Set Up Reference Timeline
1. **Specify reference timeline file path in settings**
   - Enter up to 10 JSON file paths separated by commas in "Settings" → "Reference Timeline File Path"
   - Example: `timeline_popculture_japan_01.json, timeline_ai_01.json`

2. **Direct specification in URL parameters**
   - Add `refTimelines` (JSON array) to URL (can specify importance level)
   - Example:
     ```
     nativetimeline201.html?owner=hortense667&repo=nativetimeline&filePath=timeline_digital_japan_01.json&refTimelines=%5B%7B%22owner%22%3A%22hortense667%22%2C%22repo%22%3A%22nativetimeline%22%2C%22filePath%22%3A%22timeline_backglound_01.json%22%2C%22minImportance%22%3A2%7D%5D
     ```

#### Reference Timeline Features
- **Read-only**: Cannot edit or delete (pencil and trash icons are grayed out)
- **Independent genre management**: Control genre on/off for each reference timeline
- **Visual distinction**: Reference timeline items are displayed in blue
- **Search target**: Items from reference timelines with genres turned on are included in search

#### How to Edit Reference Timeline
To edit reference timeline content, open that file as the main file path in a separate browser tab.

Example:
- Main tab: `timeline_digital_japan_01.json` + Reference: `timeline_popculture_japan_01.json`
- Edit tab: Open `timeline_popculture_japan_01.json` as main and edit

### Usage by Purpose

#### 1. People Who Just Want to View and Operate (Viewers)

**Mobile / tablet**:
- Narrow viewports use a **browse-first** layout (horizontal scroll on the timeline, search, item detail)
- Header shows **search + ≡ menu**; genre, importance, reload, settings, etc. expand from **≡**
- Detail list, item detail panel, and globe (🌐) preview open as **bottom sheets**
- Touch devices skip hover; use **tap** (🌐 opens preview on tap)
- Edit icons (✏️🗑️) only with `?editmode=ON`; **PC recommended** for full editing

**Target**: Cannot add or edit data, but can temporarily add through loading

**Basic Operations**:
- Display and scroll timeline
- Use search function
- Genre and importance filters
- Timeline utilization (aligning event years and birth years)

**Search Result Operations**:
- The same URL rules as the detail list apply: hover previews 🌐 URLs; click opens ↗️ URLs in a new tab.
- Clicking a blue search result item displays a popup with the item's note (English note in English mode, Japanese note in Japanese mode)
- Click again or move the mouse away to close the note popup

**Wildcard Search**:
- Entering "*" in the search box displays all items in the currently selected genres as search results
- Importance filter settings are also applied if configured

**Web Preview Panel**:
- With no `webLinkBehavior`, Wikipedia URLs and `#https://...` use 🌐 preview, `@https://...` displays an image in 🌐 preview, and other URLs use ↗️ to open a new tab.
- `webLinkBehavior=open_tab` makes every URL use ↗️ and open in a new tab on click.
- The Amazon-specific `URL&imageURL` format is removed. Use `@https://example.com/image.png` for images.
- **Preview an ↗️ URL**: Shift+click its detail-list icon or search result to open the same pinned preview as 🌐, without opening a new tab. Use this to decide whether the URL should be prefixed with `#`.

#### Detail list and X comment integration

**Detail list** (per-year item list):
- **Edit mode** (`?editmode=ON`): pencil, trash, and Add are available. **Without editmode**, pencil and trash are **hidden** (not grayed out).
- **🔗** — Opens **Share & search panel** (copy link, X posts, X search)
- **Label (blue, clickable)** — Opens **item detail panel** (note + URL list)
- **🌐 / ↗️** — Web action (see below; `open_tab` uses ↗️)
- Manual **X comment mark** shows an 𝕏 badge on the label (checkbox in edit modal)

**Share & search panel** (🔗 click):
- **Share comments** — **Post comment on X** opens X compose (label + `#XnativeTimeline` + URL)
- For correction or addition suggestions, add `#EditReq` or `#AddReq` to the hashtags when posting (no dedicated buttons; see the note in the panel)
- **View X posts for this item** — Opens X search in a new tab (**X only** for public post search)
- **Share outside X** — Copy item label + share URL for Facebook, LINE, etc.
- Hashtag rules are shown in the panel

**Item detail panel** (label click, or opening via `?gh=...&t=...` from a share link):
- Shows **note** and **URL links** beside the detail list
- From a share URL: opens the **year detail list**, then finds the item **by label within that year**. Opens the item panel only on match; **no item panel if not found**

#### Short share links (gh + t) and per-author xnative_link_map.json

Prefer **`gh`** (GitHub ID) + **`t`** (short timeline key) instead of a long query string.

1. Example: `https://xnative.netlify.app/xnative051.html?gh=hortense667&t=jimbocho03-y1910&lk=…`
2. On startup the app loads **`xnative_link_map.json`** from **`{gh}/xnative-timeline`** (`main`)
3. Short `t` (e.g. `jimbocho03-y1910`) expands to **`y`** and file settings; **`lk`** is kept from the URL
4. After load, the app finds the item by label in that year; opens the item panel only if found

**Authors** — create a GitHub repo named **`xnative-timeline`**, put `xnative_link_map.json` at the repo root, and use short keys (e.g. `jimbocho03`, `ai02`):

```json
"jimbocho03": {
  "params": "filePath=timeline_jimbocho_03.json",
  "label": "Kanda Jimbocho Timeline"
}
```

**`params` format**:
- Standard query string without leading `?`; **join multiple parameters with `&`**
- Omit `owner` to use `gh`; omit `repo` to use **`xnative-timeline`**
- URL-encode JSON values once (e.g. `refTimelines`)

| Pattern | Share URL | Behavior |
|---------|-----------|----------|
| Preferred | `?gh=alice&t=jimbocho03-y1910&lk=…` | Author map in `alice/xnative-timeline`; **`y` from `-y{year}`** |
| Legacy (unsupported) | `?xid=jimbocho03-y1910&lk=…` | No longer supported |

**Timeline metadata (optional)**: `xHashtag`, `xLinkId` (must match map key), `shareBaseUrl` (if omitted, current page origin+pathname is used), `webLinkBehavior` (`open_tab` opens every URL in a new tab; omitted uses the URL-prefix rules above) — see Japanese section above.

Push the map to your **`xnative-timeline` `main`** branch.

#### Web preview (globe icon)

**How to open**:
- `hover` mode: hover (~1 s) over the globe icon (🌐) in the detail list or a blue search result item; click the globe icon to pin the panel
- `open_tab` mode: click ↗️ in the detail list, or click a blue search result item, to open a new tab (no preview panel)
- Use **Open in New Tab**, **Switch to other URL**, and **Close** in the header (`|` -separated URLs; `url` / `url_en` switching supported)

**Embeddable sites** (e.g. Wikipedia):
- Shown inside the panel iframe

**Non-embeddable sites** (many commercial sites, government portals, note.com, etc.):
- Cannot be shown in iframe; the panel shows:
  - Browser-style background (address bar + blurred page thumbnail when available)
  - Message: “This site can be viewed in a new tab. Open in a new tab?”
  - **Yes** button (opens the URL in a new tab)
- You can also use **Open in New Tab** in the header

**Image URLs**:
- Prefix an image with `@`, such as `@https://example.com/image.png`, to show it directly in the preview panel.

**How blocking is decided**:
- If the timeline JSON includes `metadata.embedBlocklist` or a companion `timeline_xxx_embed.json`, those URLs skip iframe and show the message immediately
- URLs not in the list still try iframe first; on failure, the same message is shown

#### For timeline authors: embed-block pre-check

After editing URLs in a timeline JSON:

```bash
node tools/check-embed-urls.mjs timeline_xxx.json timeline_xxx_embed.json --update-metadata
```

- Writes `timeline_xxx_embed.json` with `blockedUrls` / `blockedHostPatterns`
- With `--update-metadata`, also updates `metadata.embedBlocklist` in the timeline JSON
- Checks `X-Frame-Options` and CSP `frame-ancestors` via HEAD (Node only; browsers cannot read these headers cross-origin)
- The app works without `_embed.json` (built-in domain hints + iframe failure detection as fallback)

Place `_embed.json` next to the timeline JSON to load it automatically.

**Search Result Operations (Edit)**:
- Double-click a blue search result item to open the edit modal (edit mode only)

**AI Search**:
- Click `AI Search` in the header and enter a natural-language query.
- Use Up/Down keys in the input box to recall previous queries.
- Results are shown as blue labels (same as normal search results).
- Scope is only currently selected genres; when `Main only` is ON, reference timelines are excluded.
- If estimated input exceeds token limits, the app shows an error before API call.
- Provider/model/token limits are configurable in Settings → AI Search.

**Temporary Data Addition**:
- Load data from CSV file using "Load" function
- Edit/add/delete are available (GitHub save in normal mode, CSV export when no token)
- Set Data Source to "Local JSON (on your PC)" when you want to keep everything local only

#### 2. People Who Want to Participate in Editing Existing Timeline (Collaborators)

**Target**: People who can provide downloaded data after "sync" without access token

**Note**: Currently, this functionality is not fully supported but exists as a feature.

**Basic Operations**:
- Edit, add, delete items in addition to viewer operations
- Export CSV when saving without an access token
  - Filename: `xnative_changes_{owner}_{repo}_{timeline}_{YYYYMMDD-HHMMSS}_{count}items.csv`
- Provide exported data to administrator

**Limitations**:
- Cannot directly update remote data
- Edits are saved locally only
- No real-time sync with other users

#### 3. People Who Want to Create Their Own Timeline (Local Administrators)

**Target**: People who want to operate only with local JSON files (without GitHub)

**Use Cases**: Suitable for using simple timelines for presentations and analysis

**Basic Operations**:
- All viewer and collaborator operations
- Set Data Source to "Local JSON (on your PC)" in Settings
- Use "Clear all displayed labels and load from Local" to open `timeline_*.json`
- Saving from edit modal or confirming reorder (close) writes to local JSON
- Header "Save" button also writes to local JSON
- First save chooses destination; later saves overwrite the same file (on supported browsers)
- Complete data management locally

**Recommended Workflow**:
1. Set Data Source to "Local JSON (on your PC)" in Settings
2. Load a local `timeline_*.json`
3. Edit/add/delete/reorder as needed
4. Save from edit flow or header "Save" to update JSON
5. Optionally save work state with "Snapshot Save"
6. Next session, open the same local JSON again

#### 4. People Who Want to Publish Their Own Timeline (GitHub Administrators)

**Target**: People who want to host and publish data on GitHub

**Required Preparation**:
- GitHub account
- Personal Access Token
- Repository creation

### Sharing / collaboration (up-to-date docs)
The detailed, maintained procedures are in these docs:

- GitHub workflow (fork → sync → PR, token, etc.): `timeline-sharing-github.md`
- Local creation to GitHub publish (beginner-friendly): `timeline-local-to-github-guide.md`
- Local → GitHub quickstart (1-2 pages): `timeline-local-to-github-quickstart.md`

#### Note: Migrating Google Sheets → GitHub JSON
`sheet_to_json_coverter.html` is provided to convert a timeline managed in Google Sheets into the JSON format to be managed on GitHub (Sheets → JSON conversion).
Google Sheets (GAS) data source is currently unsupported. After migration, use Local JSON or GitHub JSON.

### Recommended Operation Policy

#### Data Management Policy

1. **Regular Backup**
   - Utilize GitHub's backup function
   - Always execute "Snapshot Save" before important edits
  - Regularly reflect to GitHub with “Save/Delete/Close (reorder)”

2. **Batch Reflect vs Daily Edit**
   - Use **Load → Save (batch reflect)** when importing many CSV/TSV records and reflecting the merged main timeline at once
   - Use item-level save/delete/reorder-close for normal day-to-day edits
   - Batch Save is a strong operation that reflects the full main timeline

3. **Version Management**
   - Record commit messages on GitHub before major changes
   - Use tags and branches as needed

4. **Collaborative Editing Management**
   - Establish rules beforehand for multiple editors
  - Always get latest data with “Reload” before editing
  - Always reflect changes with “Save/Delete/Close (reorder)” after editing
   - Take backup with "Snapshot Save" before editing

#### LocalStorage Capacity Maintenance (Cloudflare/Netlify)

In long-running browser usage, old timeline namespaces may remain in `localStorage`. In rare cases this can trigger `QuotaExceededError` and impact editing operations.

- Check usage in DevTools Console:
  - `inspectXnativeStorageUsage()`
  - `listXnativeNamespaces()`
- Preview removable old namespaces (no deletion):
  - `cleanupOldXnativeNamespaces()`
- Remove old namespaces:
  - `cleanupOldXnativeNamespaces({ dryRun: false, confirmToken: "DELETE" })`
- If needed, preview/remove large keys:
  - Preview: `cleanupLargestXnativeKeys({ topN: 10, minKiB: 256 })`
  - Remove: `cleanupLargestXnativeKeys({ dryRun: false, confirmToken: "DELETE", topN: 10, minKiB: 256 })`

Operational guideline:
- This is not a mandatory periodic task in normal use.
- Run it when editing fails to open, save becomes unstable, or `QuotaExceededError` appears.
- After cleanup, verify with `inspectXnativeStorageUsage()`.

#### Publication Policy

1. **Data Quality Management**
   - Regularly check data consistency
   - Check for inappropriate content

2. **Update Frequency**
   - Aim for regular updates
   - Add important events promptly

3. **Community Collaboration**
   - Utilize Issues and Pull Requests
   - Actively incorporate user feedback

### Data Format Details

#### CSV Format (For Loading)

**Basic Format**:
