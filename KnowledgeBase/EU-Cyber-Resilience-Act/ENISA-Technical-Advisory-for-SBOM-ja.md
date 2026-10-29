> **【翻訳版に関するご案内】**
> 本書は、ENISA（欧州連合サイバーセキュリティ局）が2026年10月に公開した技術アドバイザリ『ENISA Technical Advisory for Software Bill of Materials』（原文: 英語）の日本語翻訳版です。
> - 原典: ENISA が公開した PDF（ファイル名: `ENISA_Technical_Advisory_-_Software_Bill_of_Materials_-_v1_10.pdf`）
> - 原文は © 欧州連合サイバーセキュリティ局 (ENISA), 2026 であり、CC BY 4.0（クリエイティブ・コモンズ 表示 4.0 国際）ライセンスで提供されています。本翻訳版も同ライセンスの下で提供します。原文からの変更点: 日本語への翻訳、PDF から Markdown への変換（ページヘッダー・ページ番号の除去、脚注の Markdown 化、表の再構成、目次のリンク化）、および本注記の追加。表紙画像（© Adobe Stock）は、CC BY の対象外のため含めていません。
> - 本翻訳版は ENISA が作成・承認・推奨したものではなく、**ENISA 非公認**の翻訳です。
> - 解釈に疑義がある場合は、必ず英語の原文を参照してください。

# ENISA ソフトウェア部品表 (SBOM) 技術アドバイザリ (ENISA Technical Advisory for Software Bill of Materials)

2026年10月 · TLP: CLEAR

## 欧州連合サイバーセキュリティ局 (ENISA) について (About ENISA)

欧州連合サイバーセキュリティ局 (ENISA) は、欧州全体で高い水準の共通のサイバーセキュリティを達成することに取り組む、EU の機関です。2004年に設立され、EU サイバーセキュリティ法によって強化された欧州連合サイバーセキュリティ局は、EU のサイバー政策に貢献し、サイバーセキュリティ認証スキームによって ICT 製品、サービス、プロセスの信頼性を高め、加盟国および EU の機関・組織と協力し、欧州が将来のサイバー上の課題に備えるのを支援しています。知識の共有、能力構築、意識向上を通じて、主要な関係者とともに、つながる経済への信頼を強化し、EU のインフラのレジリエンスを高め、最終的には、欧州の社会と市民をデジタル上で安全に保つことに取り組んでいます。ENISA とその活動に関する詳細は、www.enisa.europa.eu をご覧ください。

## 連絡先 (Contact)

著者に連絡する場合は、product_security@enisa.europa.eu をご利用ください。

本書に関する報道機関からの問い合わせは、press@enisa.europa.eu をご利用ください。

## 著者 (Author)

ENISA

## 法的通知 (Legal notice)

本刊行物は、特に断りのない限り、ENISA の見解と解釈を表すものです。規則 (EU) 2019/881 に基づく、ENISA または ENISA の組織の規制上の義務を支持するものではありません。

ENISA は、本刊行物またはその内容のいずれかを、変更、更新、または削除する権利を有します。本刊行物は情報提供のみを目的としており、無償でアクセス可能でなければなりません。本刊行物への言及、または全体もしくは一部の利用においては、すべて、ENISA を出典として明記しなければなりません。

第三者の情報源は、適宜引用されています。ENISA は、本刊行物で参照されている外部ウェブサイトを含む外部の情報源の内容について、責任または賠償責任を負いません。

ENISA も ENISA を代理して行動するいかなる者も、本刊行物に含まれる情報の利用によって生じうる結果について責任を負いません。

ENISA は、本刊行物に関する知的財産権を保持します。

## 著作権表示 (Copyright notice)

© 欧州連合サイバーセキュリティ局 (ENISA), 2026

