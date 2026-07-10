# 1〜2ページ版: ローカル作成 → GitHub公開 クイックスタート

このガイドは、**初めての人が迷わず 30〜60分で一通り体験する**ための最短手順です。  
方針は「ローカルで安全に作る → 形になったら GitHub で公開」です。

## ゴール

- ローカルJSONで年表を新規作成できる
- 編集・並び替え・削除・保存の基本操作を確認できる
- 最後に GitHub に置いて共有URLで開ける

---

## 0. 事前準備（5分）

- 年表を `?editmode=ON` 付きで開く
- 作業用フォルダを作る（例: `my-timeline-work`）
- ブラウザは Chrome / Edge 推奨（ローカル上書き保存が安定）

---

## 1. 初期データを作る（5分）

1. `timeline_initial_00.json` をコピー  
2. `timeline_myfirst_01.json` にリネーム  
3. 作業フォルダに保存

ポイント:

- `timeline_initial_00.json`は、https://github.com/hortense667/Xnative/blob/main/timeline_initial_00.json からダウンロード。
- ファイル名は `timeline_` 始まり
- 文字コードは UTF-8

---

## 2. ローカルモードで読み込む（3分）

1. 「設定」を開く
2. データソースを「ローカルJSON（PC上）」に設定
3. 「表示中の全項目をクリアしてローカルから読み込み」
4. `timeline_myfirst_01.json` を選択

読み込み後、設定 → データソースの **「読み込み／保存先の年表JSON」** に選んだファイル名が表示されます。  
`?datasrc=local` はローカルモード指定のみで、**ファイルの自動読み込みはできません**。

---

## 3. いったん初期化して自分用の土台にする（5分）

`timeline_initial_00.json` の内容を理解する目的で一度触ったあと、  
自分の年表を作るときは次を実行します。

1. 「初期化（表示中の全項目とジャンル、時代区分をクリア）」  
2. CSV/TSV の「ロード」で自分のデータを投入  

これで「文具の既存データが残っていて邪魔」という状態を避けられます。

---

## 3.5 ロード用データ形式（CSV/TSV）一式

`ロード` は、先頭の非空行を見て区切り文字を自動判定します。

- 対応区切り: **タブ / `;` / `,`**
- 推奨: **`;` かタブ**（テキストにカンマを含めても壊れにくい）
- `#` で始まる行はコメントとして無視
- 文字コードは UTF-8

重要:

- このローダーは単純分割なので、一般的なCSVの `"` 引用（RFC4180）を厳密には解釈しません  
  → カンマ区切りを使う場合、本文中カンマで列ずれしやすいです。**`;` かタブ区切り推奨**。

### A. イベント行（基本）

列順（10列）:

`開始年;終了年;ラベル;label_en;ジャンル;重要度;URL;url_en;注釈;note_en`

メモ:

- 終了年は空欄可。継続は `ongoing` 可
- ジャンルは `・` または `|` 区切り可（例: `AI|JAPAN`）
- 重要度は 1〜5

### B. 追加で使える行タイプ

- ジャンル定義:  
  `genre;CODE;LABEL;label_en;conjunction;[DELETE]`
- 時代区分:  
  `era;name;startYear;endYear;color;opacity;enabled;fillEnabled`
- タイトル:  
  `title;日本語タイトル;English Title`
- 説明:  
  `description;日本語説明;English Description`
- 初期作成者:  
  `initialCreator;名前`
- 貢献者:  
  `contributors;name1,name2,name3`

### C. 削除行（必要なとき）

- イベント削除: `重要度` 列に `DELETE` を入れる  
  （開始年/終了年・ラベル・ジャンルで対象特定）
- ジャンル削除: `genre` 行の6列目に `DELETE`

### D. そのまま使える最小サンプル（`;` 区切り）

```txt
# イベント（10列）
1946;;ENIAC;ENIAC;CP|WORLD;5;https://ja.wikipedia.org/wiki/ENIAC;https://en.wikipedia.org/wiki/ENIAC;初の大規模電子計算機;First large-scale electronic computer
2022;ongoing;生成AIブーム;Generative AI boom;AI|WORLD;5;https://en.wikipedia.org/wiki/Generative_artificial_intelligence;;社会実装が加速;Rapid social adoption

# ジャンル定義
genre;AI;AI;AI;;
genre;CP;コンピュータ;Computer;;
genre;WORLD;世界;World;true;

# 時代区分
era;戦後復興;1945;1955;#4169E1;0.25;true;true
era;インターネット普及;1995;2010;#32CD32;0.20;true;false

# メタデータ
title;マイ年表;My Timeline
description;個人作成の年表;Personal timeline
initialCreator;Your Name
contributors;Your Name,Collaborator A
```

---

## 4. 最低限の編集を試す（10〜15分）

次を必ず1回ずつ実行:

- 新規追加: 左カラム空白クリック → 項目作成 → 「保存」
- 編集: 既存項目を編集 → 「保存」
- 並び替え: 詳細一覧で上下入替 → 「閉じる」
- 削除: 1件削除

ローカルモードでは、上の操作時にローカルJSONが保存されます。  
初回のみ保存先選択が出る場合がありますが、以後は同じファイルへ上書きします（対応ブラウザ）。  
「セーブ（ローカル保存）」後も、設定のデータソース欄に保存先ファイル名が表示されます。

---

## 5. ローカル品質確認（5〜10分）

最低限のチェック:

- 検索で項目が引けるか
- 年・ジャンル・重要度が意図どおりか
- URLプレビューが破綻しないか
- 保存後に再読み込みして内容が残るか

推奨:

- 節目ごとにファイル複製（`_02`, `_03` など）
- 必要ならスナップショット保存も併用

---

## 6. 年表名・著作権などメタ情報を整える（5分）

年表名・著作権・ライセンス等は、最終的に JSON の `metadata` 編集が必要です。  
（画面操作だけでは完結しない項目があります）

最低限、公開前に次を確認:

- `metadata.title`（年表名）
- `metadata.copyright`
- `metadata.license` / `metadata.licenseUrl`

---

## 7. GitHub公開へ切り替える（10〜20分）

1. GitHub でリポジトリ作成（例: `my-timeline`）
2. 仕上がった `timeline_myfirst_01.json` を push
3. 次のURLで表示確認

`?datasrc=github&owner=<あなたのID>&repo=<repo名>&filePath=timeline_myfirst_01.json`

4. 問題なければ共有

必要なら `xnative_link_map.json` に `xid` を追加して短縮共有も可能。

---

## よくあるつまずき

- **Q. ローカルモードなのにGitHub保存される？**  
  → されません。ローカルJSON保存のみです。

- **Q. 保存先選択が毎回出る**  
  → 同じブラウザ/同じタブ運用を推奨。非対応環境ではダウンロード保存になります。

- **Q. まず何を完成とする？**  
  → 「追加・編集・並び替え・削除を1回ずつ実施し、再読み込みで再現できる状態」を最初の完成ラインにしてください。

---

## 次の一歩

- 詳細版: `timeline-local-to-github-guide.md`
- 全体ガイド: `users_guide.md`
