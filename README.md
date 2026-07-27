# VolputasData

Volputasのローカル専用モードで利用できる、公開サンプル用アンケートデータです。

Volputas本体とは独立したリポジトリです。必要な場所へ明示的にcloneして利用します。
個人の回答やプレイ記録はローカルにだけ保存し、この公開リポジトリへcommitしません。

## アンケート

- `gamer-preference` — ゲーム嗜好とプレイスタイル (12次元 + 15軸)
- `gamer-subtypes` — ゲーマータイプのサブタイプ判定 (5主タイプ×4 = 20タイプ)
- `gamer-emotions` — 体験の自由記述から感情傾向 (20次元) を取る
- `play-habits` — 普段のゲームプレイ習慣
- `accessibility-preferences` — ゲーム設定とアクセシビリティの好み
- `review-perspectives` — ゲームレビューで重視する観点

`gamer-preference`・`gamer-subtypes`・`gamer-emotions`は測るものごとに分けた3本
セットです。1本にまとめると80問近くなり、主タイプだけ知りたい回答者に
サブタイプ20問を強制することになるため分割しています。主タイプだけなら
`gamer-preference`だけで完結します。

定義は`surveys/<survey-id>.json`へ、整形済みJSONで保存します。ファイル名と
アンケート内の`id`は一致させてください。

任意の`category`オブジェクト（`id`・`label`・`order`）で、Volputasの
サイドバーに表示するグループと順序を指定できます。未指定のアンケートは
`General`カテゴリにまとめられます。

設問には、それが何を測るかを表す任意のタグを付けられます。付けた設問だけが
対応する分析へ寄与し、付いていない設問は回答として保存されるだけです。

- `dimension` — 12次元 (Gamer / Mechanics / Story) 分析
- `axis` — 15軸プレイスタイル分析
- `subtype` — `<主タイプ>.<サブタイプ>` 形式の20サブタイプ判定
- `scoring` — 選択肢の値ごとの -1..1 スコア（`dimension`・`axis`・`subtype`共通）
- `weight` — `freetext`設問が感情傾向ベクトルへ寄与する重み

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
