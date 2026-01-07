# Serverless Portfolio on AWS

AWS CloudFormation を用いて構築した、完全サーバーレスアーキテクチャのポートフォリオサイトです。
インフラのコード化 (IaC) から CI/CD パイプラインによる自動デプロイまで、モダンな開発フローを採用しています。

## 🏗 Architecture (構成図)

![Architecture Diagram](./architecture.png)

### データの流れ
1.  **Frontend**: ユーザーは **Amazon CloudFront** (CDN) 経由で **S3** 上の静的サイトにアクセスします (HTTPS)。
2.  **Backend**: サイト内のJavaScriptが **API Gateway** を呼び出します。
3.  **Compute**: **AWS Lambda** (Python) がリクエストを処理し、**DynamoDB** の訪問者カウンターを更新・取得します。
4.  **DevOps**: **GitHub Actions** により、コードをプッシュするだけでインフラとアプリケーションが自動デプロイされます。

## 🛠 Tech Stack (使用技術)

| Category | Technology |
| --- | --- |
| **Infrastructure** | AWS CloudFormation (IaC) |
| **Frontend** | HTML5, CSS3, JavaScript, Amazon S3, Amazon CloudFront |
| **Backend** | AWS Lambda (Python), Amazon API Gateway |
| **Database** | Amazon DynamoDB |
| **CI/CD** | GitHub Actions |
| **Security** | IAM (Least Privilege), OAC (Origin Access Control) |

## 🚀 Features (特徴)

* **Infrastructure as Code (IaC)**: サーバー構成、ネットワーク、権限周りをすべてYAMLコードで管理。
* **Serverless**: サーバー管理不要のフルマネージドサービスのみで構成し、ランニングコストを最小化。
* **CI/CD Pipeline**: GitHubへのPushをトリガーに、AWSへのデプロイを完全自動化。
* **Visitor Counter**: LambdaとDynamoDBのアトミックカウンタを使用した、スケーラブルなアクセスカウンター機能。

## 👤 Author

* **[Mitsuhiro Demura]**
* GitHub: [@shockpan-web]

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