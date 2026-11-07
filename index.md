サイバーセキュリティ関連の公開文書について試行的に日本語へ訳出した参考資料と、脆弱性対応を手助けする小さなツールを公開しています。

日本語訳は、いずれも **非公式の翻訳** です。内容に疑義がある場合は、必ず各サイトに記載の原文を参照してください。

## 日本語訳

### GCVE BCP 日本語訳(gcve-bcp-ja)

<https://lex0xf0c.github.io/gcve-bcp-ja/>

[GCVE](https://gcve.eu/) が公開している BCP(Best Current Practice)文書を日本語に訳出したものです。脆弱性の取扱いと開示の実践ガイド(BCP-02)や、GCVE 脆弱性形式(BCP-05)、KEV アサーションの形式(BCP-07)などを収録しています。

- リポジトリ: <https://github.com/Lex0xF0C/gcve-bcp-ja>

### ENISA Secure by Design and Default Playbook 日本語訳(enisa-sbd-playbook)

<https://lex0xf0c.github.io/enisa-sbd-playbook/>

ENISA(欧州連合サイバーセキュリティ局)が公開している「Secure by Design / Secure by Default」プレイブック集を日本語に訳出したものです。「セキュア・バイ・デザイン」(アーキテクチャの基盤、運用の完全性)と「セキュア・バイ・デフォルト」(デフォルトのハードニング、ガイド付きの保護)の全 22 本のプレイブックで構成されています。

- リポジトリ: <https://github.com/Lex0xF0C/enisa-sbd-playbook>

### 欧州委員会によるサイバーレジリエンス法に関するFAQ第14版 日本語訳
<https://lex0xf0c.github.io/KnowledgeBase/EU-Cyber-Resilience-Act/FAQs_on_the_CRA_v14.ja.html>

### ソフトウェア部品表 (SBOM) に関する ENISA 技術アドバイザリ (ENISA Technical Advisory for Software Bill of Materials)
<https://lex0xf0c.github.io/KnowledgeBase/EU-Cyber-Resilience-Act/ENISA-Technical-Advisory-for-SBOM-ja.html>

### security.txt、CVD ポリシー、セキュリティアドバイザリに関する ENISA 技術アドバイザリ (ENISA Technical Advisory on security.txt, CVD Policies and Security Advisories)
<https://lex0xf0c.github.io/KnowledgeBase/EU-Cyber-Resilience-Act/ENISA_technical_advisory_security_txt_cvd_policies_advisories_ja.html>

### 日本語訳についての注意

- いずれの翻訳も、原文の作成者が作成・承認・推奨したものではありません。
- 原文のライセンスに従い、翻訳版も同じライセンスの下で公開しています。ライセンスと帰属表示の詳細は、各サイトをご覧ください。
- 翻訳に誤りがある場合、その責任は翻訳者にあります。

## Secriptorium（セクリプトリウム）: 脆弱性開示・CRA適合支援ツール

Secriptorium（セクリプトリウム）は、デジタル要素を含む製品の開発者、中小企業（SME）、および PSIRT（Product Security Incident Response Team）担当者が、脆弱性情報やセキュリティ関連文書をブラウザ上だけで安全かつスピーディーに作成・管理できる、サーバーレス型の静的Webユーティリティです。

---

### 1. プロジェクト基本情報

- **名称**: Secriptorium（セクリプトリウム）
- **Webサイト (Live Demo)**: <https://lex0xf0c.github.io/secriptorium/>
- **GitHub リポジトリ**: <https://github.com/Lex0xF0C/secriptorium>
- **ライセンス**: MIT License
- **開発・デプロイ**: Vite + Vue 3 + TypeScript（GitHub Actions による自動ビルド・デプロイ）

---

### 2. 開発思想とセキュリティ・アーキテクチャ

Secriptorium は、未公開の脆弱性情報や製品の設計データ（SBOM等）を扱うツールの性質上、**「Static. Client-side. Nothing leaves your browser.（ブラウザ完結・データ送出ゼロ）」** を絶対原則として構築されています。

1. **完全クライアントサイド処理**
   - データベースやバックエンドサーバーを一切使用しません。入力されたテキストや生成された JSON / Markdown データは、すべて利用者のブラウザ（JavaScript / TypeScript）内でのみ処理されます。
2. **厳格な Content Security Policy (CSP)**
   - 外部ネットワークへの通信を遮断（`connect-src 'none'`）し、外部スクリプト、外部スタイルシート、CDN 依存を完全に排除しています。
3. **安全な DOM 描画**
   - クロスサイトスクリプティング（XSS）等の危険を防止するため、`v-html` や `innerHTML` を一切使用せず、プレーンテキストとして安全に描画します。

---

### 3. 主要機能ハイライト

Secriptorium は、脆弱性の発見・報告受付から是正・影響評価・公開・適合性証明に至るまで、脆弱性管理ライフサイクル全体をカバーする以下の機能を提供します。

#### 3.1 脆弱性アドバイザリ作成機能 (Advisory Mode)
- **マルチフォーマット同時出力**: WEB掲載用の **Markdown** 文書と、機械処理可能な **CSAF 2.0 (JSON)** 仕様準拠データをリアルタイムで同時生成します。
- **入力アシスト & プリセット**: CWE（共通脆弱性タイプ）を選択するだけで概要・脅威文言が自動入力されるほか、概要、検証手順、対策、回避策、謝辞、連絡先の定型文をワンタップで挿入できます。
- **バリデーション警告**: CSAF 2.0 規格で必須とされる項目（発行者名、発行者URL、CVSSベクター等）の不足を画面上でリアルタイムに通知します。

#### 3.2 CVSS v3.x グラフィカル計算機 (CVSS Calculator Mode)
- **基本スコア & 深刻度自動判定**: CVSS v3.0 および v3.1 に対応し、基本スコアと深刻度（Critical, High, Medium, Low, None）を即時算出します。
- **ベクターパース & 逆引き**: JVN や NVD 等に掲載されているベクター文字列（`CVSS:3.1/AV:N/...`）を貼り付けるだけで、各メトリック選択ボタンへ自動反映されます。
- **攻撃シナリオプリセット**: RCE（リモートコード実行）、XSS/フィッシング、LAN限定、ローカル管理者権限などの代表的シナリオをワンタップで試行・適用できます。

#### 3.3 SBOM / VEX 作成支援機能 (SbomMode & VexMode)
- **Excel/TSV スプレッドシート一括コピペインポート**: 大量のソフトウェア部品リストを Excel や Google スプレッドシートからタブ区切り（TSV）で一括で取り込み・編集できます。
- **PURL 自動生成**: エコシステム（npm, PyPI, Maven, Go, generic等）とコンポーネント名・バージョンから Package URL (PURL) を自動組み立てします。
- **標準規格出力**: **CycloneDX 1.6 JSON**（SBOM および VEX）と **CSAF 2.0 VEX JSON** の相互出力に対応します。

#### 3.4 security.txt (RFC 9116) 作成機能 (SecurityTxtMode)
- **RFC 9116 準拠**: 脆弱性報告窓口（Contact）、有効期限（Expires - ISO 8601）、暗号化キー（Encryption）、謝辞（Acknowledgments）、推奨言語（Preferred-Languages）、ポリシー URL（Policy）などを安全に作成します。
- **即時エクスポート**: ワンクリックでのクリップボードコピーおよび `security.txt` ファイルの直接ダウンロードが可能です。

#### 3.5 CVD（協調的脆弱性開示）ポリシー作成機能 (CvdPolicyMode)
- **国際標準準拠**: ISO/IEC 29147 や ENISA ガイドラインに準拠した組織向け脆弱性開示ポリシーを対話的に作成できます。
- **クイックセットアップ**: 中小企業向け標準、大手/PSIRT向け、OSSプロジェクト向けなどの事前定義プリセットを用意しています。

#### 3.6 CVD プロセス管理 & タイムライン生成機能 (CvdProcessMode)
- **ライフサイクル追跡**: 受領・初動対応 $\rightarrow$ 技術検証・パッチ作成 $\rightarrow$ 調整・公表準備 $\rightarrow$ 修正公開・情報共有の 4 フェーズ全ステップをステップ式チェックリストで管理します。
- **進捗レポート出力**: 案件の進捗率（%）や完了マイルストーンを反映した Markdown 形式の進捗レポートおよびバックアップ用 JSON をワンクリックで出力します。

#### 3.7 セキュア・バイ・デザイン 最低限の証跡 (Minimum Evidence) アテステーション機能 (SbdAttestationMode)
- **ENISA Playbook 準拠**: ENISA『セキュア・バイ・デザイン／デフォルト プレイブック』（Playbook 4.13, 4.14, 第5章）に基づき、製品のセキュリティ品質を立証する「最低限の証跡（Minimum Evidence）」を網羅的に検証します。
- **CDXA アテステーション出力**: 人間が読める **Markdown 証跡報告書** と同時に、欧州監査・顧客提出用の機械可読 **CycloneDX 1.6 CDXA (Declarations) JSON** を自動生成します。

---

### 4. 欧州 CRA（サイバーレジリエンス法）・ENISA 適合ロードマップ

Secriptorium は、欧州にデジタル要素を含む製品を輸出・展開する製造担当者や中小企業が、CRA（Cyber Resilience Act）附属書 I に定める法的要件を満たせるよう、以下の 4 ステップガイド（CraGuide）を提供しています。

| ステップ | CRA 該当要件 | 作成アーティファクト | 担当モード |
| :--- | :--- | :--- | :--- |
| **Step 1: 報告窓口の公開** | 附属書 I 第 II 部 (6) 脆弱性報告窓口 | `security.txt` (RFC 9116) | `SecurityTxtMode` |
| **Step 2: CVD 方針の策定** | 附属書 I 第 II 部 (5) CVD ポリシー | CVD ポリシー文書 (.md) | `CvdPolicyMode` |
| **Step 3: 部品表 (SBOM) 整備** | 附属書 I 第 II 部 (1) コンポーネント特定 | SBOM (CycloneDX 1.6 JSON) | `SbomMode` |
| **Step 4: 脆弱性対応と情報公開** | 附属書 I 第 II 部 (2), (4) 修正・周知 | 進捗レポート / VEX / アドバイザリ | `CvdProcessMode` / `VexMode` / `AdvisoryMode` |

---

### 5. 出力規格 & 技術フォーマット

- **Markdown**: WEBポータル掲載用（アドバイザリ、CVDポリシー、進捗レポート、証跡報告書）
- **CSAF 2.0 (Common Security Advisory Framework)**: Profile 4 (Security Advisory) & Profile 5 (VEX) JSON
- **CycloneDX 1.6**: SBOM, VEX, および CDXA (CycloneDX Attestations) JSON
- **RFC 9116**: security.txt プレーンテキスト

---

### 6. 免責事項 & ライセンス

- **ライセンス**: [MIT License](https://github.com/Lex0xF0C/secriptorium/blob/main/LICENSE) © 2026 Lex0xF0C
- **免責事項**: 
  - 本ツールは文書作成およびフォーマット変換の補助ユーティリティです。公表の可否、記載内容の正確性、CVSS 評価の妥当性は利用者が最終判断してください。
  - 生成された CSAF 2.0 や CycloneDX データを公式に運用・公開する前に、公認の検証ツール（Secvisogram 等）による最終検証および社内（法務・広報・PSIRT等）の確認を受けることを推奨します。
  - CVSS は FIRST.Org, Inc. が所有・管理する登録商標であり、規定の条件に基づき使用しています。


## その他のツール
### Incident Chronology Studio（クロノロジー作成支援ツール）

<https://lex0xf0c.github.io/incident-chronology-studio/>

サイバーインシデントを時系列で整理する「クロノロジー」の作成のための支援ツールです。

- リポジトリ: <https://github.com/Lex0xF0C/incident-chronology-studio>
- ライセンス: MIT

### lite-advisory-maker(脆弱性アドバイザリ作成ツール)

<https://lex0xf0c.github.io/lite-advisory-maker/>

製品の脆弱性アドバイザリを、Markdown 形式で作成するための小さなツールです。CVSS v3.1 基本値の計算、定型文、公開前チェックを備え、日本語・英語の表示に対応しています。ブラウザの中だけで動作し、入力内容を外部へ送信しません。実験・試行レベルのツールであり、不具合が含まれている可能性があります。

- リポジトリ: <https://github.com/Lex0xF0C/lite-advisory-maker>
- ライセンス: MIT

### 脆弱性開示プロセス体験ツール(CVD_Role-play_RPG)

<https://lex0xf0c.github.io/tools/CVD_Role-play_RPG/index.html>

### 脆弱性開示コミュニケーション文面サポートツール

<https://lex0xf0c.github.io/tools/Communication_Support/index.html>

### ツールについての注意

- 本ツールは文面づくりの補助です。公開の可否、内容の正確性、CVSS 評価の妥当性は、利用者が判断してください。
- 無保証で提供しています。詳細は、リポジトリの LICENSE をご覧ください。

作成・翻訳: [Lex0xF0C](https://github.com/Lex0xF0C)
