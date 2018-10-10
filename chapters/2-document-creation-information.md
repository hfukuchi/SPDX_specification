# 2 Document Creation Information（文書作成情報）

SPDXファイルごとに一つのインスタンスが必要である。ツールの前方後方互換性のために必要な情報を提供する。

基数：必須、1

フィールド：

## 2.1 SPDX Version（SPDXバージョン）<a name="2.1"></a>

**2.1.1** 目的：ファイルをパースして解釈する方法を理解するのに役立つ参照番号を提供する。仕様の将来の変更と後方互換性を可能にする。バージョン番号は、メジャー、マイナー バージョン指示子で構成される。メジャー フィールドは、バージョン間で後方非互換の変更（一つ以上のセクションの追加、変更、削除）がされたときに更新される。マイナー フィールドは、後方互換の変更がされたときに更新される。

**2.1.2** 意図：SPDX仕様に従って情報交換する関係者は、情報がどのSPDX仕様に従っているかを100%透明にする必要がある。

**2.1.3** 基数：必須、1

**2.1.4** データ フォーマット：“SPDX?M.N”

`M`はメジャー バージョン番号

`N`はマイナー バージョン番号

**2.1.5** Tag: `SPDXVersion:`

    例：

      SPDXVersion: SPDX-2.1

**2.1.6** RDF: `spdx:specVersion`

    例：

      <SpdxDocument rdf:about="...">
          <specVersion>SPDX-2.1</specVersion>
      </SpdxDocument>

## 2.2 Data License（データ ライセンス<a name="2.2"></a>

**2.2.1** 目的：SPDX仕様に適合するには、SPDXフィールドに適当なデータ（"SPDX?Metadata"）の記入が必要である。SPDX仕様は、SPDX作成者がSPDXメタデータに関連する説明文を記入する多数のフィールドを含んでいる。
データベース権（適応可能な裁判権の中で）の適法性に言及しなくても、そのような説明文はほとんどのベルヌ条約国において著作権対象になる。
SPDX仕様あるいはその一部を利用することで、あなたは、説明文（これに限らない）を含むSPDXメタデータにおけるすべての著作権（あなたの裁判権で決められた）はクリエイティブ コモンズ CC0 1.0ユニバーサルライセンスの条項に従うべきであることを認めたことになる。For SPDX-Metadata not containing any copyright rights, you hereby agree and acknowledge that the SPDX-Metadata is provided to you "as-is" and without any representations or warranties of any kind concerning the SPDX-Metadata, express, implied, statutory or otherwise, including without limitation warranties of title, merchantability, fitness for a particular purpose, non-infringement, or the absence of latent or other defects, accuracy, or the presence or absence of errors, whether or not discoverable, all to the greatest extent permissible under applicable law.

**2.2.2** 意図：SPDXに含まれる内容物（データやデータベース）が情報の再利用や同じプロジェクトに対して別のSPDXファイルを作成することを制限しうる知的財産権の影響下にあるかもしれないという懸念を軽減する。このアプローチは、SPDXファイルに関する知的財産や関連する制限事項を避けている。しかしながら、それでも、個人は相互にSPDXファイルの特定集合（ソフトウェアBOMを構成）のリリースやSPDXファイルの提供者の特定を制限する約束をすることができる。

**2.2.3** 基数：必須、1

**2.2.4** データ フォーマット：“CC0?1.0”

**2.2.5** Tag: `DataLicense:`

    例：

    DataLicense: CC0-1.0

**2.2.6** RDF: `spdx:dataLicense`

    例：

    <SpdxDocument rdf:about="...">
        <dataLicense rdf:resource="http://spdx.org/licenses/CC0-1.0" />
    </SpdxDocument>

## 2.3 SPDX Identifier（SPDX識別子） <a name="2.3"></a>

**2.3.1** 目的：内部の他のファイルやパッケージや外部の文書との関係で参照される現行のSPDX文書を特定する。全体として他の文書を参照するため、この識別子は外部文書識別子といっしょに使われるべきである。“Relationships between SPDX Elements”（「SPDX要素間の関係」）を参照。

**2.3.2** 意図：他の要素との関係で、文書がそれ自体を参照する方法を提供する。

**2.3.3** 基数：必須、1

**2.3.4** データ フォーマット：`SPDXRef-DOCUMENT`

**2.3.5** Tag: `SPDXID:`

    例：

    SPDXID: SPDXRef-DOCUMENT

**2.3.6** RDF: 文書のURIは、以下が付けられた文書名前空間である。

`#SPDXRef-DOCUMENT`

    <spdx:SpdxDocument rdf:about="http://spdx.org/spdxdocs/spdx-example-444504E0-4F89-41D3-9A0C-0305E82C33...">
        ...
    </spdx:SpdxDocument>

