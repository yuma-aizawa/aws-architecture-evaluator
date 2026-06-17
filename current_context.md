# IaCベースのクラウド構成評価・学習支援システム（ゼミ研究）

## 研究概要

本研究は、Infrastructure as Code（IaC）を対象に、クラウド構成をデプロイ前に静的解析し、AWS Well-Architected FrameworkおよびCSA CCM（Cloud Controls Matrix）に基づいて評価・学習支援を行うシステムの設計・実装を目的とする。

対象は主にTerraformで記述されたIaCコードとし、ユーザーが制御可能な範囲（Customer Responsibility）におけるクラウド設計の良し悪しを自動評価する。

---

## 2. 研究目的

- IaCコードからクラウド構成の品質を自動評価する
- 初学者がクラウド設計のトレードオフ（コスト・可用性など）を学習できる環境を提供する
- 実環境へのデプロイを必要とせず、設計段階で評価を完結させる
- AWS Well-Architected FrameworkおよびCSA CCMを統合した評価モデルを構築する

---

## 3. 評価対象

### 入力
- Terraform（IaC）コード

### 評価範囲
- ユーザー責任範囲（Customer Responsibility）内の設定・設計要素

### 評価対象外
- 動的運用ログ
- 実行中リソースの状態
- クラウドベンダー管理領域（AWS責任範囲）

---

## 4. 参考フレームワーク（評価基準）

### 4.1 AWS Well-Architected Framework

クラウド設計のベストプラクティスを定義するフレームワーク。

- 運用上の優秀性（Operational Excellence）
- セキュリティ（Security）
- 信頼性（Reliability）
- パフォーマンス効率（Performance Efficiency）
- コスト最適化（Cost Optimization）
- 持続可能性（Sustainability）

※本研究ではAWS Well-Architected Toolそのものは使用せず、概念モデルとして利用する

---

### 4.2 CSA CCM / CAIQ

Cloud Security Alliance（CSA）が提供するクラウドセキュリティ評価体系。

- CCM（Cloud Controls Matrix）
  - クラウド統制の体系的マトリクス
- CAIQ（Consensus Assessments Initiative Questionnaire）
  - CCMに対応する評価質問群

本研究では以下の目的で利用する：

- W-Aのセキュリティ観点の補強
- IaCレベルでのセキュリティ統制の詳細化
- より粒度の高い評価軸の導入

---

## 5. 既存ツールとの比較・差別化

既存のIaC解析ツールは主に単一観点の検出器として機能する。

### 主要ツール

- tfsec（Terraform security scanner）
- Infracost（IaCコスト見積もり）
- TFLint（構文・ベストプラクティスチェック）
- Checkov / Terrascan（ポリシー検査）

---

### 比較表

| 項目 | 既存ツール | 本研究 |
|------|------------|--------|
| 評価観点 | セキュリティ・コストなど単一 | 複数観点の統合評価 |
| フィードバック | 警告・検出結果のみ | 教育的説明＋改善提案 |
| 解析手法 | ルールベース検出 | フレームワーク統合型評価 |
| 目的 | 脆弱性検出 | 学習支援・設計理解 |

---

## 6. 研究の基本設計思想

本研究は以下の3層構造で構成される。

### 6.1 解析層

- IaCコードを解析
- tfsec / Infracostなど既存ツールを利用
- 構成要素・設定値を抽出

---

### 6.2 評価層（翻訳層）

- AWS Well-Architected FrameworkおよびCSA CCMに基づく評価モデル
- IaCの構成情報を意味的に変換
- スコアリングおよびトレードオフ評価を実施

---

### 6.3 教育・対話層

- 評価結果を自然言語で説明
- トレードオフ（例：可用性向上 → コスト増加）を可視化
- 学習者向け改善提案を生成

---

## 7. 設計方針

- 静的解析中心設計
  - 実環境・ログ等の動的情報に依存しない

- 責任共有モデル準拠
  - ユーザーが制御可能な範囲のみ評価対象とする

- トレードオフの可視化
  - 複数評価軸間の関係性を明示する

---

## 8. 現在の研究フェーズ

- 先行技術調査：完了
- 評価設計フェーズ：進行中
- 実装フェーズ：未着手（または初期段階）

---

## 9. 主要タスク

- AWS Well-Architected各項目のIaC観測可能性分解
- CSA CCM / CAIQ項目のIaC対応付け
- 評価スコアリングモデル設計
- 教育用フィードバック生成エンジン設計
- CLIまたはWebプロトタイプ実装

---

## 10. 研究の中核定義

本研究は、AWS Well-Architected FrameworkおよびCSA CCMを基に、IaC静的解析結果を統合し、実環境構築不要かつ設計段階でクラウド構成を評価・学習支援するシステムの設計・実装を目的とする。
