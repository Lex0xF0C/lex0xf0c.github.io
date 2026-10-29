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
<https://lex0xf0c.github.io/KnowledgeBase/EU-Cyber-Resilience-Act/enisa_technical_advisory_security_txt_cvd_policies_advisories_ja_md.html>

### 日本語訳についての注意

- いずれの翻訳も、原文の作成者が作成・承認・推奨したものではありません。
- 原文のライセンスに従い、翻訳版も同じライセンスの下で公開しています。ライセンスと帰属表示の詳細は、各サイトをご覧ください。
- 翻訳に誤りがある場合、その責任は翻訳者にあります。

## ツール

### 脆弱性アドバイザリ作成ツール(lite-advisory-maker)

<https://lex0xf0c.github.io/lite-advisory-maker/>

製品の脆弱性アドバイザリを、Markdown 形式で作成するための小さなツールです。CVSS v3.1 基本値の計算、定型文、公開前チェックを備え、日本語・英語の表示に対応しています。ブラウザの中だけで動作し、入力内容を外部へ送信しません。実験・試行レベルのツールであり、不具合が含まれている可能性があります。

- リポジトリ: <https://github.com/Lex0xF0C/lite-advisory-maker>
- ライセンス: MIT

### secriptorium（CSAF作成試行ツール）

<https://lex0xf0c.github.io/secriptorium>

CSAFを最小限構成で試行的に作成するためのツールです。CSAFのフォーマットへの適合は別途公式ツールで確認する必要があります。
実験・試行レベルのツールであり、不具合が含まれている可能性があります。lite-advisory-maker を流用して作成しています。

- リポジトリ: <https://github.com/Lex0xF0C/secriptorium>
- ライセンス: MIT

### ツールについての注意

- 本ツールは文面づくりの補助です。公開の可否、内容の正確性、CVSS 評価の妥当性は、利用者が判断してください。
- 無保証で提供しています。詳細は、リポジトリの LICENSE をご覧ください。

作成・翻訳: [Lex0xF0C](https://github.com/Lex0xF0C)
