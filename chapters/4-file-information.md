# 4 File Information（ファイル情報）

ソフトウェア パッケージ内の各ファイルごとに 1つのFile Information（ファイル情報）インスタンスが必要である。それは、ライセンスや著作権を含む対象ファイルの重要なメタデータを提供する。SPDX 2.0を使う場合には、ファイル セットを包含するパッケージは必ずしも必要ではない。

`tag:value`フォーマットを実装するときは、ファイル要素の位置は構文的に重要である。

パッケージが存在する場合は、ファイルは直前に置かれるPackage Information（パッケージ情報）と関係づけられることが仮定される。
明示的なRelationship（関係）が使われない限り、新しいPackage Information（パッケージ情報）の存在は、先行するパッケージと関連するファイルセットの終了を示す。
パッケージがファイルを含む場合は、File Information（ファイル情報）セクションはPackage Information（パッケージ情報）セクションに後続しなければならない。
ファイルがどのパッケージにも含まれない場合は、SPDX文書内のいずれのPackage Information（パッケージ情報）セクション参照よりも先行しなければならない。
`tag:value` フォーマットでは、ファイルの記述を開始する最初のフィールドはFile Name（ファイル名）でなければならない。
File information（ファイル情報）は、先行するFile Name（ファイル名）と関係づけられる。
ファイルに対するAnnotations（注釈）とファイルからのRelationships（関係）は、ファイル情報の後で、次のファイルかPackage Information（パッケージ情報）セクションの前に置かれる。

RDFでファイル情報を実装する場合は、`spdx:hasFile`属性はパッケージとファイルを関係づけるために使用される。

## 4.1 File Name（文書名） <a name="4.1"></a>

**4.1.1** 目的：このセクション中のファイル情報に対応するフルパスとファイル名を特定する。

**4.1.2** 意図：ファイル情報に対応する正しいファイルを見つける手助けをする。

**4.1.3** 基数：必須、1

**4.1.4** データフォーマット：パッケージアーカイブやディレクトリのルートからの相対ファイル名。