特に断りのない限り、本文書の再利用は、クリエイティブ・コモンズ 表示 4.0 国際 (CC BY 4.0) ライセンス (https://creativecommons.org/licenses/by/4.0/) に基づいて許可されます。これは、適切なクレジットが表示され、変更点が示されていれば、再利用が許可されることを意味します。

（原文: “Unless otherwise noted, the reuse of this document is authorised under the Creative Commons Attribution 4.0 International (CC BY 4.0) licence (https://creativecommons.org/licenses/by/4.0/). This means that reuse is allowed, provided appropriate credit is given and any changes are indicated.”）

表紙画像の著作権: © Adobe Stock

ENISA が著作権を有しない写真その他の素材を使用または複製する場合は、著作権者から直接許諾を得なければなりません。

ISBN 978-92-9204-813-6, ISSN 3094-600X doi: 10.2824/2077129, カタログ番号 TP-01-26-022-EN-N

**免責事項:** 生成 AI は、言語の洗練と文書の予備的なスクリーニングを支援する目的で、限定的に使用されました。すべての出力は、分野の専門家によってレビューされ、検証されました。実質的な人間による監督なしに使用された AI 生成コンテンツはありません。

## 目次 (Table of contents)

- [1. はじめに (Introduction)](#1-はじめに-introduction)
  - [1.1 はじめに (Introduction)](#11-はじめに-introduction)
  - [1.2 範囲と文脈 (Scope and Context)](#12-範囲と文脈-scope-and-context)
  - [1.3 本書の現行版に関する注記 (Note on the current version of the document)](#13-本書の現行版に関する注記-note-on-the-current-version-of-the-document)
- [2. SBOM のアーキテクチャとデータフロー (SBOM Architecture and Data Flows)](#2-sbom-のアーキテクチャとデータフロー-sbom-architecture-and-data-flows)
  - [2.1 ソフトウェア部品表の仕組み (How Software Bill of Materials works)](#21-ソフトウェア部品表の仕組み-how-software-bill-of-materials-works)
    - [2.1.1 データモデル (Data Model)](#211-データモデル-data-model)
    - [2.1.2 SBOM の形式 (SBOM Formats)](#212-sbom-の形式-sbom-formats)
    - [2.1.3 SBOM の種類 (SBOM Types)](#213-sbom-の種類-sbom-types)
  - [2.2 SBOM のライフサイクル (SBOM Lifecycle)](#22-sbom-のライフサイクル-sbom-lifecycle)
    - [2.2.1 SBOM のライフサイクルのフェーズ (SBOM Lifecycle Phases)](#221-sbom-のライフサイクルのフェーズ-sbom-lifecycle-phases)
    - [2.2.2 CI/CD パイプラインの一部としての SBOM (SBOM as part of a CI/CD Pipeline)](#222-cicd-パイプラインの一部としての-sbom-sbom-as-part-of-a-cicd-pipeline)
    - [2.2.3 SBOM のオープンソースツールの全体像 (SBOM Open-source Tooling Landscape)](#223-sbom-のオープンソースツールの全体像-sbom-open-source-tooling-landscape)
- [3. SBOM の脅威とリスク (SBOM Threats and Risks)](#3-sbom-の脅威とリスク-sbom-threats-and-risks)
  - [3.1 SBOM の脅威 (SBOM Threats)](#31-sbom-の脅威-sbom-threats)
  - [3.2 SBOM に関する一般的なリスク (SBOM General Risks)](#32-sbom-に関する一般的なリスク-sbom-general-risks)
- [4. SBOM のベストプラクティス (SBOM Best Practices)](#4-sbom-のベストプラクティス-sbom-best-practices)
  - [4.1 SBOM の統合と自動化 (SBOM Integration and Automation)](#41-sbom-の統合と自動化-sbom-integration-and-automation)
    - [4.1.1 統合パターン (Integration Patterns)](#411-統合パターン-integration-patterns)
    - [4.1.2 共通の構成要件 (Common Configuration Requirements)](#412-共通の構成要件-common-configuration-requirements)
  - [4.2 一般的なセキュリティ推奨事項 (General Security Recommendations)](#42-一般的なセキュリティ推奨事項-general-security-recommendations)
- [5. 参考文献 (Bibliography)](#5-参考文献-bibliography)

# 1. はじめに (Introduction)

## 1.1 はじめに (Introduction)

現代のソフトウェア製品は、数百から数千のコンポーネントを含んでおり、それぞれが、アプリケーションやオペレーティングシステムのセキュリティを脅かす脆弱性を抱えている可能性があります。コンポーネントを可視化できなければ、組織は盲目的に運用することになり、悪用が起きて初めて露出に気づくことになります。

**ソフトウェア部品表 (Software Bill of Materials, SBOM)** は、潜在的な脆弱性を持つコンポーネントを特定することで、先手を打った脆弱性の追跡を支援します。これにより、セキュリティチームは、コンポーネントのインベントリを、公開されているセキュリティ脆弱性と突き合わせ、新たに生じるリスクに対応できます。当面の脆弱性にとどまらず、SBOM のデータは、コンポーネントの存続性やサプライチェーンの持続可能性に関するリスクの評価も支援します。

**SBOM** は、デジタル要素を含む製品のソフトウェア要素に含まれるコンポーネントの詳細とサプライチェーン上の関係を含む、正式な記録です。SBOM は、デジタル要素を含む製品に含まれるコンポーネントを識別し文書化する、一般に使用されている機械可読な形式で作成すべきです。SBOM は、ソフトウェアを製造し、購入し、運用する人々に、サプライチェーンへの理解を深める情報を提供できます。これには複数の利点があり、特に、新たに判明した既知の脆弱性やサイバーセキュリティリスクを、製造者とユーザーが追跡するのに役立ちます[^1]。

**中核となる能力 (Core Capabilities)**

- **透明性 (Transparency)**。現代のソフトウェアを構成するサードパーティおよびオープンソースのコンポーネントを明らかにする。
- **追跡可能性 (Traceability)**。デプロイされたソフトウェアを、上流のサプライヤーと下流の利用者に結び付ける。
- **コンプライアンス (Compliance)**。規制上および契約上の要件に対する、監査可能な記録を提供する。
- **セキュリティ (Security)**。脆弱性の検知と、ソフトウェアの来歴の検証を支援する。

SBOM は、基盤となるデータ層を形成するものであり、完全なセキュリティソリューションではありません。その価値は、適時のパッチ適用、緩和活動、文書化された脆弱性対応の判断といったセキュリティプロセスとの統合や、継続的な保守、ソフトウェア開発ライフサイクル (SDLC) 全体にわたる体系的なデプロイを通じて生まれます。

本書は、SBOM の導入に関する実践的なガイダンスを提供するものであり、ソフトウェアサプライチェーンの透明性を高めるための初期の能力を整えようとしている組織、特に零細企業を含む中小企業 (SME) およびスチュワードを対象としています。ENISA のセキュア・バイ・デザインおよびセキュア・バイ・デフォルトのプレイブック[^2]のセキュリティ原則、とりわけサプライチェーンの管理策、ライフサイクル管理、セキュアコーディングと検証の実践に沿っています。SBOM に取り組み始める組織を支援するため、主要な概念、業界標準、ユースケース、実装の実践を紹介します。具体的には、本書は次のことを行います。

- 定義されたライフサイクルに基づく、SBOM の実装アーキテクチャとデータフローの概要を示す;
- 対象とするリスクとともに、SBOM の脅威モデルの例を示す;
- SBOM エコシステム全体にわたるセキュリティ上の問題に対処するための対策を一覧にする。

本技術アドバイザリは、サイバーレジリエンス法 (CRA)[^3] に定められているものなどの規制要件、特に製造者の SBOM に関する義務に関連する必須要件を考慮しています。ただし、基本的には、それらの要件を超えうる、推奨されるベストプラクティスを説明するものです。

本書は、SBOM のライフサイクル全体にわたる一般的な脅威と、それらを緩和するための実践的な推奨事項を説明することで、こうした要件に技術的な文脈を提供することを目指しています。ただし、本書を CRA の法的解釈とみなしてはなりません。

## 1.2 範囲と文脈 (Scope and Context)

本技術アドバイザリは、ガイダンスの目的のみを意図しています。ここに記載された推奨事項とベストプラクティスは、強制ではなく、法的、規制上、またはコンプライアンス上の義務を新たに設けたり、変更したりするものでもありません。

本技術アドバイザリの範囲は、ソフトウェア部品表に限定されており、AI 向けのソフトウェア部品表、ハードウェア部品表 (HBOM)、暗号部品表 (CBOM) などの、新たに登場しつつあるその他の部品表 (BOM) やその派生形は対象外です。すべての成果物がいくつかの共通原則を共有しうる一方で、それぞれに異なる特徴もあるため、本アドバイザリの範囲外としています。

本技術アドバイザリは、業種を問わず、運用環境や産業にかかわらず、あらゆる種類の組織に適用できます。主として、SBOM の導入の初期段階にある組織を対象としており、組織の成熟度を評価し改善するためのフレームワークは提供しません。今後の版では、このテーマをより広範に扱う可能性があります。

## 1.3 本書の現行版に関する注記 (Note on the current version of the document)

本書の現行版は、2025年12月17日から2026年1月23日にかけて行われた ENISA の意見募集[^4]の結果として公開されるものであり、2026年6月9日に公表された ENISA の「SBOM Adoption State of Play 2026」[^5]で示された調査結果に大きく影響を受けています。意見募集を通じて、ENISA は、官民の関係者、サイバーセキュリティの専門家、オープンソースコミュニティから、67件の意見を受け取りました。

こうした意見と調査結果に基づき、ENISA は、「**SBOM Landscape Analysis: Towards an implementation guide**」を「**Technical Advisory for Software Bills of Materials**」へと転換し、エコシステムのニーズと意見により適切に応える必要があると認識しました。

最後に、本版は、2026年7月31日から9月11日にかけて実施されたレビューサイクルの一環として、**CRA 専門家グループの SBOM ワークストランドに参加する専門家**から提供された意見も反映しています。

謝辞 (Acknowledgements)

**意見やフィードバックを寄せてくださったすべての関係者に、公に感謝申し上げます。** すべての寄稿はレビューされ、可能な限り、推奨事項と所見は、この最終版で対処されています。本書は、定期的に改訂される可能性があります。

# 2. SBOM のアーキテクチャとデータフロー (SBOM Architecture and Data Flows)

## 2.1 ソフトウェア部品表の仕組み (How Software Bill of Materials works)

SBOM は、特定のソフトウェア製品について、ソフトウェアコンポーネントとその依存関係を把握する、構造化されたインベントリです。この「材料のリスト」を作成することで、製造者とユーザーは、自社のソフトウェア製品の「材料」を、誰が作ったのか、どこから来たのか、そしてそれらの「材料」がリスクをもたらしうるのかについて、よりよく理解し、より高い可視性を得られます。

**SBOM ジェネレーターは、さまざまな情報源から情報を収集**し、自社開発のコンポーネント、オープンソースライブラリ、サードパーティの商用ライブラリ、オペレーティングシステムのパッケージ、コンテナイメージなどを効果的に特定します。**情報源**の例は、次のとおりです。

- ソースコードリポジトリ、
- ビルド成果物、
- パッケージマネージャーのマニフェスト、
- ロックファイル、
- コンテナイメージ、
- バイナリ分析。

SBOM ジェネレーターは、特定されたソフトウェアコンポーネントのそれぞれについて、コンポーネント名、コンポーネントのバージョン、コンポーネントの作成者、一意の識別子、ライセンス情報、外部参照、依存関係などの**メタデータ**を収集し、相互に関連付けます。収集されるメタデータの範囲と網羅性は、その入手可能性、SBOM ジェネレーターの分析手法、選択された SBOM のデータモデル（例: CycloneDX や Software Package Data Exchange (SPDX)）によって決まります。その結果は、単なるコンポーネントの一覧ではなく、それらの依存関係の表現でもあります。

ソフトウェア構成分析、メタデータの収集、関係の発見が完了すると、SBOM は**標準的な機械可読な形式**（最も一般的には CycloneDX または SPDX）で生成されます。SBOM は、JSON、XML、YAML、Tag-Value として生成・保存できます。SBOM は、ソフトウェア開発ライフサイクル (SDLC) のさまざまなフェーズで生成できることを強調しておくことが重要です。異なる SDLC のフェーズで生成された SBOM は、異なるニーズに応え、異なる情報を含みます。

SBOM の生成は、運用およびセキュリティのプロセスを支援するために**能動的に利用**されない限り、限られた価値しかもたらしません。SBOM の利点は、脆弱性管理、ソフトウェア資産のインベントリ、ライセンスコンプライアンス、調達、規制対応などのユースケースへの**統合**にあります。

SBOM をコンプライアンス上の成果物以上のものとして扱う必要性は、**ENISA SBOM Adoption State of Play 2026** の調査結果にも表れています。回答者は、SBOM の作成と利用をソフトウェア開発の実践に統合するための**ベストプラクティスに関する業界のコンセンサス**を最優先事項（23%）とし、次いで、SBOM をリスクとコンプライアンスのプロセスに統合するためのベストプラクティス (19%)、SBOM の作成と利用の方法が時間とともにどう進化すべきかについてのガイダンス (19%) を挙げました。これらの調査結果は、成熟した SBOM の導入に向けた重要な一歩として、組織が、既存の開発、セキュリティ、ガバナンスのワークフローへの **SBOM の運用上の統合**を考えていることを示しています。

### 2.1.1 データモデル (Data Model)

SBOM の生成と利用の全体にわたって、相互運用性と一貫性を実現することを目的として、権威ある機関が SBOM のデータフィールドに関するガイダンスを公表しています。**ドイツ連邦情報セキュリティ庁** (BSI) は、必須のデータフィールドを定義した技術ガイドラインを公表しています。一方、**米国サイバーセキュリティ・インフラストラクチャセキュリティ庁** (CISA) は、米国電気通信情報局 (NTIA) が以前に公表した既存の成果を踏まえて、「ソフトウェア部品表の最小要素 (Minimum Elements for a Software Bill of Materials)」を定義しています。どちらの文書も、SBOM を生成するためのベースラインを提供します。

次の表は、国際的な相互運用性と規制上の要件を満たす SBOM を組織が作成するのを支援するため、BSI が必須とするデータフィールドを、米国 CISA が定義する最小要素に対応付けようとするものです。

| **データフィールド (Data Fields)** | **技術ガイドライン BSI TR-03183: 第2部 ソフトウェア部品表**[^6] | **データフィールド (Data Fields)** | **米国 CISA「ソフトウェア部品表 (SBOM) の最小要素」**[^7] |
|---|---|---|---|
| **SBOM メタデータ (SBOM Metadata)** | | | |
| **SBOM の作成者 (Creator of the SBOM)** | SBOM を作成した主体の電子メールアドレス。電子メールアドレスが利用できない場合は、「Uniform Resource Locator (URL)」でなければならない (MUST)。例: 作成者のホームページやプロジェクトの Web ページ。 | **SBOM 作成者 (SBOM Author)** | 主要コンポーネントの SBOM データを作成する主体の名称。 |
| - | - | **SBOM バージョン (SBOM Version)** | 以前に特定されたバージョンからの SBOM 文書の変更を示す、または最初のバージョンであることを示すために、*SBOM 作成者*が指定する識別子。 |
| **SBOM-URI** | この SBOM の「Uniform Resource Identifier (URI)」。 | - | - |
| - | - | **SBOM データ形式名 (SBOM Data Format Name)** | SBOM データを表現するために使用するデータ形式の名称。 |
| - | - | **SBOM データ形式バージョン (SBOM Data Format Version)** | データ形式のバージョンを示すために、SBOM のデータ形式が指定する識別子。 |
| - | - | **SBOM 作成者の署名 (SBOM Author Signature)** | *SBOM 作成者*に帰属するデジタル署名。 |
| - | - | **SBOM ツール名 (SBOM Tool Name)** | *SBOM 作成者*が SBOM を生成または修正するために使用したツールの名称。 |
| - | - | **SBOM ツールバージョン (SBOM Tool Version)** | *SBOM ツール名*の要素で特定されたツールのバージョンの識別子。 |
| **タイムスタンプ (Timestamp)** | 各形式の仕様に従った、SBOM データの編集の日時。<br>注: タイムスタンプには UTC のみを使用することが推奨される。 | **SBOM タイムスタンプ (SBOM Timestamp)** | SBOM データの直近の更新の日時の記録。 |
| - | - | **SBOM 生成コンテキスト (SBOM Generation Context)** | *SBOM 作成者*が SBOM を生成した時点での、相対的なソフトウェアライフサイクルのフェーズと、利用可能だったデータ（ビルド前、ビルド中、ビルド後）。 |
| **コンポーネントデータ (Component Data)** | | | |
| **コンポーネントの作成者 (Component creator)** | 該当するコンポーネントを作成し、該当する場合は保守している主体の電子メールアドレス。電子メールアドレスが利用できない場合は、「Uniform Resource Locator (URL)」でなければならない (MUST)。 | **コンポーネント製作者 (Component Producer)** | コンポーネントを作成し、定義し、識別する主体の名称。 |
| **コンポーネント名 (Component name)** | コンポーネントの作成者がコンポーネントに割り当てた名称。名称が割り当てられていない場合は、実際のファイル名でなければならない (MUST)。 | **コンポーネント名 (Component Name)** | *コンポーネント製作者*がソフトウェアコンポーネントに割り当てた名称。 |
| **コンポーネントのファイル名 (Filename of the component)** | コンポーネントの実際のファイル名。 | | |
| **コンポーネントのバージョン (Component version)** | 以前に作成されたバージョンからのコンポーネントの変更を示すために、作成者が使用する識別子。 | **コンポーネントバージョン (Component Version)** | 以前に特定されたバージョンからのソフトウェアコンポーネントの変更を示す、または最初のバージョンであることを示すために、*コンポーネントの作成者*が使用する識別子。 |
| **ソースコード URI (Source code URI)** | コンポーネントのソースコードの「Uniform Resource Identifier (URI)」。例: リポジトリ内で利用されたソースコードのバージョンの URL。バージョンを指定できない場合は、利用されたソースコードリポジトリそのもの。 | **コンポーネント識別子 (Component Identifiers)** | コンポーネントを識別するために、または関連するデータベースの検索キーとして使用される識別子。 |
| **コンポーネントのデプロイ可能な形式の URI (URI of the deployable form of the component)** | コンポーネントのデプロイ可能な形式を直接指し示す「Uniform Resource Identifier (URI)」。 | | |
| **その他の一意な識別子 (Other unique identifiers)** | コンポーネントを識別したり、関連するデータベースで検索したりするために使用できるその他の識別子。例: Common Platform Enumeration (CPE) や Package URL (purl)。 | | |
| **security.txt の URL（任意） (URL of the security.txt (optional))** | コンポーネントの作成者の security.txt の「Uniform Resource Locator (URL)」を含む。 | | |
| **デプロイ可能なコンポーネントのハッシュ値 (Hash value of the deployable component)** | デプロイされた／デプロイ可能なコンポーネントの、暗号的に安全なチェックサム（ハッシュ値）。 | **コンポーネントのハッシュ値 (Component Hash Value)** | 実行可能なコンポーネントの成果物に暗号学的ハッシュアルゴリズムを適用して生成された出力。 |
| **コンポーネントのソースコードのハッシュ値（任意） (Hash value of the source code of the component (optional))** | コンポーネントのソースコードの、暗号的に安全なチェックサム（ハッシュ値）。複数のソースファイルやソースコードツリーのハッシュ値をどのように作成するか、およびそのためにどのハッシュアルゴリズムを使用するかについての特定のアルゴリズムは、まだ決まっていない。 | | |
| - | - | **コンポーネントのハッシュアルゴリズム (Component Hash Algorithm)** | ソフトウェアコンポーネントの*コンポーネントのハッシュ値*を計算するために使用する、暗号学的アルゴリズム。 |
| **配布ライセンス (Distribution licences)** | ライセンシーがコンポーネントを使用できる、コンポーネントの配布ライセンス。 | **コンポーネントのライセンス (Component License)** | ソフトウェアコンポーネントが利用可能となるライセンスの識別子。 |
| **元のライセンス (Original licences)** | コンポーネントの作成者が割り当てたライセンス。 | | |
| **有効なライセンス（任意） (Effective license (optional))** | 現在の SBOM の作成者であるライセンシーが、コンポーネントを使用する際のライセンス。 | | |
| **他のコンポーネントへの依存関係 (Dependencies on other components)** | このコンポーネントが直接依存している、またはこのコンポーネントが含んでいる、すべてのコンポーネントの列挙。 | **コンポーネントの依存関係 (Component Dependency Relationship)** | 一方のコンポーネントが他方の動作に必要である場合の、2つのコンポーネント間の関係。 |
| **実行可能プロパティ (Executable property)** | コンポーネントが実行可能かどうかを記述する。取りうる値は「executable」と「non-executable」。 | - | - |
| **アーカイブプロパティ (Archive property)** | コンポーネントがアーカイブかどうかを記述する。取りうる値は「archive」と「no archive」。 | - | - |
| **構造化プロパティ (Structured property)** | コンポーネントが構造化されたファイル、すなわち内容のメタデータが残っているファイルかどうかを記述する。取りうる値は「structured」と「unstructured」。 | - | - |

***表1 - データモデル (Table 1 - Data Models)***

### 2.1.2 SBOM の形式 (SBOM Formats)

SBOM の形式も、ソフトウェアサプライチェーン全体にわたる相互運用性の決定要因です。標準化された形式は、共通のデータモデルを提供し、ソフトウェアの製作者、利用者、セキュリティツール、脆弱性管理プラットフォーム、コンプライアンスソリューションが、ソフトウェア構成分析の情報を一貫した方法で処理し交換できるようにします。

ENISA の SBOM Adoption State of Play 2026 によれば、組織の**73%**近くが CycloneDX または SPDX を使用しています。表2は、現在のバージョンに基づく、この2つの主要な形式を示します。

| | **SPDX (System Package Data Exchange) V 3.0.1**[^8] | **CycloneDX V 1.7**[^9] |
|---|---|---|
| **説明 (Description)** | システムコンポーネントの情報を文書化するための包括的なフレームワーク。製品ラインにおける脆弱性、ライセンス、依存関係の追跡を可能にする、詳細なソフトウェアメタデータの支援に、歴史的に重点を置いている。 | ソフトウェア部品表に対する、セキュリティに重点を置いたアプローチ。脆弱性の追跡、暗号的な完全性、包括的な依存関係の分析を重視している。 |
| **標準／後ろ盾 (Standard/Backing)** | SPDX® 仕様 v2.2.1 は、ISO 標準化された形式 (ISO/IEC 5962:2021) である。<br>SPDX 3 は、ISO/IEC 5962:2021 の更新として掲載されるよう、ISO で手続き中である。<br>SPDX 3.0 は、OMG 標準として承認されている[^10]。 | ECMA International により ECMA-424 として承認されている[^11]。<br>ECMA 技術委員会 54 (TC54) を通じて、正式な標準化プロセスとガバナンスモデルを維持している。<br>現在、ISO JTC1 のファストトラックを進めている。 |
| **主な要件 (Key Requirement)** | リスク分析: 製品ラインのリスク分析を支援する、明確で機械可読なメタデータを提供する。これには、脆弱性管理（ネイティブの CVE と VEX のメタデータ、CSAF などの形式、精密なライセンスコンプライアンスのメタデータ、依存関係の追跡）、精密なライセンスコンプライアンスのメタデータ、依存関係の追跡が含まれる。 | 脆弱性管理: ネイティブの VEX (Vulnerability Exploitability eXchange) のサポートにより、コンポーネントとセキュリティ脆弱性の精密な関連付けを可能にする。 |
| | サプライチェーンの透明性: ナレッジグラフを作成するための豊富な関係の選択肢とともに、包括的なコンポーネントの来歴と暗号的な完全性を可能にする。 | セキュリティの自動化: 軽量で効率的な形式により、セキュリティツールや CI/CD パイプラインとのシームレスな統合を促進する。 |
| | 規制への整合: 規制対象の産業におけるソフトウェアの透明性への要求の高まりに応える。 | 運用上の可視性: 静的なコンポーネントだけでなく、実行時のサービス、API、運用上の依存関係も文書化する。 |
| | 相互運用性: 多様なツールチェーンとエコシステムにまたがる、ソフトウェア構成のための共通言語を確立する。 | 暗号的な完全性: サプライチェーンのアテステーションとコンポーネントの認証のための、堅牢な検証の仕組みを提供する。 |

***表2 - SBOM の形式 (Table 2 - SBOM Formats)***

### 2.1.3 SBOM の種類 (SBOM Types)

SBOM の形式の選択だけが、SBOM に含まれる情報を左右する決定要因ではないことを理解することが重要です。SBOM が「**いつ**」生成されるかによって、含まれる情報の形式や目的は異なりえます。SBOM を生成する「いつ」の選択は、組織の運用上のニーズに応えるものであると同時に、適用される規制要件にも沿うものであるべきです。

この場合、SBOM の分類は、それらが生成される **SDLC のフェーズ**に由来します。米国 CISA による SBOM の種類[^12]に基づく、最も広く認知されている SBOM の種類は、次のとおりです。

| **SBOM の種類 (SBOM Type)** | **定義 (Definition)** | **取得される可能性のある情報 (Information Potentially Captured)** | **使用の例 (Indicative Use)** |
|---|---|---|---|
| **設計 (Design)** | 新しいソフトウェア成果物に含まれるコンポーネント（一部は存在しない可能性がある）の、意図された設計に関する SBOM。 | • 計画されているサードパーティライブラリ<br>• オープンソースパッケージ<br>• 商用コンポーネント<br>• 外部サービスと API<br>• 想定されるバージョン<br>• 意図されたライセンスモデル | • アーキテクチャ上の判断<br>• ライセンスの購入<br>• 脅威モデリング<br>• 規制要件の管理 |
| **ソース (Source)** | 新しい製品の成果物のビルドに使われる、開発環境、ソースファイル、含まれる依存関係から、直接作成される SBOM。 | • ソースコードにある既存のコンポーネント<br>• サードパーティおよびオープンソースのコンポーネントからの直接の依存関係<br>• 正確なバージョン<br>• ライセンス | • 依存関係の可視性<br>• 脆弱性の早期検知 |
| **ビルド (Build)** | ソースファイル、依存関係、ビルドされたコンポーネント、ビルドプロセスの一時的なデータ、その他の SBOM などのデータから、リリース可能な成果物（例: 実行ファイルやパッケージ）を作成するために、ソフトウェアをビルドするプロセスの一環として生成される SBOM。 | • 直接の依存関係<br>• 推移的依存関係<br>• リンクされたライブラリ<br>• 生成された成果物<br>• ビルド時のパッケージ<br>• オペレーティングシステムのコンポーネント<br>• 正確なバージョン<br>• 暗号学的ハッシュ<br>• サプライヤー情報<br>• 依存関係グラフ<br>• パッケージ URL<br>• CPE 識別子<br>• ライセンス | • 規制への適合<br>• 脆弱性評価<br>• ソフトウェアの透明性 |
| **分析 (Analysed)** | ビルド後に、成果物（例: 実行ファイル、パッケージ、コンテナ、仮想マシンイメージ）の分析を通じて生成される SBOM。こうした分析には、一般に、さまざまなヒューリスティックが必要である。文脈によっては、「サードパーティ」SBOM と呼ばれることもある。 | • 直接の依存関係<br>• 推移的依存関係<br>• リンクされたライブラリ<br>• 生成された成果物<br>• バージョン管理<br>• 暗号に関する情報<br>• ライセンス<br>• 完全性の検証<br>• ソフトウェアの出所<br>• サプライヤーの信頼に関する情報 | • ライセンスコンプライアンス<br>• 来歴の検証<br>• サプライチェーンのリスク評価<br>• セキュリティ認証／検証 |
| **デプロイ済み (Deployed)** | システム上に存在するソフトウェアのインベントリを提供する SBOM。これは、構成オプションの分析と、（場合によっては模擬された）デプロイ環境での実行時の振る舞いの検証を組み合わせた、他の SBOM の集合体であることもある。 | • インストールされているパッケージ<br>• コンテナイメージ<br>• 環境固有の依存関係<br>• プラットフォーム固有のライブラリ | • 企業レベルの資産インベントリ<br>• パッチ管理<br>• 環境固有のリスク評価<br>• 構成管理 |
| **ランタイム (Runtime)** | ソフトウェアを実行しているシステムに計装を施して生成される SBOM。システム内に存在するコンポーネントと、外部への呼び出しや動的にロードされるコンポーネントのみを取得する。文脈によっては、「計装された (Instrumented)」または「動的な (Dynamic)」SBOM と呼ばれることもある。 | • 動的にロードされるライブラリ<br>• プラグイン<br>• ランタイムモジュール<br>• コンテナのサイドカー<br>• 注入されたエージェント<br>• 共有サービス | • 脅威の検知<br>• 攻撃対象領域のリスク評価<br>• ランタイムの監視 |

***表3 - SBOM の種類 (Table 3 - SBOM Types)***

## 2.2 SBOM のライフサイクル (SBOM Lifecycle)

SBOM のデータモデル、形式、種類の主要な概念を整理したうえで、本節では、**SBOM のライフサイクルとアーキテクチャ**を示します。SBOM は、SDLC 全体を通じて継続的に管理され、新しいソフトウェアリリースによってコンポーネントが追加、更新、変更、削除されるのに合わせて、ソフトウェアの進化に追従するときに、付加価値をもたらします。

構造化され自動化された SBOM のライフサイクルは、SBOM が、社内外で適切に作成され、利用されることを確保することを目的としています。この考え方の必要性を示すため、ENISA SBOM Adoption State of Play 2026 では、組織が **SBOM に求めるもの**と**実際に受け取るもの**との間に大きなギャップがあることが明らかになりました。回答者の36%は、宣言された既知の未知 (known unknowns) を含む、すべての主要コンポーネントと直接の依存関係を、自組織が必要としていると回答しましたが、実際に受け取っているのは29%にとどまります。さらに、24%は完全な深さの分析を伴う SBOM を必要としていますが、受け取っているのは14%だけです。最後に、27%は、宣言された既知の未知を含む深さの分析を伴う SBOM を求めていますが、受け取っているのは12%にすぎません。

本節では、**概念と技術の両面から見た SBOM のライフサイクル**を示します。まず、生成から利用、継続的な保守に至る、SBOM のライフサイクルのフェーズを説明し、次に、これらのフェーズを CI/CD パイプラインにどのように統合し自動化できるかを示し、最後に、定義されたすべてのフェーズを支援するために利用可能なオープンソースのツールスタックを一覧にします。

### 2.2.1 SBOM のライフサイクルのフェーズ (SBOM Lifecycle Phases)

図1は、SBOM の主要な原則に沿った、**SBOM のライフサイクルの概念的な見方**を示しています。ライフサイクルは、必要な情報源に基づくソフトウェアのビルドと SBOM の生成から始まり、生成された SBOM の品質を評価する SBOM の検証へと進み、その後、完全性と真正性を保護するための暗号署名、セキュアな保管、運用での利用、そして継続的な保守と更新が続きます。

![図1 - SBOM のライフサイクル](assets/images/fig1.png)

***図1 - SBOM のライフサイクル (Figure 1 - SBOM Lifecycle)***（図中の文言は原文のとおり英語です）

### 2.2.2 CI/CD パイプラインの一部としての SBOM (SBOM as part of a CI/CD Pipeline)

SBOM の生成と利用を CI/CD パイプラインに統合することは、網羅性、正確性、信頼性を達成するためのベストプラクティスの1つとして、ますます採用され、認識されています。自動化により、組織は、最新の SBOM を生成し、検証し、更新し、利用できるようになります。SBOM Adoption State of Play 2026 の調査結果もこれを反映しており、組織の41%が、**リリース／ビルドごとの SBOM 生成の完全な自動化**を目指していると報告しました。しかし、ビルド段階より後の自動化は、まだ発展途上です。製品のサポート期間を通じて SBOM の更新を完全に自動化すると考える回答者は26%にとどまり、部分的に自動化すると考えるのは23%近くです。

前節では、SBOM のライフサイクルの概念的な見方を示しましたが、本節では、**CI/CD パイプラインの一部としての SBOM の技術的な実装**を示します。図2のアーキテクチャ図は、定義された SBOM のライフサイクルのフェーズに沿って、SBOM の SDLC への統合と、各フェーズの自動化を示しています。

各フェーズには、成功とみなすために考慮すべき主要な要素とプロセスが、基本的な障害点とともに含まれています。これは、SBOM を生成し利用する際に考慮すべき手順や側面の網羅的な一覧と解釈すべきではなく、SBOM の統合と自動化をどのように実装できるかの例として捉えるべきです。

プロセスは、情報源を生み出すソースコードのビルドから始まり、それが SBOM の生成を引き起こします。SBOM ジェネレーターは、ソフトウェアコンポーネントの特定、関連するメタデータの抽出、依存関係の分析を試み、標準化された形式（例: SPDX や CycloneDX）の機械可読な SBOM を作成します。ジェネレーターは、ソフトウェアのビルドプロセスと関連するリポジトリから、メタデータを収集し、相互に関連付け、構造化します。

SBOM の生成が成功すると、次のプロセスを開始する前に、SBOM が構文的に正しいか、選択した SBOM の仕様に適合しているか、必要なメタデータを含んでいるかを評価するため、検証プロセスが開始されます。このプロセスでは、コンポーネント識別子の検証も行うことが不可欠です。

検証されると、SBOM は、リポジトリやレジストリに保管され、下流のセキュリティツールによって利用される前に、真正性と完全性を確保するために暗号署名されます。

SBOM の保守と更新のフェーズは、SBOM を最新の状態に保ち、ソフトウェアの現行バージョンと同期させ続ける、継続的なプロセスを示しています。SBOM を再生成し、ライフサイクルのフェーズに従う必要性を反映するため、自動のトリガーの例が含まれています。

最後に、パイプライン全体を通じて SBOM の完全性、真正性、可用性を保護するための、セキュリティ管理策と信頼の仕組みの例が示されています。これにより、組織は、開発、セキュリティ、運用、調達、コンプライアンスの各チームで利用できる、信頼できる SBOM を作成できます。

![図2 - SBOM のアーキテクチャ図](assets/images/fig2.png)

***図2 - SBOM のアーキテクチャ図 (Figure 2 - SBOM Architectural Diagram)***（図中の文言は原文のとおり英語です）

### 2.2.3 SBOM のオープンソースツールの全体像 (SBOM Open-source Tooling Landscape)

統合と自動化は、必要なツールスタックによって支えられて初めて可能になります。SBOM Adoption State of Play 2026 によれば、組織の33%がオープンソースのツールに依拠しているため、表4では、CycloneDX と SPDX の両方の形式について、エンドツーエンドの SBOM のライフサイクルを支援するために CI/CD パイプラインに統合できるオープンソースのツールを示します。ツールは、SBOM のライフサイクルのフェーズに基づいて分類されており、網羅的なものではなく、本書の目的を支える例示的な一覧として捉えるべきです。

次の表は、一部のツールは形式に依存せず両方の SBOM 形式を支援できる一方で、SBOM の生成、スキーマの検証、および／または利用といった特定の段階では、形式に固有のツールが必要となることを示しています。

| **SBOM のライフサイクルのフェーズ／形式** | **生成: 自動化 (Generation: Automation)** | **検証: スキーマ (Validation: Schema)** | **検証: 品質スコア (Validation: Quality Score)** | **暗号署名: アテステーション (Cryptographic Signing: Attestation)** | **暗号署名: キーレス (Cryptographic Signing: Keyless)** | **保管: ワークフロー成果物 (Store: Workflow artifact)** | **利用: 脆弱性管理 (Consumption: Vulnerability Management)** |
|---|---|---|---|---|---|---|---|
| **CycloneDX**[^13] | cyclonedx-maven-plugin (Java/Maven),<br>@cyclonedx/ cyclonedx-npm (npm),<br>Cyclonedx-gomod (Go),<br>Cyclonedx dotnet tool (.NET),<br>cdxgen,<br>Syft,<br>SBOMit | CycloneDX CLI | sbomqs,<br>sbom-scorecard (eBAY) | GitHub CLI (gh attestation generate) | Cosign,<br>Sigstore | actions/upload-artifact@v4 | Grype,<br>Trivy,<br>OWASP Dependency Check,<br>OWASP Dependency-Track,<br>GitHub Dependency Review,<br>OWASP dep-scan,<br>OSV-Scanner (Go),<br>CVE Binary Tool, |
| **SPDX**[^14] | spdx-gradle-plugin,<br>spdx-maven-plugin,<br>spdx/tools-python,<br>spdx/tools-java,<br>spdx/tools-golang,<br>yocto (enabled by default in poky),<br>linux (make spdx),<br>zephyr (west spdx),<br>kubernetes-sigs/bom,<br>GitHub SBOM,<br>Microsoft sbom-tool (.NET),<br>Syft,<br>Trivy,<br>ORT,<br>SBOMit | tools.spdx.org/app/validate/<br>https://tools.spdx.org/app/ntia_checker/ | sbomqs,<br>sbom-scorecard (eBAY) | GitHub CLI (gh attestation generate) | Cosign,<br>Sigstore | actions/upload-artifact@v4 | Fossology,<br>sbomify,<br>sbom-cve-check,<br>tools.spdx.org/app/spdx3_viz,<br>GitHub Dependency Review |

***表4 - オープンソースの SBOM ツールスタック (Table 4 - Open-source SBOM Tool Stack)***

SBOM の形式が乱立していることは、実装とツールの全体像にとって大きな課題です。OpenSSF の[^15] Protobom のように、形式間をシームレスに変換するツールも存在します。

# 3. SBOM の脅威とリスク (SBOM Threats and Risks)

## 3.1 SBOM の脅威 (SBOM Threats)

本節では、SBOM のライフサイクル全体にわたる脅威の特定と緩和を組織が行うのを支援するため、**SBOM に焦点を当てた STRIDE 脅威モデル**を示します。Microsoft が開発した STRIDE 脅威モデルは、脅威の継続的な評価のための構造化されたフレームワークを提供します。これは、6つのカテゴリー、すなわち、**S**poofing（なりすまし）、**T**ampering（改ざん）、**R**epudiation（否認）、**I**nformation disclosure（情報漏えい）、**D**enial of service（サービス拒否）、**E**levation of privilege（権限昇格）に分けられています。

特定された脅威は、SBOM という成果物だけでなく、SBOM のエコシステム全体（例: SBOM の生成ツール、検証・署名サービス、リポジトリ、利用のパイプライン）を対象としています（表5）。

| **STRIDE** | **脅威 (Threat)** | **脅威シナリオ (Threat Scenario)** | **想定される影響 (Potential Impact)** | **緩和活動の例 (Indicative Mitigation Activities)** |
|---|---|---|---|---|
| **なりすまし (Spoofing)** | SBOM 作成者またはソフトウェア製作者のアイデンティティのなりすまし | 侵害された SBOM を配布するために、正当な SBOM 作成者またはソフトウェア製作者になりすます。 | 悪意あるソフトウェアや侵害されたコンポーネントを信頼し、使用してしまう。 | - デジタル署名<br>- サプライヤーのアイデンティティの検証 |
| | 利用者のアイデンティティのなりすまし | 制限された SBOM への不正アクセスを得るために、正当な利用者になりすます。 | 攻撃者の偵察や標的型攻撃を助ける、制限された情報へのアクセスを得られてしまう。 | - 利用者のアイデンティティの検証<br>- 管理された SBOM の共有 |
| | CI/CD パイプラインのなりすまし | SBOM が、信頼できる CI/CD パイプラインから生成されたように見える。 | 悪意あるソフトウェアの来歴を信頼してしまう。 | - ビルドのアテステーション<br>- ビルドのアテステーション<br>- 認証された CI/CD パイプライン |
| | SBOM 生成ツールのなりすまし | 悪意あるツールが、有効に見える SBOM を生成する。 | 悪意のある、または侵害された SBOM を信頼し、使用してしまう。 | - 信頼できるツールの使用<br>- コード署名 |
| | 証明書のなりすまし | 盗まれた証明書が、悪意ある SBOM に署名するために使われる。 | 信頼できる情報源からの正当なものに見える、悪意ある SBOM を信頼し、使用してしまう。 | - セキュアな鍵管理<br>- 証明書の失効 |
| | SBOM リポジトリのミラーのなりすまし | 侵害されたリポジトリのミラーが、正当に見える悪意ある SBOM を配布する。 | 信頼できる情報源からの正当なものに見える、悪意ある SBOM を信頼し、使用してしまう。 | - SBOM の署名の検証<br>- 暗号学的ハッシュを、信頼できるメタデータと比較する<br>- リポジトリの証明書を監視する |
| **改ざん (Tampering)** | SBOM データの改ざん | コンポーネント、バージョン、または依存関係が、生成後に改ざん（追加、削除、または変更）される。 | 依存関係の分析と脆弱性の特定が不正確になる。 | - 完全性の検証<br>- 署名の検証 |
| | メタデータの改ざん | コンポーネントのバージョン、ハッシュ、ライセンス、またはサプライヤーが、SBOM の生成前に改ざんされる。 | ソフトウェアのインベントリが不正確になり、コンプライアンス違反が生じる。 | - 暗号学的な完全性のチェック |
| | ハッシュの改ざん | 暗号学的ハッシュが変更される。 | 成果物の適切な検証が行われない。 | - 文書の署名 |
| | 来歴の改ざん | ビルドの来歴が変更される。 | 信頼できる情報源からのものに見える、悪意ある SBOM を信頼し、使用してしまう。 | - 署名付きアテステーション |
| | 外部参照の改ざん | PURL や CPE が変更される。 | 脆弱性の突き合わせと評価を行うために、既知で信頼できるものに見える、侵害されたリソースを使用し、それに基づいて行動してしまう。 | - デジタル署名<br>- 外部参照の検証 |
| **否認 (Repudiation)** | ソフトウェア製作者または SBOM 作成者による否認 | ソフトウェア製作者または SBOM 作成者が、SBOM の生成または公開を否認する。 | 説明責任の欠如。 | - デジタル署名<br>- タイムスタンプ<br>- 監査ログ |
| | 配布の否認 | SBOM 作成者またはソフトウェア製作者が、SBOM の配布を否認する。 | サプライチェーンの透明性の低下。 | - リポジトリのログ記録<br>- 署名付きリリース |
| **情報漏えい (Information Disclosure)** | 技術スタックの漏えい | 管理された SBOM の共有がないために、ソフトウェアのフレームワークとバージョンが明らかになる。 | 攻撃者の偵察を助け、攻撃対象領域を広げる。 | - 管理された SBOM の共有<br>- アクセス制御 |
| | コンポーネントの漏えい | 独自のソフトウェアコンポーネントが見えるようになる。 | 知的財産権の侵害。 | - 管理された SBOM の共有<br>- アクセス制御 |
| | サプライヤー関係の漏えい | サプライヤーとの関係が、公に見えるようになる。 | 攻撃対象領域の拡大と、より標的を絞った攻撃。 | - 管理された SBOM の共有<br>- アクセス制御 |
| | 依存関係グラフの漏えい | ソフトウェアのアーキテクチャと依存関係が、公に見えるようになる。 | 攻撃対象領域の拡大と、より標的を絞った攻撃。 | - 管理された SBOM の共有<br>- アクセス制御 |
| | バージョンの漏えい | 正確なソフトウェアのバージョンから、脆弱性との対応付けが可能になる。 | 既知の CVE を利用した、より迅速な悪用。 | - 管理された SBOM の共有<br>- アクセス制御 |
| | 暗号素材／メタデータの漏えい | 埋め込まれた証明書や鍵の識別子が、信頼関係を漏らす。ハッシュや識別子が、内部のリリースプロセスを明らかにする。 | 攻撃者の偵察を助け、攻撃対象領域を広げる。 | - 鍵管理<br>- アクセス制御<br>- 監査ログ |
| **サービス拒否 (Denial of Service)** | SBOM リポジトリへの DoS | SBOM リポジトリが利用できなくなる。 | インシデント対応中や調達中に SBOM が利用できない。 | - 冗長なインフラ<br>- DDoS 対策 |
| | パーサーへの DoS | 極端に大きい、または深く入れ子になった SBOM が、過剰な計算を引き起こし、パーサーのリソースを枯渇させる。 | リソースの枯渇とパーサーの障害。 | - SBOM のサイズ制限<br>- パーサーのハードニング |
| | ストレージへの DoS | 大量の SBOM が、リポジトリの容量を使い果たす。 | リソースの枯渇と、SBOM が必須の手順である場合の CI/CD パイプラインの中断の可能性。 | - SBOM のサイズと数の制限。<br>- SBOM の保持ポリシー |
| **権限昇格 (Elevation of Privilege)** | CI/CD パイプラインでの権限昇格 | SBOM を生成するビルドパイプラインでの、権限の昇格。 | 正当に見える、破損した SBOM の生成。 | - アクセス制御<br>- CI/CD パイプラインのハードニング |
| | SBOM リポジトリでの権限昇格 | SBOM リポジトリへの不正アクセス。 | 侵害された SBOM の使用と配布。 | - アクセス制御 |
| | 署名基盤での権限昇格 | 侵害された基盤が、信頼される SBOM を作成する。 | 侵害された SBOM の使用と信頼。 | - 鍵管理<br>- アクセス制御 |

***表5 - SBOM の脅威モデル (Table 5 - SBOM Threat Model)***

## 3.2 SBOM に関する一般的なリスク (SBOM General Risks)

脅威の特定を補完するものとして、本節では、SBOM の正確性、完全性、運用化を損なう、いくつかの一般的なリスクを示します。表6は、リスクシナリオの例、その想定される影響、および推奨される緩和活動を一覧にしたものです。

| **リスク (Risk)** | **リスクシナリオ (Risk Scenario)** | **想定される影響 (Potential impact)** | **緩和活動の例 (Indicative Mitigation Activities)** |
|---|---|---|---|
| **非標準の SBOM 形式** | 独自の、カスタムの、構造化されていない、またはその他の相互運用できない形式で生成された SBOM。 | 製作者と利用者の間の相互運用性の低下。 | - SPDX や CycloneDX などの確立された標準を用いて SBOM を生成する |
| **機械可読でない形式の SBOM** | 主として人間が読むことを意図した形式でのみ提供される SBOM。 | SBOM の利用における自動化とスケーラビリティの低下、およびコンポーネントを脆弱性データベースと自動的に関連付けられないこと。 | - 自動処理に適した、機械可読な形式の SBOM |
| **不完全な SBOM** | コンポーネントや依存関係が、SBOM で十分にカバーされていない。 | 脆弱性が発見されないままとなり、ソフトウェアのインベントリが不完全になる。 | - リリース時の自動生成<br>- CI/CD への統合<br>- 既知の未知と欠落したメタデータの、文書化された取り扱い |
| **古い SBOM** | SBOM が、ソフトウェアの現行バージョンをもはや反映していない。 | 脆弱性管理が不十分になり、リスク評価が不正確になる。 | - 上記で特定したトリガーに基づいて、SBOM を再生成する |
| **コンポーネントの識別が不十分** | コンポーネントが、エコシステムをまたいで一意に識別されていない。 | 脆弱性の関連付けと突き合わせが不正確になる。 | 標準化された、エコシステムを考慮したコンポーネント識別子を使用する。<br>- 上流のソースリポジトリのリポジトリ URL を使用する、または<br>- 名前空間、正確なバージョン、および該当する場合は暗号学的ハッシュと組み合わせた Package URL を使用する、または<br>- 名前空間、正確なバージョン、および該当する場合は暗号学的ハッシュとともに、命名規則に一貫して従って CPE を使用する |
| **SBOM の正確性が不十分** | ヒューリスティックな分析に頼ってコンポーネントと依存関係を特定する SBOM 生成ツールが、実際には存在しない、または使われていないコンポーネント（偽陽性）を含み、存在するコンポーネント（偽陰性）を欠落させ、あるいはバージョン、依存関係、識別子を誤って報告する SBOM を生成することがある。 | 偽陽性のコンポーネントによる過剰な脆弱性アラートとアラート疲れ、省略された、または誤って識別されたコンポーネントによる脆弱性の見落とし、および／または誤った脆弱性の突き合わせ。 | - ソフトウェアエコシステム、ビルドプロセス、成果物の種類、意図される SBOM の用途に応じて、適切な SBOM の生成手法を選択する<br>- 生成された SBOM を、ソフトウェア成果物と照合して検証する<br>- 網羅性と正確性のチェックを行う<br>- コンポーネント識別子を検証する |
| **SBOM と成果物の結び付きが弱い** | SBOM が、それが記述する正確なソフトウェア成果物、ビルド、リリース、コンテナイメージ、パッケージに、強く、かつ曖昧さなく関連付けられていない。 | 誤った SBOM が脆弱性分析に使われ、脆弱性の突き合わせにおける偽陽性や偽陰性が増える可能性がある。 | - 暗号学的ハッシュや不変のダイジェストを用いて、SBOM を正確な成果物に暗号的に結び付ける<br>- SBOM と成果物の関連付けを検証する |
| **SBOM の運用化が限定的** | SBOM が生成されているが、SDLC に統合されていない。 | SBOM の導入による価値が低下し、脆弱性管理が効果的でなくなる。 | - 資産管理、脆弱性管理、ライセンスコンプライアンスなどのために、SBOM を利用する |
| **SBOM の保持とライフサイクルの証跡が不十分** | 過去の SBOM と、それに関連する証跡（例: 過去の SBOM のバージョン、ビルドの識別子、成果物のダイジェスト、署名、VEX 文書）を、適切な期間にわたって保持していない。 | 過去の、またはデプロイ済みのソフトウェアのバージョンが、新たに発見された脆弱なコンポーネントを含んでいるかどうかを判断できない。 | - SBOM の保持ポリシーを定める<br>- リリースごとに SBOM を保持する<br>- バージョン履歴を維持する<br>- SBOM と成果物の追跡可能性を維持する<br>- ライフサイクル上の廃棄手順を定める |
| **脆弱性の優先順位付けの欠如** | SBOM を通じて特定されたすべての脆弱性が、悪用可能性を考慮せずに、同等に扱われる。 | 脆弱性の氾濫と、標的にされやすい脆弱性の是正の遅れ。 | - SBOM のデータと VEX を組み合わせて、悪用可能性と到達可能性を評価する<br>- 資産の重要度と露出度を考慮に入れる<br>- リスクに基づく脆弱性の優先順位付けのプロセスを確立する |

***表6 - SBOM に関する一般的なリスク (Table 6 - SBOM General Risks)***

# 4. SBOM のベストプラクティス (SBOM Best Practices)

本節では、定義された SBOM のライフサイクルに基づく、安全な SBOM の統合と自動化のためのベストプラクティスの例を示します。あわせて、前節で示した、特定された脅威と一般的なリスクに対する、推奨される緩和活動を補完します。

## 4.1 SBOM の統合と自動化 (SBOM Integration and Automation)

実用最小限の実装としては、ビルド時の統合を基盤として始めてください。このアプローチは、依存関係が最も正確に把握されている時点で取得でき、必要なインフラの変更も最小限で済みます。

既存の継続的インテグレーションの基盤を活用し、パイプラインのステージとして SBOM の生成を追加してください。現在のビルド環境と互換性のあるコマンドラインインターフェースを使用し、生成された SBOM は、既存の成果物リポジトリを使って、ビルド成果物とともに保管してください。最後に、標準的なパイプラインのテストの仕組みを通じて、検証を実装してください。（図3）

![図3 - パイプラインへの統合](assets/images/fig3.png)

***図3 - パイプラインへの統合 (Figure 3 - Pipeline Integration)***（図中の文言は原文のとおり英語です）

### 4.1.1 統合パターン (Integration Patterns)

**ビルド時の統合パターン (Build-Time Integration Pattern)**

コンパイルの成功の直後に、生成を統合します。ビルドのコンテキストが利用可能なうちに、直接の依存関係と推移的依存関係の両方を取得します。ビルド環境の詳細やコンパイルパラメータを含む、補足的なメタデータを生成します。Yocto、Kubernetes、Linux、Zephyr などの多くのビルド環境には、すでに自動 SBOM 生成の機能が統合されており、ビルドでそれらを有効にするだけで済みます。

**イベント駆動の生成パターン (Event-Triggered Generation Pattern)**

特定のイベントを契機に生成を開始するよう、リポジトリの Webhook を構成します。コミットまたはプルリクエスト、リリースのイベントなど、複数のトリガーの種類をサポートします。同時に発生する生成リクエストを処理するため、キューイングの仕組みを実装します。監査とロールバックの機能のために、生成の履歴を維持します。

### 4.1.2 共通の構成要件 (Common Configuration Requirements)

**リポジトリ構造の整理 (Repository Structure Organisation)**

リポジトリ構造の中に、SBOM の保管専用のディレクトリを設けます。ソースの SBOM と、生成された出力との分離を維持します。SBOM を、関連するコンポーネントと対応付ける命名規則を実装し、SBOM がビルドに含まれるのを防ぐ ignore パターンを構成します。

**パイプラインのオーケストレーション用テンプレート (Pipeline Orchestration Templates)**

SBOM の操作のための、再利用可能なパイプラインのセグメントを定義します。複数のプロジェクトの種類を支援できるよう、テンプレートをパラメータ化します。標準的な検証を含め、一時的な障害に対処するためのエラー処理とリトライのロジックを実装します。

**検証のチェックポイント (Validation Checkpoints)**

成果物を公開する前に、形式の検証を強制します。組織のポリシーに照らして、ライセンスの互換性を確認します。アテステーションが必要な場合は、暗号署名を検証します。

**脆弱性管理 (Vulnerability Management)**

構成された脆弱性データベースを用いて、既知の脆弱性を確認します。SBOM の利用を通じて特定された脆弱性は、定義された是正の期限、深刻度のしきい値、エスカレーション経路に結び付けるべきです。是正の期限は、深刻度、悪用可能性、露出度、製品の重要度、パッチの入手可能性、補完的対策を考慮すべきです。

**自動化の利点 (Automation Benefits)**

自動化は、手作業での生成に伴う不整合をなくすとともに、すべてのビルドが、対応する SBOM の文書を確実に生成するようにします。この継続的な生成により、新たな脅威が現れたときに、即座に脆弱性を評価できます。また、過去の SBOM を保持しておくことで、フォレンジック分析とコンプライアンスの実証を支援できます。最後に、自動化された検証は、非準拠の SBOM が本番環境に入ることを防ぎます。

**成功のための前提条件 (Prerequisites for Success)**

統合を成功させるには、成熟した継続的インテグレーションの基盤と、標準化されたビルドプロセスが必要です。生成のトリガー、保管場所、保持期間に関する明確なポリシーを確立しなければならず、同時に、監視機能によって、生成の成功率を追跡し、体系的な失敗を特定すべきです。

SBOM のプロセスは、社内監査、適合性評価、インシデント対応、監督当局からの要請のための証跡を生成すべきです。この証跡には、生成ログ、検証結果、署名、タイムスタンプ、リリースへのリンク、保持の記録が含まれます。

最後に、組織は、SBOM のカバレッジにおける、既知のギャップ、例外、「既知の未知」を文書化すべきです。特に、一部の依存関係が特定できない場合、サプライヤー情報が利用できない場合、またはバイナリのみのコンポーネントを十分に分析できない場合にはそうです。

## 4.2 一般的なセキュリティ推奨事項 (General Security Recommendations)

機密性、完全性、可用性、真正性、否認防止という主要な原則を守るため、セキュリティ管理策は、SBOM の CI/CD パイプライン全体にわたって、エンドツーエンドで適用すべきです。表7は、CI/CD パイプラインを構築する際に考慮すべきセキュリティ管理策の例と、その目的を示しています。

| **ライフサイクルのフェーズ (Lifecycle Phase)** | **セキュリティ管理策 (Security control)** | **目的 (Purpose)** |
|---|---|---|
| **すべてのフェーズ (All Phases)** | ロールベースのアクセス制御 (RBAC) | 最小権限に基づいて、リポジトリ、CI/CD ワークフロー、署名サービス、SBOM リポジトリへのアクセスを制限する。 |
| | 多要素認証 (MFA) | 開発者、管理者、CI/CD プラットフォームのアカウントを、認証情報の侵害から保護する。 |
| | 最小権限 | ユーザー、サービスアカウント、自動化に付与する権限を最小限にする。 |
| | セキュアなトランスポート層 | 証明書の検証を伴う TLS 1.3 を用いて、パイプラインのコンポーネント間の通信を保護する。 |
| | 監査ログ | 生成、検証、署名のイベントなどを含む、すべてのパイプラインの活動を記録する。 |
| | セキュリティイベントのアラート | 検証の失敗、署名の失敗、不正アクセスについてアラートを生成する。 |
| | パイプラインの完全性の保護 | コードレビューとブランチ保護を通じて、CI/CD ワークフローを不正な変更から保護する。 |
| | 構成管理 | パイプラインのコンポーネントとセキュリティポリシーについて、バージョン管理され、承認された構成を維持する。 |
| | ツールスタックの検証 | 実行前に、SBOM ジェネレーター、バリデーター、支援ツールの完全性と来歴を検証する。 |
| **生成 (Generation)** | 信頼できるリポジトリ | 認証された信頼できるレジストリまたはミラーからのみ、依存関係を取得する。 |
| | 来歴の生成 | ソース、ビルドプロセス、SBOM、ソフトウェア成果物を結び付ける、検証可能なビルドの来歴を生成する。 |
| **検証・署名・保管 (Validation, Signing, Store)** | セキュアなシークレット管理 | 該当する場合、署名鍵、API トークン、リポジトリの認証情報を、セキュアなボールトに保存する。 |
| **署名・保管 (Signing, Store)** | 成果物との結び付け | SBOM を、それが記述するソフトウェア成果物に、暗号的に関連付ける。 |
| **保管 (Store)** | 改ざん検知可能な保管 | 完全性の保護を備えた、不変の、またはバージョン管理されたリポジトリに、SBOM と成果物を保管する。 |
| | リポジトリの完全性の監視 | ソースコード、成果物、SBOM リポジトリへの不正な変更を検知する。 |
| **保管・保守と更新 (Store, Maintenance & Update)** | バージョン管理 | ソフトウェア成果物と、関連する SBOM のバージョン履歴を維持する。 |
| | バックアップと復旧 | SBOM リポジトリ、署名素材、監査ログを復旧できるようにする。 |

***表7 - セキュリティ推奨事項 (Table 7 - Security Recommendations)***

# 5. 参考文献 (Bibliography)

（参考文献は、書誌情報として原文のとおり英語で表記しています。）

REGULATION (EU) 2024/2847 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL, 2024. Horizontal cybersecurity requirements for products with digital elements and amending Regulations (EU) No 168/2013 and (EU) No 2019/1020 and Directive (EU) 2020/1828 (Cyber Resilience Act).

European Union Agency for Cybersecurity (ENISA), 2026. *SBOM Adoption State of Play - 2026*.

European Union Agency for Cybersecurity (ENISA), 2026. *Secure by Design and Secure by Default playbook Version 1.1.*

European Union Agency for Cybersecurity (ENISA), 2026. *Technical Advisory for Secure Use of Package Managers Version 1.1.*

German Federal Office for Information Security (BSI), 2025. *BSI TR-03183-2: Cyber Resilience Requirements for Manufacturers and Products - Part2: Software Bill of Materials (SBOM) Version 2.1.0.*

U.S. Cybersecurity and Infrastructure Security Agency (CISA), 2026. *Minimum Elements for a Software Bill of Materials (SBOM).*

Open Worldwide Application Security Project (OWASP), 2025. *Authoritative Guide to SBOM - Implement and optimize use of Software Bill of Materials Third Edition.*

The Linux Foundation and its Contributors, 2024. *The System Package Data Exchange (SPDX©) Specification Version 3.0.1.*

U.S. Cybersecurity and Infrastructure Security Agency (CISA) and SBOM Tooling and Implementation WG Contributors, 2023. *Types of Software Bill of Materials*.

U.S. Cybersecurity and Infrastructure Security Agency (CISA) and SBOM Tooling and Implementation WG Contributors, 2024. *Framing Software Component Transparency: Establishing a Common Software Bill of Materials (SBOM) Third Edition.*

SBOM Sharing & Exchanging Working Group, 2024. *SBOM Sharing Roles and Considerations*

Open Source Security Foundation (OpenSSF) Best Practices Working Group, 2023. *Source Code Management Platform Configuration Best Practices*.

Open Source Security Foundation (OpenSSF) Best Practices Working Group, 2023. *Concise Guide for Developing More Secure Software*.

Open Source Security Foundation (OpenSSF) and its Contributors, 2025. *Supply-chain Levels for Software Artifacts Version 1.2.*

Open Source Security Foundation (OpenSSF), 2025. *Improving Risk Management Decisions with SBOM Data*.

Open Source Security Foundation (OpenSSF) and its Contributors, 2025. Supply-chain Levels for Software Artifacts (SLSA) Version 1.2.

Cloud Native Computing Foundation (CNCF), 2026. *in-toto Attestation Framework Spec Version 1.2*.

Open Worldwide Application Security Project (OWASP), 2020. *Software Component Verification Standard Version 1.0*.

Open Worldwide Application Security Project (OWASP),2025. Software Supply Chain Security Cheat Sheat.

Open Worldwide Application Security Project (OWASP),2025. Dependency Graph & SBOM Best Practices Cheat Sheat

National Telecommunications and Information Administration (NTIA), 2021. *How-To Guide for SBOM Generation*.

National Telecommunications and Information Administration (NTIA), 2021. *Software Suppliers Playbook: SBOM Production and Provision Version 1.0*.

Microsoft. *The STRIDE Threat Model*.

Open Source Security Foundation (OpenSSF) End Users Working Group, 2024. *Threat Model of Enterprise Open Source Supply Chains*.

U.S. National Institute of Standards and Technology (NIST), 2022. *NIST Special Publication 800-218 - Secure Software Development Framework (SSDF) Version 1.1*.

Open Worldwide Application Security Project (OWASP), 2026. *Dependency Track Documentation Version 4.14.*

Sigstore Project. *Cosign Documentation.*

Open Source Security Foundation (OpenSSF) SBOM Everywhere WG, 2025. *SBOM Landscape*.

---

[^1]: 欧州議会及び理事会の2024年10月23日付規則 (EU) 2024/2847（デジタル要素を含む製品に関する水平的なサイバーセキュリティ要件、並びに規則 (EU) No 168/2013 及び (EU) 2019/1020 並びに指令 (EU) 2020/1828 の改正に関するもの）（サイバーレジリエンス法）（OJ L, 2024/2847, 20.11.2024, ELI: http://data.europa.eu/eli/reg/2024/2847/oj）。

[^2]: ENISA, Secure by Design and Default Playbook, 入手先: https://www.enisa.europa.eu/publications/enisa-secure-by-design-and-default-playbook

[^3]: 欧州議会及び理事会の2024年10月23日付規則 (EU) 2024/2847（デジタル要素を含む製品に関する水平的なサイバーセキュリティ要件、並びに規則 (EU) No 168/2013 及び (EU) 2019/1020 並びに指令 (EU) 2020/1828 の改正に関するもの）（サイバーレジリエンス法）（OJ L, 2024/2847, 20.11.2024, ELI: http://data.europa.eu/eli/reg/2024/2847/oj）。

[^4]: ENISA, ‘Call for feedback: Advancing software supply chain security together!’, プレスリリース, 2025年12月17日。

[^5]: ENISA, SBOM Adoption State of Play – 2026, 入手先: https://www.enisa.europa.eu/publications/sbom-adoption-state-of-play-2026

[^6]: BSI, Technical Guideline BSI TR-03183: Cyber Resilience Requirements for Manufacturers and Products Part 2: Software Bill of Materials, 入手先: https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TR03183/BSI-TR-03183-2_v2_1_0.html

[^7]: CISA, 2026 Minimum Elements for a Software Bill of Materials (SBOM), 入手先: https://www.cisa.gov/resources-tools/resources/2026-minimum-elements-software-bill-materials-sbom

[^8]: The Linux Foundation, The System Package Data Exchange® (SPDX®) Specification Version 3.0.1, 入手先: https://spdx.github.io/spdx-spec/v3.0.1/

[^9]: OWASP, Authoritative Guide to SBOM – Implement and optimize use of Software Bill of Materials, 入手先: https://cyclonedx.org/guides/OWASP_CycloneDX-Authoritative-Guide-to-SBOM-en.pdf

[^10]: OMG Standard, 入手先: https://www.omg.org/spec/SPDX/3.0/About-SPDX

[^11]: EXCMA-424, 入手先: https://ecma-international.org/publications-and-standards/standards/ecma-424

[^12]: U.S. CISA, Types of Software Bill of Materials (SBOM), 入手先: https://www.cisa.gov/resources-tools/resources/types-software-bill-materials-sbom

[^13]: https://cyclonedx.org/tool-center/

[^14]: https://spdx.dev/use/spdx-tools/

[^15]: https://sbom-catalog.openssf.org/catalog/#/Circle/Normalize/HowTo
