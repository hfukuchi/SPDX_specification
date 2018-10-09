# SPDX License Expressions（SPDXライセンス表現）

## Overview（概要）

ほとんどの場合に単独のライセンスがソースコードやバイナリー ファイルのライセンス条件を表現するのに使用されるが、単独のライセンス識別子では不十分な場合がある。共通的な例としては、2つ以上のライセンス（たとえばGPL-2.0とBSD-3-Clause）を選択できる場合である。他の例としては、異なるライセンス（たとえばLGPL-2.1とBSD-3-Clause）が適用された2つ以上のソースコードをコンパイルとリンクすることで作成されたバイナリー ファイルを表現するのにライセンスの組が必要な場合である。

SPDXライセンス表現は、オープン ソース ソフトウェアのソース コードで典型的に見られるライセンス条件をもっと正確に表現する方法を提供する。ライセンス表現は、SPDXライセンス リストに掲載された単独のライセンス識別子、LicenseRef-`[idString]`によって記述されるユーザー定義ライセンス参照、SPDX例外と組み合わせたライセンス識別子、演算子のセット（AND、OR、WITH、+）によって構成されたライセンス識別子とライセンス参照の組み合わせである。このセクションで有効なSPDXライセンス表現の定義を提示する。

エージェントとツールを識別する正確な構文は、以下のように[ABNF（オーグメンティッド バッカス ナウア記法 ）](http://tools.ietf.org/html/rfc5234)

idstring = 1*(ALPHA / DIGIT / "-" / "." )

license-id = \<short form license identifier in [Appendix I.1](./appendix-I-SPDX-license-list.md)>

license-exception-id = \<short form license exception identifier in [Appendix I.2](appendix-II-license-matching-guidelines-and-templates.md)>

license-ref = ["DocumentRef-"1\*(idstring)":"]"LicenseRef-"1*(idstring)

simple-expression = license-id / license-id"+" / license-ref

compound-expression = 1*1(simple-expression /


simple-expression "WITH" license-exception-id /

  compound-expression "AND" compound-expression /

  compound-expression "OR" compound-expression ) /

  "(" compound-expression ")" )

license-expression = 1*1(simple-expression / compound-expression)

以下のセクションで、現代のソフトウェアのライセンス条件をより正確に表現できるライセンス表現文字列`<license-expression>`の詳細を記述する。

有効な `<license-expression>` 文字列は、以下で構成される：

(i)単独のライセンス識別子のような単純なライセンス表現 ；または

(ii)より小さな表現をブール ライセンス演算子で組み合わせて構成する複雑な表現

license-idと後続の`+`の間にスペースを入れてはいけない。これによって、パースの容易さと後方互換性がサポートされる。演算子"WITH"の両サイドにはスペースを入れなくてはいけない。演算子`AND` と `OR`の両サイドにはスペースかつ／または括弧を入れなければならない。

## Simple License Expressions（単純ライセンス表現） <a name="simple-expr"></a>

単純な `<license-expression>` は以下のどれか一つで構成される：

*  SPDXライセンス リスト簡易形式識別子例：GPL-2.0
* ライセンスの当該バージョンとそれ以降のバージョンを表現する、SPDXライセンス リスト簡易形式識別子と単項"+"演算接尾子例：GPL-2.0+
* SPDXユーザー定義ライセンス参照：["DocumentRef-"1*(idstring)":"]"LicenseRef-"1*(idstring) 

いくつかの例：

    LicenseRef-23

    LicenseRef-MIT-Style-1

    DocumentRef-spdx-tool-1.2:LicenseRef-MIT-Style-2

## Composite License Expressions （複合ライセンス表現）<a name="composite-expr"></a>

より表現力のある複合ライセンス表現は、算術演算子を使った数学表現を構成するのと同様に、"OR"、"AND"、"WITH"演算子を使って構成できる。`tag:value` フォーマットでは、2つ以上のライセンス識別子かつ／またはLicenseRefで構成されるライセンス表現は、括弧で包含されるべきである。："( )"これは、表現のパースが容易になるように仕様化されている。入れ子の括弧は、サブセクション（4）で議論される優先順位を特定できる。

### 1) Disjunctive "OR" Operator（離接"OR"演算子）

2つ以上のライセンスの選択が提示される場合、左右の演算対象は有効なライセンス表現値であるような新しいライセンス表現を構成するために、離接二項演算子"OR"を使用する。

たとえば、LGPL-2.1とMITライセンスから選択が可能な場合には、有効な表現は以下となる：

    (LGPL-2.1 OR MIT)

3つの異なるライセンスから選択するライセンスの例としては以下がある：

(LGPL-2.1 OR MIT OR BSD-3-Clause)

### 2) Conjunctive "AND" Operator（接続"AND"演算子）

同時に2つ以上のライセンスに従うことを要求される場合、左右両方の演算対象が有効なライセンス表現値であるような新しいライセンス表現を構成するために、接続二項演算子"AND"を使用する。

たとえば、LGPL-2.1とMITライセンスの両方に従う必要がある場合には、有効な表現は以下となる：

    (LGPL-2.1 AND MIT)

3つの異なるライセンスが適用される例は以下となる：

    (LGPL-2.1 AND MIT AND BSD-2-Clause)

### 3) Exception "WITH" Operator（例外"WITH"演算子）

