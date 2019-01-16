# The Software Package Data Exchange（ソフトウェア パッケージ データ交換） (SPDX®) Specification Version 2.1.1

Copyright c 2010-2018 Linux Foundation and its Contributors. This work is licensed under the Creative Commons Attribution License 3.0 Unported (CC-BY-3.0) reproduced in its entirety in [Appendix VII](appendix-VII-creative-commons-attribution-license-3.0-unported.md) herein. All other rights are expressly reserved.

次の方々の貢献と支援に謝辞を贈る: Adam Cohn, Andrew Back, Ann Thornton, Bill Schineller, Bruno Cornec, Ciaran Farrell, Daniel German, David Wheeler, Debra McGlade, Dennis Clark, Ed Warnicke, Eran Strod, Eric Thomas, Esteban Rockett, Gary O'Neall, Guillaume Rousseau, Hassib Khanafer, Jack Manbeck, Jaime Garcia, Jeff Luszcz, Jilayne Lovejoy, John Ellis, Karen Copenhaver, Kate Stewart, Kevin Mitchell, Kim Weins, Kirsten Newcomer, Kris Reeves, Liang Cao, Marc-Etienne Vargenau, Mark Gisi, Marshall Clow, Martin Michlmayr, Martin von Willebrand, Matt Germonprez, Michael J. Herzog, Michel Ruffin, Nuno Brito, Oliver Fendt, Paul Madick, Peter Williams, Phil Robb, Philip Odence, Philip Koltun, Phillippe Ombredanne, Pierre Lapointe, Rana Rahal, Robin Gandhi, Sam Ellis, Sameer Ahmed, Scott K Peterson, Scott Lamons, Scott Sterling, Shane Coughlan, Steve Cropper, Stuart Hughes, Tom Callaway, Tom Vidal, Thomas F. Incorvia, Thomas Steenbergen, Venkata Krishna, W. Trevor King, Yev Bronshteyn, and Zachary McFarland


# 目次

## 1 理論的根拠

### 1.1 趣意

### 1.2 定義

### 1.3 データ交換用の共通フォーマットはなぜ必要なのか？

### 1.4 この仕様はどの項目をカバーしているか？

### 1.5 この仕様はどの項目をカバーしないか？

### 1.6 フォーマットに対する要求

### 1.7 適合

### 1.8 SPDX仕様2.0からの差分

## 2 文書作成情報

### 2.1 SPDX Version（SPDXバージョン）

### 2.2 Data License（データ ライセンス）

### 2.3 SPDX Identifier（SPDX識別子）

### 2.4 Document Name（文書名）

### 2.5 SPDX Document Namespace（SPDX文書名前空間）

### 2.6 External Document References（外部文書参照）

### 2.7 License List Version（ライセンス リスト バージョン）

### 2.8 Creator（作成者）

### 2.9 Created（作成日時）

### 2.10 Creator Comment（作成者コメント）

### 2.11 Document Comment（文書コメント）

## 3 Package Information（パッケージ情報）

### 3.1 Package Name（パッケージ名）

### 3.2 Package SPDX Identifier（パッケージSPDX識別子）

### 3.3 Package Version（パッケージ バージョン）

### 3.4 Package File Name（パッケージ ファイル名）

### 3.5 Package Supplier（パッケージ提供者）

### 3.6 Package Originator（パッケージ原作者）

### 3.7 Package Download Location（パッケージ ダウンロード位置）

### 3.8 Files Analyzed（解析したファイル）

### 3.9 Package Verification Code（パッケージ検証コード）

### 3.10 Package Checksum（パッケージ チェックサム）

### 3.11 Package Home Page（パッケージ ホーム ページ）

### 3.12 Source Information（ソース情報）

### 3.13 Concluded License（結論されたライセンス）

### 3.14 All Licenses Information from Files（ファイルからの全ライセンス情報）

### 3.15 Declared License（宣言されたライセンス）

### 3.16 Comments on License（ライセンスへのコメント）

### 3.17 Copyright Text（著作権テキスト）

