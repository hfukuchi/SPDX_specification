# 5 Snippet Information（コード断片情報）

Snippets（コード断片）は、あるファイルが他のオリジナル ソースから取り入れられた内容を含むとわかっている場合に任意で使用可能である。これらは、ファイルの一部分が最初は他のライセンスの下で作成されたことを示すのに役に立つ。

Snippet Information（コード断片情報）の各インスタンスは、SPDX文書の特定ファイルと関連付けられている必要がある。

タグ値フォーマットで記述する場合は、Snippet（コード断片）要素の位置は構文上重要である。

File（ファイル）がSnippets（コード断片）を含む場合は、Snippet Information（コード断片情報）セクションは関連するFile Information（ファイル情報）セクション（文書に存在する場合）に後続するべきである。
明確なRelationship（関係）を使用しない限り、 新しいファイルやパッケージ セクションの存在はオリジナルファイルに関連付けられるコード断片セットの終了を意味する。
`tag:value`フォーマットでは、Snippet（コード断片）の記述を開始する最初のフィールドは、Snippet Identifier（コード断片識別子）でなければならない。
Snippet（コード断片）に対するAnnotations（注釈）とSnippet（コード断片）からのRelationships（関係）は、次のファイルかPackageセクションの前で、Snippet Information（コード断片情報）の後に置かれる。

## 5.1 Snippet SPDX Identifier（コード断片SPDX識別子） <a name="5.1"></a>

**5.1.1** 目的：他の要素から参照されるSPDX文書内の各要素を一意に特定する。これらは、内部から参照され、SPDX文書識別子と組み合わせて外部からも参照される。

**5.1.2** 意図：SPDX文書内に複数のコード断片のインスタンスを持てる。各コード断片は一意に参照できなければならないので、コード断片と他要素は明確に関連付けられる。

**5.1.3** 基数：必須、1

**5.1.4** データ フォーマット：`SPDXRef-[idstring]`

ここで `[idstring]` は一意の文字、数字、`.` かつ／または`-`.を含む文字列。

**5.1.5** Tag: `SnippetSPDXID:`

例：

    SnippetSPDXID: SPDXRef-1

**5.1.6** RDF: 要素のURIは以下のフォームに従う：`[SpdxDocumentURI]#SPDXRef-[idstring]`  ここで `[SpdxDocumentURI]` は要素を含んでいる

xml:baseを使用した例：

    <rdf:RDF xml:base="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349A1B"
    ...
    <Snippet rdf:ID=”SPDXRef-1”>
      ...
    </Snippet>

URIを使用した例：

    <Snippet rdf:about="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349...">
      ...
    </Snippet>

## 5.2 Snippet from File SPDX Identifier（ファイル由来コード断片SPDX識別子） <a name="5.2"></a>

**5.2.1** 目的：コード断片が関連付けられているSPDX文書中のファイルを位置に特定する。

**5.2.2** 意図：SPDX文書内には、同じファイルの複数バージョンが存在する可能性がある。各要素は、一意に参照できる必要があるので、要素間の関係は明確に示すことができる。

**5.2.3** 基数：必須、1

**5.2.4** データ フォーマット： ["DocumentRef-"[idstring]":"] SPDXID

