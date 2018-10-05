# 8 Annotations（注釈）

## 8.1 Annotator（注釈者） <a name="8.1"></a>

**8.1.1** 目的：このフィールドは、ファイル、パッケージ、文書全体に対してコメントした個人、組織、ツールを特定する。

**8.1.2** 意図：ソフトウェア サプライチェーンの一員にとって、不明瞭なファイルやパッケージを検証して情報を追加することは重要である。

**8.1.3** 基数：条件付き（必須、1）、Annotation（注釈）がある場合.

**8.1.4** データ フォーマット：以下のキーワードを含む1行の文。

    "Person:" 人名および任意で "(email)"を付加
 "Organization:" 組織名および任意で"(email)"を付加
 "Tool: ツール識別子 - バージョン”

**8.1.5**  Tag: `Annotator:`

例：

    Annotator: Person: Jane Doe ()

**8.1.6** RDF: Property `spdx:annotator` in class `spdx:Annotation`

例：

    <Annotation>
 <annotator> Person: Jane Doe () </annotator>
 </Annotations>

## 8.2 Annotation Date（注釈日時） <a name="8.2"></a>

**8.2.1** 目的：いつコメントされたかを特定する。これは、ISO8601標準のUTCフォーマットで記述された結合日時に従って特定される。

**8.2.2** 意図：注釈日時は、実際のレビューがいつ行われたかの確認となる。

**8.2.3** 基数：条件付き（必須、1）、Annotation（注釈）がある場合

**8.2.4** データ フォーマット： `YYYY-MM-DDThh:mm:ssZ`

ここで

* `YYYY`は年
* `MM` は月（左0詰め）
* `DD` は日（左0詰め）
* `T` は時間の境界指示子
* `hh` は時間（左0詰め、24時間表記）
* `mm` は分（左0詰め）
* `ss`  は秒（左0詰め）
* `Z` は協定世界時指示子

**8.2.5** Tag: `AnnotationDate:`

例：

    AnnotationDate: 2010-01-29T18:30:22Z

**8.2.6** RDF: Property spdx:annotationDate in class spdx:Annotation

例：

    </Annotation>
 <annotationDate> 2010-01-29T18:30:22Z </annotation Date>
 </Annotation>

## 8.3 Annotation Type（注釈タイプ） <a name="8.3"></a>

**8.3.1** 目的：このフィールドは注釈タイプを記述する。注釈は通常誰かがファイルをレビューした際に作成される。このケースでは、注釈タイプは`REVIEW`（レビュー）とするべきである。作成者が、作成時にある要素に対する追加情報を保存したい場合には、注釈タイプは`OTHER`（その他）とすることが推奨される。

**8.3.2** 意図：注釈タイプの記録を可能にする。

**8.3.3** 基数：条件付き（必須、1）、Annotation（注釈）がある場合

**8.3.4** データ フォーマット： `REVIEW` | `OTHER`

**8.3.5** Tag: `AnnotationType:`

例：

    AnnotationType: REVIEW

**8.3.6** RDF: Property `rdfs:comment` in class `spdx:Annotation`

例：

    <Annotation>
 <spdx:annotationType rdf:resource="http://spdx.org/rdf/terms#annotationType_other"/>
 </Annotation>

## 8.4 SPDX Identifier Reference（SPDX識別子参照） <a name="8.4"></a>

**8.4.1** 目的：参照されているSPDX文書中の要素を一意に特定する。これらは、内部から参照され、SPDX文書識別子と組み合わせて外部からも参照される。

**8.4.2** 意図：SPDX文書内に、同一パッケージやファイルの複数バージョンがありうる。各要素は、一意に参照できる必要があるので、要素間の関係は明確に示すことができる。

**8.4.3** 基数：条件付き（必須、1）、Annotation（注釈）がある場合

**8.4.4** データ フォーマット： `[DocumentRef-[idstring]:]SPDXID`

ここで

["DocumentRef-"[idstring]":"] は、セクション2.6で記述される外部SPDX文書への任意の参照
`SPDXID` は、セクション2.3、3.2、4.2で記述された一意の文字、数字、`.` かつ／または `-`を含む文字列。

**8.4.5** Tag: `SPDXREF:`

例：

    SPDXREF: SPDXRef-45

例：

    SPDXREF: DocumentRef-spdx-tool-1.2:SPDXRef-5

**8.4.6** RDF:

RDFでは、注釈は対象のSPDX要素の属性である。

    <SpdxElement rdf:about=”#SPDXRef-45”>
 <annotation>
 <Annotation>
 ...
 </Annotation>
 </annotation>
 </SpdxElement rdf:about=”#SPDXRef-45”>

## 8.5 Annotation Comment（注釈コメント） <a name="8.5"></a>

**8.5.1** 目的：この任意の自由形式テキストフィールドによって、注釈者が解析についてコメントすることが可能になる。

**8.5.2** 意図：注釈者は、独立したアセスメントを提供し、解析に合意できない点を記述できる。

**8.5.3** 基数：条件付き（必須、1）、Annotation（注釈）がある場合

**8.5.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**8.5.5** Tag: `AnnotationComment:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例：

    AnnotationComment: <text>ファイルにあるすべてのライセンスは、人手の検査で見たものと整合している。
 ある条項は結論されたライセンスに影響を与える可能性がある。他の選択肢が可能である。しかし、結論されたライセンスは任意選択の一つである。</text>

**8.5.6** RDF: Property `rdfs:comment` in class `spdx:Annotation`

例：

    <Annotation>
 <rdfs:comment>ファイルにあるすべてのライセンスは、人手の検査で見たものと整合している。
 ある条項は結論されたライセンスに影響を与える可能性がある。他の選択肢が可能である。しかし、結論されたライセンスは任意選択の一つである。
 </rdfs:comment>
 </Annotation>