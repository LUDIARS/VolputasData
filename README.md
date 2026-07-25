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

Volputasは`<GitHub名>/responses/<survey-id>.json`の存在を正本として、
アンケートごとに`answered`または`unanswered`を表示します。状態だけを表す
別ファイルは作りません。

実際の回答にはGit Author情報が含まれるため、この公開サンプルリポジトリでは
ルート直下の回答ファイルを`.gitignore`で除外しています。