ここで `DocumentRef-[idstring]`：[セクション 2.6](2-document-creation-information.md#2.6)で記述される外部SPDX文書への任意の参照

ここで `SPDXID` は文字、数字、`.` かつ／または `-`を含む文字列。各セクションで記載(2.3, 3.2, 4.2).

**5.2.5** Tag: `SnippetFromFileSPDXID:`

例（ローカルSPDX文書中のファイル由来のコード断片）

    SnippetFromFileSPDXID: SPDXRef-filecontainingsnippet

例（外部SPDX文書中のファイル由来のコード断片）

    SnippetFromFileSPDXID: DocumentRef-ExternalDoc1:SPDXRef-filecontainingsnippet

**5.2.6** RDF: Property `spdx:snippetFromFile` in class `spdx:Snippet`

例（ローカルSPDX文書中のファイル由来のコード断片）

    <Snippet “rdf:ID=”SPDXRef-1”>
    <snippetFromFile rdf:about=”#SPDXRef-filecontainingsnippet”>
      ...
    </Snippet>

例（外部SPDX文書中のファイル由来のコード断片）

    <Snippet “rdf:ID=”SPDXRef-1”>
    <snippetFromFile rdf:about=”http://foo.org/ExternalDocument1#SPDXRef-filecontainingsnippet”>
      ...
    </Snippet>

## 5.3 Snippet Byte Range（コード断片バイト範囲） <a name="5.3"></a>

**5.3.1** 目的：このフィールドはコード断片情報が適用されるオリジナル ホスト ファイル(in [5.2](#5.2)) のバイト範囲を定義する。

**5.3.2** 意図：バイト範囲は、さまざまなフォーマットに起因する懸念とは無縁であり、差分を参照するもっとも正確な方法である。選択は、バイト範囲の番号付けを1で開始し、W3Cに従って行われる。（参照 http://www.w3.org/TR/Pointers-in-RDF10/）

**5.3.3** 基数：必須、1

**5.3.4** データ フォーマット： `number1:number2`

ここで`number1` は1以上で`number2`未満

かつ`number2`はファイルの全バイト数以下である。

位置number1と位置number2は範囲に含まれる。

**5.3.5** Tag: `SnippetByteRange:`

例：

    SnippetByteRange: 310:420

**5.3.6** RDF: Property `spdx:byteRange` in class `spdx:Snippet`. RDFはW3C提案のポインター法ボキャブラリーを使う（参照 [http://www.w3.org/TR/Pointers-in-RDF10/](http://www.w3.org/TR/Pointers-in-RDF10/)）

ポインター法ボキャブラリーでサポートされるクラスは、StartEndPointerとByteOffsetPointerである。ポインター法ボキャブラリーでサポートされる属性は、以下を含む：

* startPointer
* endPointer
* reference
* offset

例：

    xmlns:ptr=http://www.w3.org/2009/pointers#

    <Snippet rdf:about="...">
      <range>
        <ptr:StartEndPointer>
          <ptr:startPointer>
            <ptr:ByteOffsetPointer>
              <ptr:reference rdf:resource="#SPDXRef-fileReference/>
              <ptr:offset>310</ptr:offset>
            </ptr:ByteOffsetPointer>
          </ptr:startPointer>
          <ptr:endPointer>
            <ptr:ByteOffsetPointer>
              <ptr:referencerdf:resource="#SPDXRef-fileReference/>
              <ptr:offset>420</ptr:offset>
            </ptr:ByteOffsetPointer>
          </ptr:endPointer>
        </ptr: StartEndPointer>
      </range>
    </Snippet>

## 5.4 Snippet Line Range（コード断片ライン範囲） <a name="5.4"></a>

**5.4.1** 目的：このフィールドはコード断片情報が適用されるオリジナル ホスト ファイル(in [5.2](#5.2)) のライン範囲を定義する。バイト範囲とライン範囲に矛盾がある場合には、バイト範囲が優先される。

**5.4.2** 意図：既知のライン デリミターがある場合、ライン範囲はファイルへの便利な参照方法である。選択は、ライン範囲の番号付けを1で開始し、W3Cに従って行われる。（参照 http://www.w3.org/TR/Pointers-in-RDF10/）

**5.4.3** 基数：任意、1

**5.4.4** データ フォーマット：`number1:number2`

ここで

`number1` は1以上で`number2`未満
かつ `number2` はファイルの全バイト数以下である。

**5.4.5** Tag: `SnippetLineRange:`

例：

    SnippetLineRange: 5:23

**5.4.6** RDF: properties `spdx:byteRange` in class `spdx:Snippet`. RDFはW3C提案のポインター法ボキャブラリーを使う（参照 http://www.w3.org/TR/Pointers-in-RDF10/）

ポインター法ボキャブラリーでサポートされるクラスは、 `StartEndPointer` と `LineCharPointer`. ポインター法ボキャブラリーでサポートされる属性は、以下を含む：

* `startPointer`
* `endPointer`
* `reference`
* `lineNumber`

例：

`xmlns:ptr=http://www.w3.org/2009/pointers#`

    <Snippet rdf:about="...">
      <range>
        <ptr:StartEndPointer>
          <ptr:startPointer>
            <ptr:LineCharPointer>
            <ptr:reference rdf:resource="#SPDXRef-fileReference"/>
            <ptr:lineNumber>5</ptr:lineNumber>
          </ptr:LineCharPointer>
        </ptr:startPointer>
        <ptr:endPointer>
          <ptr:LineCharPointer>
            <ptr:reference rdf:resource="#SPDXRef-fileReference"/>
            <ptr:lineNumber>23</ptr:lineNumber>
          </ptr:LineCharPointer>
        </ptr: StartEndPointer>
      </range>
    </Snippet>

## 5.5 Snippet Concluded License （コード断片結論されたライセンス）<a name="5.5"></a>

**5.5.1** 目的：このフィールドは、SPDXファイル作成者がコード断片に適用されると結論したライセンスを与える。ライセンスを決定できない場合には代替値を与える。このフィールドへの記入は以下に限られる：

Appendix IVで定義された有効なSPDX License Expression（SPDXライセンス表現）。

`NONE` コード断片に対するライセンスを決定する情報がない場合NONEが使用されるべきである。

`NOASSERTION` コード断片が以下の場合には、NOASSERTIONが使用されるべきである：

(i) SPDXファイル作成者が、特定を試みたが、Concluded License（結論されたライセンス）を合理的に決定できなかった；

(ii) SPDXファイル作成者は、いくつかのライセンス情報を参照したが、ライセンスの結論に満足していない；

(iii) SPDXファイル作成者は、Concluded License（結論されたライセンス）を決定しようと試みなかった；

(ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

もし、Concluded License（結論されたライセンス）がファイルのライセンスと異なる場合、Comments on License（ライセンスへのコメント、[(セクション 5.7)](#5.7)参照）フィールドに説明を記載すべきである。`NOASSERTION`に関しては、Comments on License（ライセンスへのコメント、[(セクション 5.7)](#5.7) ）フィールドに説明を記載した方が良い。

**5.5.2** 意図：SPDX文書作成者が、コード断片に関する既知のライセンス情報、ファイル自体にあるライセンス情報、パッケージに関する他の客観的情報、およびスキャンツールからの結果に基づき、コード断片に適用されるライセンスは何かについて合理的に客観性のある結論に到達すること。

**5.5.3** 基数：必須、1

**5.5.4** データフォーマット： `<SPDX License Expression>` | `NONE` | `NOASSERTION`

ここで

`<SPDX License Expression>` は、Appendix IVで定義された有効なSPDXライセンス表現。

**5.5.5** Tag: `SnippetLicenseConcluded:`

例：

    SnippetLicenseConcluded: GPL-2.0

例：

    SnippetLicenseConcluded: (LGPL-2.0 OR LicenseRef-2)

**5.5.6** RDF: Property `spdx:licenseConcluded` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...">
      ...
      <licenseConcluded>GPL-2.0</licenseConcluded>
      ...
    </Snippet>

例：

    <Snippet rdf:about="...">
      <licenseConcluded>
        <DisjunctiveLicenseSet>
          <member rdf:resource="http://spdx.org/licenses/LGPL-2.0"/>
          <member rdf:resource="#LicenseRef-2"/>
        </DisjunctiveLicenseSet>
      </licenseConcluded>
    </Snippet>

## 5.6 License Information in Snippet（コード断片中のライセンス情報） <a name="5.6"></a>

**5.6.1** 目的：このフィールドはコード断片中で実際に発見されたライセンス情報を含む。コード断片中で実際には見つからないライセンス情報、たとえば コード断片が含まれるファイルのヘッダーや、トップレベル ディレクトリーに置かれた”COPYING.txt” ファイル、はこのフィールドに反映させるべきではない。

このフィールドへの記入は以下に限られる：

ライセンスがSPDXライセンス リストにある場合には、SPDXライセンス リスト簡易形式識別子；
ライセンスがSPDXライセンス リストにない場合には、LicenseRef-`[idstring]` で示すユーザー定義参照；

`NONE` コード断片がライセンス情報を何も含まない場合；

`NOASSERTION` 以下の場合：

(i) SPDXコード断片作成者が、このフィールドを決定しようと試みなかった。；

(ii) SPDXコード断片作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

コード断片に2つ以上のライセンス情報が含まれる場合、ライセンス情報が選択を提供する場合は、各選択肢を別のエントリーとしてリストするべきである。

**5.6.2** 意図：Concluded License（結論されたライセンス）フィールドとの違いは、ここにはコード断片中の実際のライセンス情報を提供する。

**5.6.3** 基数：任意、1以上

**5.6.4** データ フォーマット： `<SPDX License Expression>` |

["DocumentRef-"`[idstring]`:"]"LicenseRef-"[idstring] |

| `NONE` | `NOASSERTION`

ここで

`<SPDX License Expression>` は、[Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なPDXライセンス表現。

* "DocumentRef-"`[idstring]` ：[セクション 2.6](2-document-creation-information.md#2.6)で記述される外部SPDX文書への任意の参照

`[idstring]` は、文字、数字、`.` かつ／または `-`を含む一意の文字列。

**5.6.5** Tag: `LicenseInfoInSnippet:`

例：

    LicenseInfoInSnippet: LGPL-2.0

    LicenseInfoInSnippet: LicenseRef-2

**5.6.6** RDF: Property `spdx:licenseInfoInSnippet` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...">
      <licenseInfoInSnippet rdf:resource="http://spdx.org/licenses/GPL-2.0" />
      <licenseInfoInSnippet rdf:resource="#LicenseRef-2" />
    </Snippet>

## 5.7 Snippet Comments on License （コード断片結論されたライセンス）<a name="5.7"></a>

**5.7.1** 目的：このフィールドは、SPDXファイル作成者が関連する背景情報やコード断片に対する結論されたライセンスに至った解析について記録する場所を提供する。

**5.7.2** 意図：コード断片に対するConcluded License（結論されたライセンス）がファイルのライセンス情報と一致しない場合や`NOASSERTION`,が設定されている場合に、Concluded License（結論されたライセンス）はどのように決定されたかの詳細説明、または、ファイル中のコード断片のライセンスを決定するのに有用な情報をSPDXファイルの受領者に提供する。

**5.7.3** 基数：任意、1

**5.7.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**5.7.5** Tag: `SnippetLicenseComments:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例：

    SnippetLicenseComments: <text>結論されたライセンスはパッケージxyzから得られた。コード断片はそこからコピーされて現在のファイルに取り込まれた。
      結論されたライセンス情報は、パッケージxyz中のCOPYING.txt file in package xyzファイルで検出された。</text>

**5.7.6 ** RDF: Property `spdx:licenseComments` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...”>
      ...
      <licenseComments>
        結論されたライセンスはパッケージxyzから得られた。コード断片はそこからコピーされて現在のファイルに取り込まれた。結論されたライセンス情報は、パッケージxyz中のCOPYING.txt file in package xyzファイルで検出された。
      </licenseComments>
      ...
    </Snippet>

## 5.8 Snippet Copyright Text（コード断片著作権テキスト） <a name="5.8"></a>

**5.8.1** 目的：コード断片の著作権保有者と日付を特定する。これは、実際のコード断片から取り出した自由形式のテキストを記入するフィールドである。このフィールドへの記入は以下に限られる：

不完全なものも含めて、著作権表記に関連するすべてのテキスト；

`NONE` ファイルがライセンス情報を何も含まない場合；

`NOASSERTION` SPDX文書作成者が実際のファイルのコンテンツを確認しなかった場合、SPDXファイル作成者が意図的に情報を提供しなかった場合（特に意味がないことを、そうすることで暗示するべきである）。

**5.8.2** 意図：コード断片のすべての著作権表記を記録する。

**5.8.3** 基数：必須、1

**5.8.4** データ フォーマット：自由形式文（複数行に渡ってもよい）| `NONE` | `NOASSERTION`

**5.8.5** Tag: `SnippetCopyrightText:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例：

    SnippetCopyrightText: <text> Copyright 2008-2010 John Smith </text>

**5.8.6** RDF: Property `spdx:copyrightText` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...">
      ...
      <copyrightText>
        Copyright 2008-2010 John Smith
      </copyrightText>
      ...
    </Snippet>

## 5.9 Snippet Comment （コード断片コメント）<a name="5.9"></a>

**5.9.1** 目的：このフィールドは、SPDXファイル作成者に、コード断片に対する一般的なコメントを記録する場所を提供する。

**5.9.2** 意図：SPDX文書の受領者に注意深いコード断片解析の後に決定された情報を提供する。

**5.9.3** 基数：任意、1

**5.9.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**5.9.5** Tag: `SnippetComment:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例：

    SnippetComment: <text>このコード断片は、商用スキャンツールがGPL-2.0でライセンスされたパッケージxyz中のファイルfoo.cから派生したと検出しており、重要項目としてこのApache-2.0ファイル中でハイライトされた。</text>

**5.9.6** RDF: Property `rdfs:comment` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...">
      ...
      <rdfs:comment>
        このコード断片は、商用スキャンツールがGPL-2.0でライセンスされたパッケージxyz中のファイルfoo.cから派生したと検出しており、重要項目としてこのApache-2.0ファイル中でハイライトされた。
      </rdfs:comment>
      ...
    </Snippet>

## 5.10 Snippet Name （コード断片名）<a name="5.10"></a>

**5.10.1** 目的：人間に便利な方法でコード断片を特定する。

**5.10.2** 意図：著作権対象のSPDX Element（SPDX要素）は名前で参照するという一貫性の下、複数個所で使用されている対象のコード断片を特定する助けとなる。

**5.10.3** 基数：任意、1

**5.10.4** データ フォーマット：1行の文

**5.10.5** Tag: `SnippetName:`

例：

    SnippetName: from linux kernel

5.10.6 RDF: Property `spdx:snippetName` in class `spdx:Snippet`

例：

    <Snippet rdf:about="...">
      <name>from linux kernel</name>
    </Snippet>