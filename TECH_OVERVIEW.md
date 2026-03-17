# チャリティーサンタ Web技術概要

NPO法人チャリティーサンタのWebのシステム構成・技術スタックをまとめたドキュメントです。

## システム構成

### 主な公開Webサイト（WordPress）

| サイト | URL |
| -------- | ----- |
| チャリティーサンタ公式 | www.charity-santa.com |
| ブックサンタ | booksanta.charity-santa.com |
| ブックサンタ オンライン書店 | bookshop.charity-santa.com |
| 作家サンタ | writer.charity-santa.com |
| シェアケーキ | sharecake.charity-santa.com |
| シェアケーキ ショップ | sharecake-shoppage.charity-santa.com |
| ファミリーメモリー | family-memory.charity-santa.com |

### Webアプリケーション（Laravel）

ECS Fargate上でLaravelアプリケーションを運用しています。

### API（Serverless）

AWS Lambda + Serverless Framework (Node.js) で構成。LINE Bot連携やKintone連携に利用。

### ランディングページ（ペライチ）

サンタクロースからの手紙(`letter`)、シェアケーキサポート(`sharecake-monthlysupport`)、シェアシネマ(`sharecinema`)、Santa Mother's Dream / ブックサンタサポート(`lp`) などのサブドメインで運用。

### ブログ（Ameba Ownd）

ほくほく通信(`hokuhoku`) で運用。

## 技術スタック

### 言語・フレームワーク

| カテゴリ | 技術 |
| ---------- | ------ |
| CMS | WordPress |
| Webアプリ | Laravel (PHP) |
| API | Node.js (Serverless Framework) |
| Kintoneカスタマイズ | TypeScript |
| 業務自動化 | Google Apps Script (JavaScript) |
| インフラ管理 | Terraform |

### AWS

| カテゴリ | サービス | 用途 |
| ---------- | ---------- | ------ |
| コンピューティング | ECS Fargate | WordPress・Laravelのコンテナ実行 |
| コンピューティング | Lambda | サーバーレスAPI |
| データベース | Aurora MySQL 8.0 Serverless v2 | RDB |
| ストレージ | S3 | 静的ファイル・ログ・Terraform state |
| ストレージ | EFS | WordPressコンテナ間の共有ファイルストレージ |
| ストレージ | ECR | コンテナイメージレジストリ |
| ネットワーク | VPC | 3AZ構成（public / private / database subnets） |
| ネットワーク | ALB | Application Load Balancer |
| ネットワーク | Route 53 | DNS管理 |
| ネットワーク | CloudFront | CDN配信 |
| セキュリティ | WAF | PHP/WordPress専用マネージドルール |
| セキュリティ | ACM | SSL/TLS証明書 |
| セキュリティ | IAM Identity Center | SSO・アクセス管理 |
| セキュリティ | Secrets Manager | 機密情報管理 |
| 監視 | CloudWatch | メトリクス・ダッシュボード・アラーム |
| 監視 | CloudWatch Synthetics | 外形監視（Canary） |
| 監査 | CloudTrail | API操作の監査ログ |

### SaaS・外部サービス

| サービス | 用途 |
| ---------- | ------ |
| Xserver | WordPressホスティング |
| GitHub | ソースコード管理・チケット管理 |
| Kintone | 業務データ管理（CRM的利用） |
| Google Workspace | メール・ドキュメント |
| SendGrid | メール配信 |
| Pay.jp | 決済 |
| LINE | Bot連携・通知 |
| ペライチ | ランディングページ |
| Ameba Ownd | ブログ |

### 開発ツール・CI/CD

| ツール | 用途 |
| -------- | ------ |
| GitHub Actions | CI/CD（ビルド・デプロイ自動化） |
| Docker / Docker Compose | ローカル開発・本番コンテナ |
| Terraform | インフラ・GitHubのIaC管理 |
| Claude Code | AIコードレビュー |
