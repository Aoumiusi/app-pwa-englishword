# Linguist Card

英語単語学習フラッシュカード PWA。自作のJSON/CSVファイルを読み込んで学習できます。

## データ形式

### JSON

配列形式で単語データを記述します。

```json
[
  {
    "word": "ephemeral",
    "phonetic": "ɪˈfem.ər.əl",
    "meaning": "はかない、短命な",
    "example": "The beauty of cherry blossoms is ephemeral.",
    "example_ja": "桜の美しさははかないものだ。"
  }
]
```

| フィールド | 型 | 必須 | 説明 |
|---|---|---|---|
| `word` | string | ✓ | 英単語 |
| `phonetic` | string | | IPA発音記号 |
| `meaning` | string | ✓ | 日本語の意味 |
| `example` | string | | 英語例文 |
| `example_ja` | string | | 例文の日本語訳 |

日本語フィールド名（`英単語`, `発音記号`, `意味`, `例文`, `例文和訳`）も使用できます。

### CSV

1行目はヘッダー行として扱われます。

```csv
word,phonetic,meaning,example,example_ja
resilient,rɪˈzɪl.i.ənt,回復力のある,She is remarkably resilient in the face of adversity.,彼女は逆境に対して驚くほどの回復力を持っている。
```

カラム順序はヘッダー名で判断されるため、順不同でも動作します。`phonetic` / `example` / `example_ja` は省略可能です。

## 機能

- カードをタップ/クリックで表裏を反転
- 🔊 ボタンで英単語の発音を再生（Web Speech API）
- ‹ › ボタンまたはキーボードの ← → キーでカード移動
- 🔀 シャッフル機能
- PWA対応（オフライン動作・ホーム画面追加）
- IndexedDBによるデータ永続化