## 2.4 Document Name（文書名）<a name="2.4"></a>

**2.4.1** 目的：作成者によって付けられた文書名を特定する

**2.4.2** 意図：文書名は重要な慣例であり、URIより簡単な参照方法である。

**2.4.3** 基数：必須、1

**2.4.4** データ フォーマット：1行の文。

**2.4.5** Tag: `DocumentName:`

    例：

    DocumentName: glibc-v2.3

    DocumentName: ubuntu-14.04

**2.4.6** RDF: Property `spdx:name` in class `Document`

    例：

    <SpdxDocument rdf:about="...">
        <name>glibc-v2.3</name>
    </SpdxDocument>

    <SpdxDocument rdf:about="...">
        <name>ubuntu-14.04</name>
    </SpdxDocument>

## 2.5 SPDX Document Namespace（SPDX文書名前空間） <a name="2.5"></a>

**2.5.1** 目的：‘#’ デリミタを除いて、[RFC-3986][rfc3986]に規定されている固有な絶対統一資源識別子[Uniform Resource Identifier][URI]（URI）としてSPDX文書特有の名前空間を提供する。SPDX文書URIはURI "part"（例えば ‘#’）を持てない。というのも‘#’は、SPDX要素URI（パッケージ、ファイル、コード断片等）の中で文書名前空間をSPDX識別子から分離するために使われるからである。さらに、スキーム（例えば“https:”）が必要である。

URIは、SPDX文書の特定バージョンを含むSPDX文書に一意の値でなければならない。SPDX文書が更新され、新しいバージョンが作成された場合には、更新された文書に新しいURIを使わなければならない。SPDX文書には1つのURIだけが対応し、与えられたURIには1つの文書だけが対応する。

