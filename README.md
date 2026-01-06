# AWS Serverless Portfolio Project

AWS CloudFormation (IaC) を使用して構築した、サーバーレスアーキテクチャのポートフォリオサイトです。
静的Webサイトのホスティングから、訪問者数カウンター（バックエンドAPI）までをすべてコードで管理・自動構築しています。

## 🏗 Architecture

![AWS Serverless Architecture](./system.png)

### Frontend
- **Amazon S3**: 静的ウェブサイトホスティング（HTML/CSS/JSの配置）
- **Amazon CloudFront**: CDNによる高速配信とHTTPS化（SSL/TLS終端）

### Backend
- **Amazon API Gateway**: REST APIのエンドポイント提供
- **AWS Lambda (Python)**: DynamoDBへのアクセスロジック、環境変数による疎結合設計
- **Amazon DynamoDB**: 訪問者数のカウントデータ（NoSQL）、オンデマンドモード

## 🚀 Features

- **Infrastructure as Code (IaC)**: すべてのリソースを `template.yaml` 一つで定義・管理。
- **Serverless**: サーバー管理不要のマネージドサービスのみで構成し、ランニングコストを最適化。
- **HTTPS & CDN**: CloudFrontを使用したセキュアで高速なコンテンツ配信。
- **Atomic Counter**: DynamoDBのアトミック操作を使用した、整合性の取れたアクセスカウンター。
- **CORS Support**: 異なるドメイン（CloudFront -> API Gateway）間の通信を許可する適切なヘッダー設定。

---

## 📚 Technical Deep Dive (学習メモ)

プロジェクト構築中に直面した課題や、技術的な詳細についての解説メモです。

### 1. CloudFormation & YAML
- **YAMLのインデント**: リストやプロパティの階層構造（スペースの数）が厳密に求められる。特に `Policies` や `Resources` のネストでエラーになりやすい。
- **組み込み関数**:
  - `!Ref`: パラメータやリソースの物理IDを参照。
  - `!GetAtt`: リソースの属性（ARNやURLなど）を取得。
  - `!Sub`: 変数を文字列の中に埋め込む。
  - `!Split` / `!Select`: S3のURLからドメイン名だけを抽出する際など、文字列操作に使用。

### 2. AWS CLI & JMESPath
AWS CLIの出力結果から特定の値を抽出するために **JMESPath** を使用。
例：作成されたAPIのURLを取得するコマンド
```bash
aws cloudformation describe-stacks \
    --stack-name MyPortfolioStack \
    --query "Stacks[0].Outputs[?OutputKey=='ApiEndpoint'].OutputValue" \
    --output text