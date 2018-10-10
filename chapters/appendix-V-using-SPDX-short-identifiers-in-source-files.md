# Appendix V: Using SPDX short identifiers in Source Files（ソース ファイルへのSPDX簡易識別子の適用）

オープン ソース ソフトウェアに対するライセンスを特定することは、報告とライセンスコンプライアンスの両方の点で重要である。しかしながら、情報の欠落と不明瞭な情報のために、時としてライセンスの決定は困難になる。ライセンス情報が提供されているときでさえ、一貫した表記が無いために、ライセンス検出作業の自動化が難しく、人手による膨大な作業を必要となる。

SPDXライセンス リストに掲載された[簡易識別子](https://spdx.org/licenses/) は、ファイル レベルでライセンス情報を示すのに使用できる。この利点は多数あるが、特に以下が言える：

* 正確である
* 簡潔である
* 言語的に中立である
* 自動化プロセスが容易で信頼性が高い。
* コードを読みやすくする
* ライセンス情報がファイルと共に伝わる。（というのも、時としてプロジェクト全体が使われるわけでなく、ライセンス ファイルが削除されるためである）
* 標準であり、国際化できる亜種を準備する必要がない
* SPDX簡易識別子は不変である
* SPDXライセンス リスト ウェブサイトで検索や参照がしやすい

既存の著作権やライセンス情報を含むソース ファイルに関していえば、SPDX簡易識別子は補強として使い、既存の情報は置き換えないことがSPDXプロジェクトの推奨である。ライセンスの著作者から標準ヘッダーが提供されている場合には、標準ヘッダーを使用する（単独、またはSPDX簡易識別子と共用）ことを推奨する。個別のファイルにSPDX簡易識別子を使用する場合には、プロジェクトのLICENSEファイル中にある全ライセンスを提示し、SPDX簡易識別子がそれを参照していることを示すことが推奨される。これらのシナリオを図示するプロジェクトへのリンクは、[SPDX WIK 事例 ページの Meta_Tags](https://wiki.spdx.org/view/Technical_Team/SPDX_Meta_Tags#Examples).を参照。

## Format for SPDX-License-Identifier（SPDX-License-Identifierフォーマット）

SPDX-License-Identifierタグは、ファイルに適用されるライセンスを宣言する。ファイル先頭やその近辺のコメントに記載すべきである。既存のライセンス情報を含むファイルに関していえば、タグは補強として使い、情報を置き換えないことが推奨される。勿論、この点はファイルの著作権所有者が絶対的に決定権を持つ事項である。

SPDXライセンス識別子構文は単独ライセンス（ [SPDXライセンス リスト](https://spdx.org/licenses/)掲載の簡易識別子で表現されたもの）か、ライセンスの結合（ライセンス表現構文によって複数のライセンスの結合が表現されたもの）で構成される。

タグは、ソース ファイル中にタグの行として、一般にはコメント中に、表示すべきである。

    SPDX-License-Identifier: <SPDX License Expression>

## Representing Single License（単独ライセンスの表現）

単独ライセンスは、 [SPDXライセンス リスト](https://spdx.org/licenses/)に掲載された簡易識別子を使って表現される。任意で単項"+" 演算子を使って後続バージョンが適用可能であることを示す。

例：

    SPDX-License-Identifier: GPL-2.0+
    SPDX-License-Identifier: MIT

## Representing Multiple Licenses（複合ライセンスの表現）

複合ライセンスは、Appendix IVで定義されたSPDXライセンスを使って表現される。ライセンスの組は括弧で包含されなければならない。（これはSPDX表現の慣例である）他の構文は以下に記述される：

1. ライセンスの選択がある（"disjunctive license" （離接的ライセンス））場合には、それらは"OR"で分離されるべきである。2つ以上のライセンスの選択が提示される場合には、新しいライセンス表現を構成するために離接二項演算子"OR"を使用する。
2. 同様に、複数のライセンスを同時に適用する必要がある（"conjunctive license"（接続的ライセンス））場合には、それらは"AND"で分離すべきである。2つ以上のライセンスに同時に従う必要がある場合には、新しいライセンス表現を構成するために接続二項演算子"AND"を使用する。
3. ある特別な状況に例外を加えて、いくつかのライセンス条件が適用されることもある。この場合には、[認識されている例外識別子](https://spdx.org/licenses/exceptions-index.html).が後続する"WITH"演算子を使用する。
4. ある特別な状況に例外を加えて、いくつかのライセンス条件が適用されることもある。この場合には、特別な例外の状況を表現する新しいライセンス表現を構成するために二項演算子"WITH" を使用する。

例：

    SPDX-License-Identifier: (GPL-2.0 OR MIT)
    SPDX-License-Identifier: (LGPL-2.1 AND BSD-2-CLAUSE)
    SPDX-License-Identifier: (GPL-2.0+ WITH Bison-exception-2.2)

ライセンス表現についてのさらに多くの例や詳細については、[SPDX 2.1仕様のAppendix IV](./appendix-IV-SPDX-license-expressions.md) を参照。

SPDXライセンス リストに掲載された識別子を使ってライセンスを表現できない場合には、ファイルにライセンスヘッダーのテキストを記載する（標準ヘッダーがあるとき）か、テキストが置かれている中立的なサイトのURLを参照するのが最も良い方法だろう。SPDXライセンス リストに新しいライセンスの追加を要求するには、ここで説明されるプロセスに従う：[http://spdx.org/spdx-license-list/request-new-license-or-exception](http://spdx.org/spdx-license-list/request-new-license-or-exception).