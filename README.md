# VolputasData

Volputasのローカル専用モードで利用できる、公開サンプル用アンケートデータです。

## アンケート

- `gamer-preference` — ゲーム嗜好とプレイスタイル
- `play-habits` — 普段のゲームプレイ習慣
- `accessibility-preferences` — ゲーム設定とアクセシビリティの好み
- `review-perspectives` — ゲームレビューで重視する観点

定義は`surveys/<survey-id>.json`へ、整形済みJSONで保存します。ファイル名と
アンケート内の`id`は一致させてください。

任意の`category`オブジェクト（`id`・`label`・`order`）で、Volputasの
サイドバーに表示するグループと順序を指定できます。未指定のアンケートは
`General`カテゴリにまとめられます。

## 回答状態

Volputasは`answers/<Name>/<survey-id>.json`の存在を正本として扱います。
Nameはデータリポジトリの`git config user.name`から自動設定し、
アンケートごとに`answered`または`unanswered`を表示します。状態だけを表す
別ファイルは作りません。

実際の回答にはGit Author情報が含まれるため、この公開サンプルリポジトリでは
`answers/`以下の回答ファイルを`.gitignore`で除外しています。

## 体験データとペルソナ分析

ローカル版Volputasは、同じNameを使って次のデータを保存します。

- `gameplay/<Name>/<record-id>.json` — ゲームプレイ情報とやりこみ度
- `voices/<Name>/<record-id>.json` — ゲーム全体・コンテンツ別の感想
- `emotion-curves/<Name>/<record-id>.json` — 動画時刻に紐づく感情とメタ情報
- `media/<Name>/screenshots/` — ゲームプレイの根拠画像
- `media/<Name>/videos/` — 感情曲線のゲームプレイ動画
- `analysis/<Name>/persona.json` — 入力データから生成した最新のペルソナ分析

ペルソナ分析は入力データ全体のフィンガープリントを保存します。前回分析後に
アンケート回答または体験データが更新された場合だけ再計算されます。

これらにはGit Author情報や個人のプレイ記録が含まれるため、この公開リポジトリ
では`.gitignore`の対象です。公開可能な形式例は`examples/profile-data/`に
匿名のサンプルとして収録しています。個人用リポジトリで記録を共有する場合は、
共有範囲を確認した上で必要なignore設定だけを変更してください。