一般的に、すべてのファイル名は`./`が先行する。構文については、[http://www.ietf.org/rfc/rfc3986.txt](http://www.ietf.org/rfc/rfc3986.txt) を参照。

**4.1.5** Tag: `FileName:`

例：

    FileName: ./package/foo.c

**4.1.6** RDF: Property `spdx:fileName` in class `spdx:File`

例：

    <File rdf:about="...">
      <fileName>./package/foo.c</fileName>
      ...
    </File>

## 4.2 File SPDX Identifier（ファイルSPDX識別子） <a name="4.2"></a>

**4.2.1** 目的：他の要素から参照されるSPDX文書内の各要素を一意に特定する。これらは、内部から参照され、SPDX文書識別子と組み合わせて外部からも参照される。

**4.2.2** 意図：SPDX文書内には、同じファイルの複数バージョンが存在する可能性がある。要素間の関係を明確に示せるように、各要素を一意に参照できる必要がある。

**4.2.3** 基数：必須、1

**4.2.4** データ フォーマット："SPDXRef-"`[idstring]`

ここで `[idstring]` は一意の文字、数字、`.` かつ／または`-`.を含む文字列。

**4.2.5** Tag: `SPDXID:`

例：

    SPDXID: SPDXRef-1

**4.2.6** RDF: 要素のURIは以下のフォームに従う：[SpdxDocumentURI]#SPDXRef-[idstring] ここで [SpdxDocumentURI] は要素を含んでいるSPDX文書へのURIである

`xml:base`を使用した例：

    <rdf:RDF xml:base="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349A1B"
    ...
    <File rdf:ID=”SPDXRef-1”>
      ...
    </File>

URIを使用した例：

    <File rdf:about="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349A1B#SPDXRef-1">
      ...
    </File>

## 4.3 File Type（ファイル タイプ） <a name="4.3"></a>

**4.3.1** 目的：このフィールドは特定された対象ファイルのタイプに関する情報を提供する。ファイル タイプはファイルに本質的なもので、ファイルがどのように使われているかとは関係がない。ファイルは1以上のファイル タイプを持つことができるが、このフィールドへの記載は以下に限定される：

* `SOURCE` （ソース）　ファイルが人に可読なソースコード（C、HTML、他）である場合；
* `BINARY` （バイナリー）　ファイルがコンパイルされたオブジェクト、ターゲット イメージ、または実行形式（.o、.a、他）である場合 ；
* `ARCHIVE` （アーカイブ）　ファイルがアーカイブ（.tar、.jar、他）である場合；
* `APPLICATION` アプリケーション）　ファイルが特定のアプリケーション タイプ（MIME type of application/*）である場合；
* `AUDIO` （オーディオ）　ファイルがオーディオ ファイル（MIME type of audio/*、たとえば.mp3）に関連付けられる場合；
* `IMAGE` （イメージ）　ファイルが画像イメージ（MIME type of image/*、例えば .jpg、.gif）に関連付けられる場合；
* `TEXT` （テキスト）　ファイルが人に可読なテキスト ファイル（MIME type of text/*）である場合；
* `VIDEO` （ビデオ）　ファイルがビデオ ファイル タイプ（MIME type of video/*）に関連付けられる場合；
* `DOCUMENTATION` （ドキュメンテーション）　ファイルがドキュメンテーション（専門知識の記録）として機能する場合；
* `SPDX` ファイルがSPDX文書である場合；
* `OTHER` （その他）　ファイルが上記カテゴリーに当てはまらない（生成物、データ ファイル、他）場合。

**4.3.2** 意図：このフィールドは、開発者視点でのファイル タイプの合理的な判断である。

**4.3.3** 基数：任意、複数

**4.3.4** データ フォーマット： `SOURCE` | `BINARY` | `ARCHIVE` | `APPLICATION` | `AUDIO` | `IMAGE` | `TEXT` | `VIDEO` | `DOCUMENTATION` | `SPDX` | `OTHER`

**4.3.5** Tag: `FileType:`

例：

    FileType: BINARY

例：(`README.TXT`)

    FileType: TEXT
    FileType: DOCUMENTATION

例 (foo.exe)

    FileType: BINARY
    FileType: APPLICATION

**4.3.6** RDF: Property `spdx:fileType` in class `spdx:File`

例：

    <File rdf:about="file1">
      <fileType rdf:resource="fileType_binary" />
    </File>

例：( ここで file2 は `README.TXT`)

    <File rdf:about="file2">
      <fileType rdf:resource="http://spdx.org/rdf/terms#fileType_text" />
      <fileType rdf:resource="http://spdx.org/rdf/terms#fileType_documentation" />
    </File>

## 4.4 File Checksum（ファイル チェックサム） <a name="4.4"></a>


**4.4.1** 目的：パッケージ内の各ファイルの解析情報と一致する一意の識別子を提供する。

**4.4.2** 意図：各ファイルの一意の識別子を提供することで、あるファイルのバージョンや変更に関する混乱を低減する。

**4.4.3** 基数：必須、1　SHA1、他は任意で提供される。

**4.4.4** アルゴリズム：SHA1()がファイルに使用される。任意で提供可能な他のアルゴリズムは、SHA256()、MD5()を含む。

**4.4.5** データ フォーマット：`tag:value` フォーマットでは、3つの要素からなる。アルゴリズム識別子（SHA1）、分離子(“:”)、およびチェックサム値である。RDFは、アルゴリズム識別子とチェックサム値を含む。たとえば、アルゴリズム識別子がSHA1の場合は、チェックサム値は小文字16進数40桁で表現された160ビット値となるべきである。他のアルゴリズムでは、適切な桁数の16進数が期待される。

**4.4.6** Tag: `FileChecksum:`

例：

    FileChecksum: SHA1: d6a770ba38583ed4bb4525bd96e50461655d2758

    FileChecksum: MD5: 624c1abb3664f4b35547e7c73864ad24

**4.4.7** RDF: Property `spdx:Checksum` in class `spdx:File`

例：

    <File rdf:about="...">
      <checksum>
        <Checksum>
          <algorithm rdf:resource="http://spdx.org/rdf/terms#checksumAlgorithm_sha1"/>
          <checksumValue>d6a770ba38583ed4bb4525bd96e50461655d2758
          </checksumValue>
        </Checksum>
      </checksum>
      <checksum>
        <Checksum>
          <algorithm rdf:resource="http://spdx.org/rdf/terms#checksumAlgorithm_md5"/>
          <checksumValue> 624c1abb3664f4b35547e7c73864ad24
          </checksumValue>
        </Checksum>
      </checksum>
    </File>

## 4.5 Concluded License（結論されたライセンス） <a name="4.5"></a>

**4.5.1** 目的：このフィールドは、SPDXファイル作成者がファイルに適用されると結論したライセンスを与える。ライセンスを決定できない場合には代替値を与える。

このフィールドへの記入は以下に限られる：

[Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なSPDXライセンス表現；

`NONE` このファイル適用できるライセンスが無い場合；

`NOASSERTION` 以下の場合：

(i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

(ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

(iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

もし、Concluded License（結論されたライセンス）がファイル中のライセンス情報と異なる場合、Comments on License（ライセンスへのコメント、[(セクション 4.7)](#4.7)参照）フィールドに説明を記載すべきである。`NOASSERTION`に関しては、Comments on License（ライセンスへのコメント、[(セクション 4.7)](#4.7) ）フィールドに説明を記載した方が良い。

**4.5.2** 意図：SPDXファイル作成者がファイル中のライセンス情報[(セクション 4.6)](#4.6) や他の客観的情報（たとえば“COPYING FILE”（COPYINGファイル））とスキャンツール結果とを合わせて解析を行い、ファイルに適用されるライセンスは何かについて合理的に客観性のある結論に到達すること。

**4.5.3** 基数：必須、1

**4.5.4** データフォーマット：`<SPDX License Expression>` | `NONE` | `NOASSERTION`

ここで

`<SPDX License Expression>` は、Appendix IVで定義された有効なSPDXライセンス表現。

**4.5.5** Tag: `LicenseConcluded:`

例：

    LicenseConcluded: LGPL-2.0

例：

    LicenseConcluded: (LGPL-2.0 OR LicenseRef-2)

**4.5.6** RDF: Property `spdx:licenseConcluded` in class `spdx:File`

例：

    <File rdf:about="file">
      <licenseConcluded>LGPL-2.0</licenseConcluded>
    </File>

例：

    <File rdf:about="...">
      <licenseConcluded>
        <DisjunctiveLicenseSet>
          <member rdf:resource="http://spdx.org/licenses/LGPL-2.0"/>
          <member rdf:resource="#LicenseRef-2"/>
        </DisjunctiveLicenseSet>
      </licenseConcluded>
    </File>

## 4.6 License Information in File（ファイル中のライセンス情報） <a name="4.6"></a>

**4.6.1** 目的：このフィールドはファイル中で実際に発見されたライセンス情報を含む。この情報はファイルのヘッダーでもっともよく見つかるが、他の場所にあることもある。ファイル中で実際には見つからないライセンス情報、たとえば トップレベル  ディレクトリーに置かれた”COPYING.txt” ファイル、はこのフィールドに反映させるべきではない。

このフィールドへの記入は以下に限られる：

ライセンスがSPDXライセンス リストにある場合には、SPDXライセンス リスト簡易形式識別子；
ライセンスがSPDXライセンス リストにない場合には、LicenseRef-`[idstring]` で示すユーザー定義参照；

`NONE`ファイルがライセンス情報を何も含まない場合；

`NOASSERTION` 以下の場合：

(i) SPDXファイル作成者が、このフィールドを決定しようと試みなかった。；

(ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

ファイルが2つ以上のライセンスを含む場合、または、ライセンス情報がパッケージ受領者にライセンスの選択を提示する場合は、各選択肢を別のエントリーとしてリストするべきである。

**4.6.2** 意図：Concluded License（結論されたライセンス）フィールドとの違いは、ここにはファイル中の実際のライセンス情報を提供することである。

**4.6.3** 基数：任意、1以上

**4.6.4** データ フォーマット： `<SPDX License Expression>` |

 ["DocumentRef-"`[idstring]`":"]"LicenseRef-"`[idstring]` |

 | `NONE` | `NOASSERTION`

ここで

`<SPDX License Expression>` は、[Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なPDXライセンス表現。

* "DocumentRef-"`[idstring]` ：[セクション 2.6](2-document-creation-information.md#2.6)で記述される外部SPDX文書への任意の参照

`[idstring]` は、文字、数字、`.` かつ／または `-`を含む一意の文字列。

**4.6.5** Tag: `LicenseInfoInFile:`

例：

    LicenseInfoInFile: GPL-2.0
    LicenseInfoInFile: LicenseRef-2

**4.6.6** RDF: Property `spdx:licenseInfoInFile` in class `spdx:File`

例：

    <File rdf:about="file1">
      <licenseInfoInFile rdf:resource="http://spdx.org/licenses/GPL-2.0" />
      <licenseInfoInFile rdf:resource="#LicenseRef-2" />
    </File>

## 4.7 Comments on License（ライセンスへのコメント） <a name="4.7"></a>

**4.7.1** 目的：このフィールドは、SPDXファイル作成者が、関連する背景情報や、ファイルに対するConcluded License （結論されたライセンス）に至った解析について記録する場所を提供する。もし、Concluded License（結論されたライセンス）がファイルのLicense Information（ライセンス情報）と異なる場合、Comments on License（ライセンスへのコメント）フィールドに説明を記載すべきである。Concluded License（結論されたライセンス）が`NOASSERTION`の場合にも、説明を記載することが望まれる。

**4.7.2** 意図：SPDXファイルの受領者に、Concluded License（結論されたライセンス）がファイルのライセンス情報と一致しない場合や`NOASSERTION`が設定されている場合に、Concluded License（結論されたライセンス）はどのように決定されたかの詳細説明、または、ファイルのライセンスを決定するのに有用な情報を提供する。

**4.7.3** 基数：任意、1

**4.7.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**4.7.5** Tag: `LicenseComments:`

`tag:value`フォーマットでは、これは `<text>...</text>` で分離される。

例：

    LicenseComments: <text>結論されたライセンスは、ファイルが含まれているパッケージから得られた。
    この情報は、xyzディレクトリーのCOPYING.txtファイルで見つかる。</text>

**4.7.6** RDF: Property `spdx:licenseComments` in class `spdx:File`

例：

    <File rdf:about="...">
      <licenseComments>
        結論されたライセンスは、ファイルが含まれているパッケージから得られた。この情報は、xyzディレクトリーのCOPYING.txtファイルで見つかる。このパッケージは、ソースとバイナリー形式で出荷された。
      </licenseComments>
    </File>

## 4.8 Copyright Text（著作権テキスト） <a name="4.8"></a>

**4.8.1** 目的：ファイルの著作権保有者と日付を特定する。これは、実際のファイルから取り出した自由形式のテキスト フィールドである。

このフィールドへの記入は以下に限られる：

不完全なものも含めて、著作権表記に関連するすべてのテキスト；

`NONE` ファイルがライセンス情報を何も含まない場合；

`NOASSERTION` 以下の場合：

(i) SPDXファイル作成者が、このフィールドを決定しようと試みなかった。；

(ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**4.8.2** 意図：ファイルのすべての著作権表記を記録する。

**4.8.3** 基数：必須、1

**4.8.4** データ フォーマット：自由形式文（複数行に渡ってもよい） | `NONE` | `NOASSERTION`

**4.8.5** Tag: `FileCopyrightText:`

`tag:value`フォーマットでは、これは `<text>...</text>` で分離される。

例：

    FileCopyrightText: <text> Copyright 2008-2010 John Smith </text>

**4.8.6** RDF: Property `spdx:copyrightText` in class `spdx:File`

例：

    <File rdf:about="...">
      <copyrightText>
        Copyright 2008-2010 John Smith
      </copyrightText>
    </File>

## 4.9 Artifact of Project Name (deprecated)（派生元プロジェクト名）（廃止予定） <a name="4.9"></a>

**4.9.1** 目的：ファイルが特定のプロジェクトから派生したことを示す。

**4.9.2** 意図：SPDXファイル受領者が特定ファイルのオリジナル ソースを決定するのを容易にする。プロジェクトがSPDX文書に記述されていない場合は、ArtifactOfを使用可能である。

プロジェクトが他のSPDX文書で記述されている場合は、Relationship（関係）を使用すべきである。

**4.9.3** 基数：任意、1以上

**4.9.4** データ フォーマット：1行の文`tag:value`フォーマットでは、ArtifactOfProjectNameは、任意の属性（ArtifactOfHomePage とArtifactOfURI）の任意のArtifactOfに先行しなくてはならない。

**4.9.5** Tag: `ArtifactOfProjectName:`

例：

    ArtifactOfProjectName: Jena

**4.9.6** RDF: Property `spdx:artifactOf/doap:Project/doap:name`

例：

    <File>
      <artifactOf>
        <doap:Project>
          <doap:name>Jena</doap:name>
        </doap:Project>
      </artifactOf>
    </File>

## 4.10 Artifact of Project Homepage (deprecated) （派生元プロジェクト名）（廃止予定）<a name="4.10"></a>

**4.10.1** 目的：ファイルが発生したプロジェクトの位置を示す。

**4.10.2** 意図：SPDXファイル受領者が特定ファイルのオリジナル ソースを決定するのを容易にする。プロジェクトが他のSPDX文書で記述されている場合は、Relationship（関係）を使用すべきである。

**4.10.3** 基数：任意、1以上

**4.10.4** データ フォーマット：uniform resource locator（URL） | `UNKNOWN`.

`tag:value` フォーマットでは、すべての任意のArtifactOfフィールドはArtifactOfProjectNameの直後に続かないといけない。

**4.10.5** Tag: `ArtifactOfProjectHomePage:`

例：

    ArtifactOfProjectHomePage: http://www.openjena.org/

**4.10.6** RDF: `spdx:artifactOf/doap:Project/doap:homepage`

例：

    <File>
      <artifactOf>
        <doap:Project>
          <doap:homepage >rttp://www.openjena.org/</doap:homepage>
        </doap:Project>
      </artifactOf>
    </File>

## 4.11 Artifact of Project Uniform Resource Identifier (deprecated) （派生元プロジェクト統一資源識別子）（廃止予定）<a name="4.11"></a>

**4.11.1** 目的：DOAP文書のプロジェクト リソースへのリンクを提供し、サポートされる異なるフォーマット間の相互運用性を確保する。

**4.11.2** 意図：SPDXファイル受領者が特定ファイルのオリジナル ソースを決定するのを容易にする。プロジェクトが他のSPDX文書で記述されている場合は、Relationship（関係）を使用すべきである。

**4.11.3** 基数：任意、1以上

**4.11.4** データ フォーマット：uniform resource identifier.（統一資源識別子）

`tag:value`では、すべての任意のArtifactOfフィールドはArtifactOfProjectNameの直後に続かなければならない。

**4.11.5** Tag: `ArtifactOfProjectURI:`

例：

    ArtifactOfProjectURI: http://subversion.apache.org/doap.rdf

**4.11.6** RDF: `spdx:artifactOf/doap`

例：

    <File>
      <artifactOf rdf:resource="http://subversion.apache.org/" />
    </File>
    <!-- Note: within the DOAP file at http://subversion.apache.org/doap.rdf
      the value "http://subversion.apache.org/" is the URI of the describes
      resource of type doap:Project -->

## 4.12 File Comment（ファイル コメント）<a name="4.12"></a>

**4.12.1** 目的：このフィールドは、SPDXファイル作成者に、ファイルの一般的なコメントを記録する場所を提供する。

**4.12.2** 意図：SPDX文書の受領者に注意深いファイル解析の後に決定された情報を提供する。

**4.12.3** 基数：任意、1

**4.12.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**4.12.5** Tag: `FileComment:`

`tag:value`フォーマットでは、これは `<text>...</text>` で分離される。

例：

    FileComment: <text>
     このファイルは、FooやUfooなど他パッケージにもある。
    </text>

**4.12.6** RDF: Property `rdfs:comments` in class `spdx:File`

例：

    <File rdf:about="...">
      <rdfs:comment>
        このファイルは、FooやUfooなど他パッケージにもある。
      </rdfs:comment>
    </File>

## 4.13 File Notice（ファイル表記） <a name="4.13"></a>

**4.13.1** 目的：このフィールドは、SPDXファイル作成者に、ライセンス表記やファイル中で発見された関連する表記を記録する場所を提供する。著作権表記を含んでも含まなくてもよい。

**4.13.2** 意図：SPDXファイルの受領者に、追加のレビューが必要かもしれない表記やConcluded License（結論されたライセンス）の決定に貢献する表記を提供する。

**4.13.3** 基数：任意、1

**4.13.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**4.13.5** Tag: `FileNotice:`

`tag:value`フォーマットでは、これは `<text>...</text>` で分離される。

例：

    FileNotice: <text>このファイルはGPLでライセンスされている。</text>

**4.13.6** RDF: Property `noticeText` in class `spdx:File`

例：

    <File rdf:about="...">
      <noticeText>
        このファイルはGPLでライセンスされている。
      </noticeText>
    </File>

## 4.14 File Contributor（ファイル貢献者） <a name="4.14"></a>

**4.14.1** 目的：このフィールドは、SPDXファイル作成者に、ファイルの貢献者を記録する場所を提供する。貢献者には、著作権保有者、著作権保有者でないがファイル内容へ貢献した著者を含む。

**4.14.2** 意図：SPDXファイル受領者に1つ以上の貢献者（クレジット）を提供する。これは、ファイルの貢献者に対して謝辞を書く一つの方法である。例えば、受領した会社が著作権保有者に他のライセンスを相談するためにコンタクトするときに役に立つだろう。

**4.14.3** 基数：任意、1以上

**4.14.4** データ フォーマット：自由形式の1行文

**4.14.5** Tag: `FileContributor:`

`tag:value` フォーマットでは、貢献者1名あたり1行の割り当てである。

例：

    FileContributor: Modified by Paul Mundt lethal@linux-sh.org
    FileContributor: The Regents of the University of California
    FileContributor: IBM Corporation

**4.14.6** RDF: Property `fileContributor` in class `spdx:File`

例：

    <File rdf:about="...">
      <fileContributor> Modified by Paul Mundt lethal@linux-sh.org </fileContributor>
      <fileContributor> The Regents of the University of California </fileContributor>
      <fileContributor> IBM Corporation </fileContributor>
    </File>

## 4.15 File Dependencies (deprecated) （ファイル依存関係）（廃止予定）<a name="4.15"></a>

SPDX 2.0から、関係についてより細かい粒度を提供する[セクション7](7-relationships-between-SPDX-elements.md)の使用を推奨しているため、このフィールドは廃止予定である。

**4.15.1** 目的：このフィールドは、SPDXファイル作成者に、ファイルの派生元、または、ビルドで依存している他のファイル リスト（SPDXファイル内で参照可能）を記録する場所を提供する。ファイル リストは、必ずしもすべてのファイル依存関係を提供する必要はない。しかし、ライセンスに影響を与える、かつ／または、ファイルの頒布義務として必要となるものを含むべきである。

**4.15.2** 意図：SPDXファイル受領者に、ファイルをビルドしたビルドシステムに関するファイル依存関係を提供する。これらのファイルは、ファイルのライセンスに影響を与える可能性や、ファイルの頒布義務を満たすために必要になる可能性がある。

**4.15.3** 基数：任意、1以上

**4.15.4** データ フォーマット：SPDX文書内のファイルへの参照。`tag:value` フォーマットでは、これはファイル名となる。RDF フォーマットでは、これは実際のファイル ノードへの参照となる。

**4.15.5** Tag: `FileDependency:`

例：

    FileDependency:./busybox-1.20.2/shell/match.h
    FileDependency:./busybox-1.20.2/shell/match.c
    FileDependency:./busybox-1.20.2/shell/ash.c

**4.15.6** RDF: Property `spdx:fileDependency` in class `spdx:File`

例：

    <File rdf:nodeID="A0">
      <fileName>./package/source1.java</fileName>
    </File>

    <File rdf:nodeID="A1">
      <fileName>./package/source2.java</fileName>
    </File>

    <File rdf:nodeID="A3">
      <fileName>./package/source3.java</fileName>
    </File>

    <File rdf:about="...">
      <fileName>./package/mylibrary.jar</fileName>
      <fileDependency rdf:nodeID="A0"/>
      <fileDependency rdf:nodeID="A1"/>
      <fileDependency rdf:nodeID="A2"/>
    </File>