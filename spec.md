# 英語学習PWAアプリ「Linguist Card」実装仕様書

## 1. プロジェクト概要
ユーザーが自作のJSON/CSV単語リストを読み込み、音声と発音記号を確認しながら学習できる、シンプルで高速なフラッシュカード型PWA。

## 2. 技術スタック
* **Frontend:** HTML5, CSS3, Vanilla JavaScript (フレームワークなし、またはReact/Vue)
* **Font:** Noto Sans (Google Fonts) ※IPA記号対応
* **Audio:** Web Speech API (SpeechSynthesis)
* **Storage:** IndexedDB または LocalStorage (インポートデータの永続化)
* **Architecture:** PWA (Service Workerによるオフライン対応)

## 3. 機能要件

### 3.1 単語データ管理
* **JSON/CSVインポート:**
    * ユーザーがローカルのJSONまたはCSVを選択し、アプリ内に取り込む機能。
    * データ形式例：`{ "word": "string", "phonetic": "string", "meaning": "string", "example": "string" }`
* **データ永続化:**
    * 一度インポートしたデータはブラウザを閉じても保持されること。

### 3.2 フラッシュカードUI
* **表面 (Front):**
    * 英単語（大きく中央に配置）
    * 発音記号（IPA、Noto Sansで正しく表示）
* **裏面 (Back):**
    * 日本語の意味
    * 例文 (Example sentence)
    * 発音ボタン (🔊 アイコン)
* **アニメーション:**
    * CSS `transform` を使用したスムーズな3D回転。
* **ナビゲーション:**
    * 「次へ」「前へ」ボタン、およびキーボードの左右キーによる操作。

### 3.3 音声出力
* `window.speechSynthesis` を使用し、裏面のボタン押下時に英単語を発音。
* 言語は `en-US` 固定、速度は `0.9` 程度に設定。

### 3.4 PWA対応
* `manifest.json` の作成（アプリアイコン、テーマカラーの設定）。
* `service-worker.js` によるアセットのキャッシュ（オフライン動作）。

## 4. デザインガイドライン
* **テーマ:** 清潔感のあるミニマルデザイン（白・薄いグレー・アクセントに青）。
* **タイポグラフィ:**
    * 英単語: Noto Sans, Bold, 32px以上。
    * 発音記号: Noto Sans, Regular, 18px, 色: #666。
* **レスポンシブ:** モバイルファースト。スマホの縦持ちで最適に表示されること。

## 5. 画面遷移 / 構成
1.  **メイン画面:** フラッシュカード表示部。データがない場合は「ファイルを読み込んでください」というプレースホルダーを表示。
2.  **管理メニュー:** インポートボタン、および学習データのクリアボタン。

