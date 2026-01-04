# AWS Serverless Portfolio Project

AWSのサーバーレスアーキテクチャを用いて構築した、個人のポートフォリオサイト（Web履歴書）プロジェクトです。
未経験からクラウドエンジニアへの転職を目指し、AWSのベストプラクティスを意識した「コスト効率」「セキュリティ」「自動化」を重視した構成で開発しています。

## 🚀 プロジェクトの目的
- 静的WebサイトホスティングからバックエンドAPI構築まで、フルスタックなAWS構築経験を積むこと。
- コンソール操作だけでなく、IaCやCI/CDを用いた現代的な開発フローを習得すること。
- **The Cloud Resume Challenge** をベースとした実践的な課題解決。

## 🏗 アーキテクチャ構成（予定）

以下の構成で開発を進めています。

![Architecture Diagram](https://img.shields.io/badge/Architecture-Serverless-orange)
*(※ここに後ほど構成図の画像を貼ります)*

1. **Frontend**: Amazon S3 (静的ホスティング) + Amazon CloudFront (CDN/HTTPS化)
2. **Backend**: AWS Lambda (Python) + Amazon DynamoDB (NoSQL)
3. **API**: Amazon API Gateway
4. **CI/CD**: GitHub Actions (フロントエンド/バックエンドの自動デプロイ)
5. **Infrastructure**: Terraform (予定)

## 🛠 使用技術・ツール

- **Cloud Provider**: AWS
- **Frontend**: HTML5, CSS3, JavaScript
- **Backend**: Python (Boto3)
- **Database**: DynamoDB
- **CI/CD**: GitHub Actions
- **Version Control**: Git / GitHub

## 📝 進捗状況 (Roadmap)

- [ ] **Phase 1**: S3バケットによる静的ウェブサイトの公開
- [ ] **Phase 2**: CloudFront + Route53によるHTTPS化・カスタムドメイン設定
- [ ] **Phase 3**: DynamoDBとLambdaによる訪問者カウンターの実装
- [ ] **Phase 4**: API Gatewayとフロントエンドの統合
- [ ] **Phase 5**: GitHub ActionsによるCI/CDパイプライン構築

## 🔗 リンク
- 公開サイトURL: (後ほど記載)

## 👨‍💻 Author
**Automotive Engineering Manager | CS Master's Degree**
* Currently based in USA (Global Assignment).
* Bridging the gap between Automotive Engineering and Cloud/SDV technologies.