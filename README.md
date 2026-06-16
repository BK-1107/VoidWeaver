<div align="center">
  <h1>Void Weaver</h1>
  <p><b>画像を編集可能な創作構造へ分解し、新しい視覚世界を編み上げる。</b></p>
  <a href="LICENSE"><img src="https://img.shields.io/badge/license-MIT-blue.svg?style=flat-square" alt="License"></a>
  <img src="https://img.shields.io/badge/frontend-React%2018-61dafb?style=flat-square" alt="React">
  <img src="https://img.shields.io/badge/backend-Spring%20Boot-6db33f?style=flat-square" alt="Spring Boot">
  <img src="https://img.shields.io/badge/API-Gemini%20%2B%20NovelAI-8b5cf6?style=flat-square" alt="AI Engines">
</div>
<br/>

> Rewrite the World Protocol Active

[中文](docs/README_CN.md) | [English](docs/README_EN.md)

<div align="center">
  <img src="docs/assets/Snipaste_2026-06-17_00-42-28.png" width="1000" alt="Gemini Hackathon Google DeepMind">
  <p><b>Gemini Hackathon 参加作品</b></p>
</div>

<br/>

<div align="center">
  <img src="https://img.youtube.com/vi/aGwaFVipMss/maxresdefault.jpg" width="1000" alt="Void Weaver デモ動画">
  <p><b>トップページプレビュー</b></p>
</div>

## Why

AI 画像生成ツールは増え続けていますが、多くのツールは創作プロセスを 1 つの prompt に押し込めています。ユーザーが文字を入力し、モデルが画像を返す。その途中にある構造は見えにくく、安定して制御することも難しいままです。

Void Weaver が解きたいのは別の問題です。**1 枚の参照画像を、編集・ロック・重み付け・反復できる創作構造へ変換すること。**

Void Weaver は参照画像を読み取り、スタイル、被写体、ポーズ、衣装、背景、構図、雰囲気などのモジュールに視覚情報を分解します。ユーザーはそれらをレイヤーのように編集できます。タグを強める、不要な説明を削除する、人物のポーズを固定して背景だけを変える、または自然言語で AI に次の変更を指示することができます。

つまり Void Weaver は「prompt を入力して結果を待つ」だけの一方向ツールではありません。現実を解析し、それから現実を書き換えるための AI 画像制作コンソールです。

## 使い方

### 1. 生成環境を設定

左側の設定サイドバーに Gemini API Key を入力し、生成エンジンを選択します。NovelAI はアニメ調やスタイル化された生成に向いており、Google Imagen は写実的な生成や幅広い創作に向いています。

### 2. 画像をアップロード

Source Material エリアに画像をドラッグします。この画像は解析、画像から画像への生成、スタイル抽出の基礎になります。

### 3. 画像を解析

DECIPHER をクリックすると、システムが Gemini を呼び出して画像を分析し、衣装、背景、動作などの構造化モジュールを生成します。解析結果はさらに微調整できます。

<div align="center">
  <img src="docs/assets/Snipaste_2026-06-17_00-05-32.png" width="900" alt="画像解析の例">
</div>

### 4. モジュールを編集

解析されたモジュールをさらに調整できます。

- 不要なタグを削除する
- タグの重みを強める、または弱める
- 変更したくないモジュールをロックする
- 新しい視覚説明を手動で追加する

### 5. 画像から画像を生成

下部の入力欄に自然言語の指示を入力します。例：

```text
服を赤いセーターに変更し、眠っているように両目を閉じた表情にして、斜め45度の半身構図にする
```

Void Weaver はロック状態に基づいて、変更が許可されたモジュールだけを更新します。

MANIFEST をクリックすると、現在のモジュールを最終 prompt に組み立て、選択したエンジンで新しい画像を生成します。

<div align="center">
  <img src="docs/assets/Snipaste_2026-06-17_00-17-00.png" width="900" alt="画像から画像を生成する例">
</div>

### 6. 直接画像を生成

画像から画像を生成するだけでなく、複数画像を組み合わせたり、自分の構想から直接画像を生成したりできます。生成前にキャンバスサイズ、生成ステップ、モデル種類などのパラメータを調整できます。

<div align="center">
  <img src="docs/assets/Snipaste_2026-06-17_00-21-10.png" width="900" alt="直接画像生成の例">
</div>

### 7. Deep Thinking

Deep Thinking は構造草図から生成を開始し、各ステップで視覚的なレビューを行います。最終出力をより安定して美しくしながら、生成過程も確認できます。

<div align="center">
  <img src="docs/assets/Snipaste_2026-06-17_00-18-50.png" width="900" alt="Deep Thinking の例">
</div>

## ワークフロー

```text
Source Image
  -> Decipher
  -> Prompt Modules
  -> Lock / Weight / Refine
  -> Manifest
  -> New World
```

## 機能

| 機能 | 使用場面 | 内容 |
| :--- | :--- | :--- |
| 画像解析 | 参照画像から視覚構造を抽出したいとき | Gemini を使って画像を編集可能な複数モジュールへ分解する |
| モジュール型 Prompt | prompt が長く、乱雑で、管理しづらいとき | Style、Subject、Pose、Costume、Background などのモジュールに分割する |
| タグ重み | 特定の視覚要素を強めたい、または弱めたいとき | 個別タグに重みを設定し、生成傾向に影響を与える |
| モジュールロック | 主体を壊さず一部だけ変更したいとき | 指定モジュールをロックし、AI が未ロック部分だけを変更する |
| 自然言語リファイン | 一文で画面を調整したいとき | 指示文を使って関連モジュールを書き換える |
| 2 種類の生成エンジン | 異なる生成スタイルが必要なとき | NovelAI と Google Imagen の 2 ルートに対応する |
| Deep Thinking | 生成前により強い自己チェックを入れたいとき | 草図生成、視覚レビュー、修正指示を経て最終画像を生成する |
| 履歴と回放 | 複数の生成結果を比較したいとき | 生成履歴を保存し、Deep Thinking のログを確認できる |

## 技術設計

Void Weaver はフロントエンドとバックエンドを分離した構成です。

| 層 | 技術 | 説明 |
| :--- | :--- | :--- |
| フロントエンド | React 18 / TypeScript / Vite | インタラクティブな創作ワークステーションを構築 |
| 状態管理 | Zustand | 画像、モジュール、生成履歴、UI 状態を管理 |
| スタイル | TailwindCSS | ダークでモジュール化されたコンソール風 UI を構築 |
| バックエンド | Spring Boot 3.2.1 | 画像解析、リファイン、生成 API を提供 |
| AI 解析 | Gemini | 画像を構造化モジュールへ変換 |
| AI 生成 | NovelAI / Google Imagen | 最終 prompt から画像を生成 |

## 環境要件

- Java 17+
- Node.js 18+
- Maven 3.8+
- Gemini API Key
- NovelAI API Token、任意
- Google Cloud Credentials、任意

## License

MIT License. Feel free to use, modify, and build on Void Weaver.