ある特別な状況に例外を加えて、いくつかのライセンス条件が適用されることもある。この場合には、特別な例外の状況を表現する新しいライセンス表現を構成するために二項演算子"WITH" を使用する。有効な `<license-expression>` は、左オペランドが`<simple-expression>`で右オペランドが特別な例外条件を表す`<license-exception-id>`である。

たとえば、Bison例外がGPL-2.0+に適用される場合、表現は以下になる：

    (GPL-2.0+ WITH Bison-exception-2.2)

現行の有効な例外は[Appendix I セクション2](appendix-I-SPDX-license-list.md#I.2)に掲載されている。最新の例外は、以下を参照： [spdx.org/licenses](https://spdx.org/licenses). SPDX例外リストに適用可能な例外が掲載されていない場合には、ライセンス条件全体（例外を含む）を表現するために、単独の`<license-ref>`を使用する。

### 4) Order of Precedence and Parentheses（優先順位と括弧）

表現中の演算子の適用順序は重要である。（算術演算子と似ている） `<license-expression>` の演算子のデフォルトの優先順位は以下となる：

    +
 WITH
 AND
 OR

ここで、小さい順位の演算子は大きい順位の演算子より前に適用される。

例、以下の表現：

    LGPL-2.1 OR BSD-3-Clause AND MIT

は、LGPL-2.1と表現BSD-3-Clause AND MITの選択を表現する。というのもAND演算子はOR演算子よりも優先順位が高い（先に適用される）からである。

デフォルトの優先順位とは異なる優先度を表現する必要がある場合には、括弧の中の演算子は括弧の外の演算子よりも大きい優先順位を持つことを示すために、`<license-expression>`を括弧：()で包含することができる。これは(5+7)/2のような代数表現における括弧の使用方法と同じである。

例、以下の表現：

    (MIT AND (LGPL-2.1+ OR BSD-3-Clause))

は、OR演算子がAND演算子よりも先に適用されることを明示している。つまり、MITライセンスを適用する前に、最初にLGPL-2.1+かBSD-3-Clauseライセンスのどちらかを選択する必要がある。

### 5) License Expressions in RDF（RDFでのライセンス表現） <a name="rdf-expr"></a>

接続的なライセンスは、接続的なライセンスに含まれる各要素に対するspdx:member属性を伴う`<spdx:ConjunctiveLicenseSet>` 要素を使ってRDFで表現可能である。2つ以上のメンバーが必要である。

    <spdx:ConjunctiveLicenseSet>
 <spdx:member rdf:resource="http://spdx.org/licenses/GPL-2.0"/>
 <spdx:ExtractedLicensingInfo rdf:about="http://example.org#LicenseRef-EternalSurrender">
 <spdx:extractedText>
 In exchange for using this software, you agree to give its author all your worldly possessions.
 You will not hold the author liable for all the damage this software will inevitably cause not only
 to your person and property, but to the entire fabric of the cosmos.
 </spdx:extractedText>
 <spdx:licenseId>LicenseRef-EternalSurrender</spdx:licenseId>
 </spdx:ExtractedLicensingInfo>
 </spdx:ConjunctiveLicenseSet>

離接的なライセンスは、離接的なライセンスに含まれる各要素に対するspdx:member属性を伴う`<spdx:DisjunctiveLicenseSet>`要素を使ってRDFで表現可能である。2つ以上のメンバーが必要である。

    <spdx:DisjunctiveLicenseSet>
 <spdx:member rdf:resource="http://spdx.org/licenses/GPL-2.0"/>
 <spdx:member>
 <spdx:ExtractedLicensingInfo rdf:about="http://example.org#LicenseRef-EternalSurrender">
 <spdx:extractedText>
 In exchange for using this software, you agree to give its author all your worldly possessions.
 You will not hold the author liable for all the damage this software will inevitably cause
 not only to your person and property, but to the entire fabric of the cosmos.
 </spdx:extractedText>
 <spdx:licenseId>LicenseRef-EternalSurrender</spdx:licenseId>
 </spdx:ExtractedLicensingInfo>
 </spdx:member>
 </spdx:DisjunctiveLicenseSet>

ライセンス例外は、`<spdx:LicenseException>` 要素を使ってRDFで表現可能である。この要素は以下の属性を有する。

*  Comment - 例外の性質を記述するrdfs:comment要素
* See Also （任意）-  例外に関する情報の外部ソースを参照するrdfs:seeAlso要素
* Example - 例外の例を記述するテキスト
* Name - 項目の人間によって可読な名前
* License Exception ID: 該当するSPDXライセンス リスト中の例外を示す識別子
* License Exception Text: ライセンス例外の全文

        <rdf:Description rdf:about="http://example.org#SPDXRef-ButIdDontWantToException">
 <rdfs:comment>This exception may be invalid in some jurisdictions.</rdfs:comment>
 <rdfs:seeAlso>http://dilbert.com/strip/1997-01-15</rdfs:seeAlso>
 <spdx:example>So this one time, I had a license exception�c</spdx:example>
 <spdx:licenseExceptionText>
 A user of this software may decline to follow any subset of the terms of this license upon
 finding any or all such terms unfavorable.
 </spdx:licenseExceptionText>
 <spdx:name>&quot;But I Don&apos;t Want To&quot; Exception</spdx:name>
 <spdx:licenseExceptionId>SPDXRef-ButIdDontWantToException</spdx:licenseExceptionId>
 <rdf:type rdf:resource="http://spdx.org/rdf/terms#LicenseException"/>
 </rdf:Description>