### 3.18 Package Summary Description（パッケージ要約記述）

### 3.19 Package Detailed Description（パッケージ詳細記述）

### 3.20 Package Comment（パッケージ コメント）

### 3.21 External Reference（外部参照）

### 3.22 External Reference Comment（外部参照コメント）

## 4 File Information（ファイル情報）

### 4.1 File Name（ファイル名）

### 4.2 File SPDX Identifier（ファイルSPDX識別子）

### 4.3 File Type（ファイル タイプ）

### 4.4 File Checksum（ファイル チェックサム）

### 4.5 Concluded License（結論されたライセンス）

### 4.6 License Information in File（ファイル中のライセンス情報）

### 4.7 Comments on License（ライセンスへのコメント）

### 4.8 Copyright Text（著作権テキスト）

### 4.9 Artifact of Project Name (deprecated)（派生元プロジェクト名）（廃止予定）

### 4.10 Artifact of Project Homepage (deprecated)（派生元プロジェクト ホームページ）（廃止予定）

### 4.11 Artifact of Project Uniform Resource Identifier (deprecated)（派生元プロジェクト統一資源識別子）（廃止予定）

### 4.12 File Comment（ファイルコメント）

### 4.13 File Notice（ファイル表記）

### 4.14 File Contributor（ファイル貢献者）

### 4.15 File Dependencies (deprecated)（ファイル依存関係）（廃止予定）

## 5 Snippet Information（コード断片情報）

### 5.1 Snippet SPDX Identifier（コード断片SPDX識別子）

### 5.2 Snippet from File SPDX Identifier（ファイル由来コード断片SPDX識別子）

### 5.3 Snippet Byte Range（コード断片バイト範囲）

### 5.4 Snippet Line Range（コード断片ライン範囲）

### 5.5 Snippet Concluded License（コード断片結論されたライセンス）

### 5.6 License Information in Snippet（コード断片ライセンス情報）

### 5.7 Snippet Comments on License（コード断片ライセンスへのコメント）

### 5.8 Snippet Copyright Text（コード断片著作権テキスト）

### 5.9 Snippet Comment（コード断片コメント）

### 5.10 Snippet Name（コード断片名）

## 6 Other Licensing Information Detected（検出された他ライセンス情報）

### 6.1 License Identifier（ライセンス識別子）

### 6.2 Extracted Text（抽出されたテキスト）

### 6.3 License Name（ライセンス名）

### 6.4 License Cross Reference（ライセンス相互参照）

### 6.5 License Comment（ライセンス コメント）

## 7 Relationships between SPDX Elements（SPDX要素間の関係）

### 7.1 Relationship（関係）

### 7.2 Relationship Comment（関係コメント）

## 8 Annotations（注釈）

### 8.1 Annotator（注釈者）

### 8.2 Annotation Date（注釈日時）

### 8.3 Annotation Type（注釈タイプ）

### 8.4 SPDX Identifier Reference（SPDX識別子参照）

### 8.5 Annotation Comment（注釈コメント）

## 9 Review Information （レビュー情報）(deprecated)（廃止予定）

### 9.1 Reviewer（レビュアー） (deprecated)（廃止予定）

### 9.2 Review Date（レビュー 日時） (deprecated)（廃止予定）

### 9.3 Review Comment （レビュー コメント）(deprecated)（廃止予定）

## Appendix I: SPDX License List（SPDXライセンス リスト）
###　I.1 Licenses with Short Identifiers（ライセンスと簡易識別子）
###　I.2 Exceptions List（例外リスト）
###　I.3 Deprecated Licenses（廃止予定ライセンス）

## Appendix II: License Matching Guidelines and Templates（ライセンス整合ガイドラインとテンプレート）

## Appendix III: RDFデータ モデル実装と識別子構文

## Appendix IV: SPDX License Expressions（SPDXライセンス表現）

## Appendix V: ソース ファイルへのSPDX簡易識別子の適用

## Appendix VI: External Repository Identifiers（外部リポジトリ識別子）

## Appendix VII: Creative Commons Attribution License 3.0 Unported