**2.5.2** 意図：URIは、他のSPDX文書がこのSPDX文書内にあるSPDX要素を参照するための明確なメカニズムを提供する。外部文書の参照方法については[セクション 2.6](#2.6) を参照。要求されていないが、SPDX文書を見つけるための情報を提供するようにURIを構成できる。たとえば、インターネット上でアクセス可能であれば、URIは、SPDX文書自体を参照するURLとして作成できる。インターネットで公にアクセス可能なSPDX文書のURIを作成するベストプラクティスは以下である。http://[CreatorWebsite]/[pathToSpdx]/[DocumentName]?[UUID]　ここで：

* CreatorWebsiteは、文書作成者によってホストされているウェブサイトである。（例えば、SPDXによって提供されるSPDX文書であれば、spdx.orgである。）
* PathToSpdxは、ウェブサイト上でSDPX文書が置かれた場所へのパスである。（例  /spdx/spdxdocs）
* DocumentNameは、SPDX文書自体へ与えられた名前である。一般的には、パッケージ（パッケージ セット）名の後にバージョンが続く。[(セクション 2.4参照)](#2.4).
* UUID はuniversally unique identifierのことである。UUIDは、[オンラインUUID生成器][uuid-gen]で生成されるバージョン4 乱数UUIDか、この特定のSPDX文書バージョンには一意であると知られているSHA1チェックサムから生成されるバージョン5 UUIDが利用可能である。
* 作成者が自分のウェブサイトを保有していない場合には、CreatorWebsiteとPathToSpdxのデフォルト値（'spdx.org/spdxdocs'）が利用可能である。SPDX文書はこのウェブサイトに保管もアクセス可能でもないことに注意。URIは、上記の慣習に従うために、一意のIDを生成するために利用される。

URIは、アクセス可能である必要はないことに注意。一意のIDを与えるためだけに使われている。多くの場合、URIは文書を入手できるウェブサイトを示しているが、これがすべて該当するとは限らない。

[URI]: https://en.wikipedia.org/wiki/Uniform_Resource_Identifier
[rfc3986]: https://tools.ietf.org/html/rfc3986
[uuid-gen]: https://www.uuidgenerator.net/

**2.5.3** 基数：必須、1

**2.5.4** データ フォーマット：[RFC-3986](https://tools.ietf.org/html/rfc3986)で規定された一意の絶対統一資源識別子（URI）、ただし以下の例外を含む：

SPDX文書URIはURI "part"（例えば ‘#’）を持てない。というのも‘#’は、SPDX要素識別子を特定するために使われるからである。
URIは、スキーム（例えば“https:”）を含まなければならない。

URIは、SPDX文書の特定バージョンを含むSPDX文書に一意の値でなければならない。SPDX文書が更新され、新しいバージョンが作成された場合には、更新された文書に新しいURIを使わなければならない。SPDX文書には1つのURIだけが対応し、与えられたURIには1つの文書だけが対応する。

**2.5.5** Tag: `DocumentNamespace:`

    例：

    DocumentNamespace: http://spdx.org/spdxdocs/spdx-tools-v1.2-3F2504E0-4F89-41D3-9A0C-0305E82...

**2.5.6** RDF: The unique ID is the URI for the SPDX document

    例：

    <SpdxDocument rdf:about="http://spdx.org/spdxdocs/spdx-tools-v1.2-3F2504E0-4F89-41D3-9A0C-0305E82...">
        <rdfs:comment>This document was created using SPDX 2.0 using licenses from the web site.</rdfs:comment>
    </SpdxDocument>

## 2.6 External Document References（外部文書参照） <a name="2.6"></a>

**2.6.1** 目的：このSPDX文書内で参照されている外部SPDX文書を特定する。

**2.6.2** 意図：この文書内で参照されるSPDX要素は、外部SPDX文書から参照される他のSPDX要素に関連しているかもしれない。SPDX要素としては、コード断片、ファイル、パッケージ、ライセンス参照、SPDX文書がありうる。

**2.6.3** 基数：任意、1以上

**2.6.4** データ フォーマット：DocumentRef?`[idstring]` `[SPDX Document URI]` `[Checksum]`

ここで

`[idstring]`は、文字、数字、“.”、“?”または“+”を含む一意の文字列。
`[SPDX Document URI]` は、[セクション2.5](#2.5) で定義されているように、対象文書を参照している外部文書の一意のIDである。

`[Checksum]` は、[セクション3.9](3-package-information.md#3.9)で定義されているチェックサム フォーマットに従って記載される外部文書のチェックサムである。

**2.6.5** Tag: `ExternalDocumentRef:`

    例：

    ExternalDocumentRef:DocumentRef-spdx-tool-1.2 http://spdx.org/spdxdocs/spdx-tools- v1.2-3F2504E0-4F89-41D3-9A0C-0305E82C3301 SHA1: d6a770ba38583ed4bb4525bd96e50461655d2759

**2.6.6** RDF: Property `spdx:externalDocumentRef` in class `spdx:Document range ExternalDocumentRef`.

ExternalDocumentRefは2つの属性を持つ。

* spdxDocument - 参照されるSPDX文書
* checksum - 参照されるSPDX文書のチェックサム

    例：

    <externalDocumentRef>
        <ExternalDocumentRef>
            <spdx:externalDocumentId>DocumentRef-spdx-tool-1.2</spdx:externalDocumentId>
            <spdxDocument rdf:about=”http://spdx.org/spdxdocs/spdx-tools-v1.2-3F2504E0-4F89-41D3-9A0C-0305E82...” />
            <checksum>
                <Checksum>
                    <algorithm rdf:resource="checksumAlgorithm_sha1"/>
                    <checksumValue>d6a770ba38583ed4bb4525bd96e50461655d2758
                    </checksumValue>
                </Checksum>
            </checksum>
        </ExternalDocumentRef>
    </externalDocumentRef>

注：RDFでは、外部参照に簡易形式の名前が必要な場合は、外部文書参照のために名前空間を作成できる。

## 2.7 License List Version（ライセンス リスト バージョン） <a name="2.7"></a>

**2.7.1** 目的：SPDXファイルの作成者がSPDXファイルを作成する際に使用したSPDXライセンス リストのバージョンを任意で記載するフィールド。

**2.7.2** 意図：バージョン更新時にSPDXライセンス リストにライセンスが加えられることを認識した上で、SPDXファイルの受領者に使用されたSPDXライセンス ファイルのバージョンを提供することを意図している。このことは、将来、現行のものより古いバージョンのSPDXライセンス リストがSPDXで使用されることを見越している。

**2.7.3** 基数：任意、1

**2.7.4** データ フォーマット： `M.N`

ここで

`M`はメジャー バージョン番号
`N`はマイナー バージョン番号

**2.7.5** Tag: `LicenseListVersion:`

    例：

    LicenseListVersion: 2.0

**2.7.6** RDF: Property `licenseListVersion` in class `spdx:CreationInfo`

    例：

    <CreationInfo>
        <licenseListVersion>2.0</licenseListVersion>
    </CreationInfo>

## 2.8 Creator（作成者） <a name="2.8"></a>

**2.8.1** 目的：誰が（ツールの場合は、何が）SPDXファイルを作成したかを特定する。SPDXファイルが個人によって作成された場合には、個人の名前を表記する。SPDXファイルが企業もしくは組織を代表して作成された場合には、組織名を表記する。SPDXファイルがツールによって作成された場合には、ツールの名前とバージョンを表記する。複数の関係者やツールがある場合には、このフィールドを複数使用する。そうする方がふさわしい場合には、個人名や組織名を“anonymous”（匿名）にしてもよい。

**2.8.2** 意図：作成方法を知ることは、SPDXファイルの受領者が解析情報の全般的な信頼性・正確度を評価する助けとなる。rmation.

**2.8.3** 基数：任意、1以上

**2.8.4** データ フォーマット：以下のキーワードを含む1行の文。

    "Person:" 人名および任意で "(email)"を付加
    "Organization:" 組織名および任意で"(email)"を付加
    "Tool: toolidentifier-version”

**2.8.5** Tag: `Creator:`

    例：

    Creator: Person: Jane Doe ()
    Creator: Organization: ExampleCodeInspect ()
    Creator: Tool: LicenseFind-1.0

**2.8.6** RDF: Property `spdx:creator` in class `spdx:CreationInfo`

    例：

    <CreationInfo>
        <creator> Person: Jane Doe () </creator>
        <creator> Organization: ExampleCodeInspect () </creator>
        <creator> Tool: LicenseFind-1.0 </creator>
    </CreationInfo>

## 2.9 Created（作成日時） <a name="2.9"></a>

**2.9.1** 目的：SPDXファイルがいつ作成されたかを特定する。作成日は、ISO8601標準のUTCフォーマットで記述された結合日時に従って特定される。このフィールドは、後続のレビューにおいて情報を追加できる、[セクション 8](8-annotations.md)で定義するフィールドとは区別される。

**2.9.2** 意図：タイム スタンプは、解析の更新が必要かどうかの基準になりうる。

**2.9.3** 基数：必須、1

**2.9.4** データ フォーマット： `YYYY-MM-DDThh:mm:ssZ`

ここで

* `YYYY`は年
* `MM` は月（左0詰め）
* `DD` は日（左0詰め）
* `T` は時間の境界指示子
* `hh` は時間（左0詰め、24時間表記）
* `mm` は分（左0詰め）
* `ss`  は秒（左0詰め）
* `Z` は協定世界時指示子

**2.9.5** Tag: `Created:`

    例：

    Created: 2010-01-29T18:30:22Z

**2.9.6** RDF: Property `spdx:created` in class `spdx:CreationInfo`

    例：

    <CreationInfo>
        <created> 2010-01-29T18:30:22Z </created>
    </CreationInfo>

## 2.10 Creator Comment（作成者コメント）<a name="2.10"></a>

**2.10.1** 目的：SPDXファイル作成者が、SPDXファイル作成に関する全般的なコメントや、他のフィールドに含まれない関連コメントを提供するための任意フィールド。

**2.10.2** 意図：SPDXファイル受領者にSPDXファイル作成者のコメントを提供する。

**2.10.3** 基数：任意、1

**2.10.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

 `tag:value` フォーマットでは `<text>..</text>`で分離され、RDFでは`<rdfs:comment>`で分離される。

**2.10.5** Tag: `CreatorComment:`

    例：

    CreatorComment: <text>This SPDX file was created by a combination of using a free tool,
     as indicated above, and manual analysis by several authors of the code.</text>

**2.10.6** RDF: Property `rdfs:comment` in class `spdx:CreationInfo`

    例：

    <CreationInfo>
        <rdfs:comment>This SPDX file was created by a combination of using a free tool, as indicated above, and manual analysis by several authors of the code.</rdfs:comment>
    </CreationInfo>

## 2.11 Document Comment（文書コメント） <a name="2.11"></a>

**2.11.1** 目的：SPDXファイル作成者がSPDXファイル受領者にコメントを提供するための任意フィールド。

**2.11.2** 意図：読者やレビュアーにSPDXファイル作成者からのSPDXファイルについてのコメントを提供する。

**2.11.3** 基数：任意、1

**2.11.4** データ フォーマット：自由形式文（複数行に渡ってもよい） `tag:value` フォーマットでは `<text>..</text>`で分離され、RDFでは`<rdfs:comment>`で分離される。

**2.11.5** Tag: `DocumentComment:`

    例：

    DocumentComment: <text>This document was created using SPDX 2.0, version 2.3 of the SPDX License List and refering to licenses in file MyCompany.Approved.Licenses.spdx.</text>

**2.11.6**  RDF: Property `rdfs:comment` in class `SpdxDocument`

    例：

    <SpdxDocument rdf:about="...">
        <rdfs:comment>
            この文書は、ウェブサイトからのライセンスを使い、SPDX2.0に従って作成された。
        </rdfs:comment>
    </SpdxDocument>