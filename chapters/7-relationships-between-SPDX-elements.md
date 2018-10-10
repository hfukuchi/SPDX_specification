# 7 Relationships between SPDX Elements（SPDX要素間の関係）

## 7.1 Relationship（関係） <a name="7.1"></a>

**7.1.1** 目的：このフィールドは2つのSPDX要素間の関係に対する情報を提供する。たとえば、2つの異なるファイル間、パッケージとファイル間、2つのパッケージ間、SPDX文書と他のSPDX文書間の関係を表現できる。サポートされる、2つの要素間の関係は以下である：

| Relationship（関係）| Description（説明） | Example（例） |
|------------------------|-------------|---------|
| DESCRIBES| SPDXRef-DOCUMENTがSPDXRef-Aを記述するときに使用される。| SPDX文書‘WildFly.spdx’がパッケージ‘WildFly’を記述する。注：これは、2つ以上のパッケージがあるかファイルセットがある場合に必須であるが、SPDX文書内にある関連する項目を整理するのを助ける論理的な関係である。|
| DESCRIBED_BY| SPDXRef-AがSPDXREF-Documentによって記述されるときに使用される。| パッケージ‘WildFly’はSPDX文書‘Wildfly.spdx’によって記述される。|
| CONTAINS| SPDXRef-AがSPDXRef-Bを含むときに使用される。| ARCHIVE（アーカイブ）ファイル‘bar.tgz’はSOURCE（ソース）ファイル‘foo.c’を含む。|
| CONTAINED_BY| SPDXRef-AがSPDXRef-Bによって含まれるときに使用される。| SOURCE（ソース）ファイル`foo.c`はARCHIVE（アーカイブ）ファイル‘bar.tgz’に含まれる。
| GENERATES| SPDXRef-AがSPDXRef-Bを生成するときに使用される。| SOURCE（ソース）ファイル‘makefile.mk’はBINARY（バイナリー）ファイル‘a.out’を生成する。
| GENERATED_FROM| SPDXRef-AがSPDXRef-Bから生成されたときに使用する。| BINARY（バイナリー）ファイル‘a.out’はSOURCE（ソース）ファイル‘makefile.mk’から生成された。BINARY（バイナリー）ファイル‘foolib.a’ はSOURCE（ソース）ファイル‘bar.c’から生成された。|
| ANCESTOR_OF| SPDXRef-AがSPDXRef-Bの先祖（同じ系統であるが古い日時のもの）であるときに使用する。| SOURCE（ソース）ファイル‘makefile.mk’はSOURCE（ソース）ファイル‘makefile2.mk’のオリジナル先祖のバージョンである。
| DESCENDANT_OF| SPDXRef-AがSPDXRef-Bの子孫（同じ系統であるが新しい日時のもの）であるときに使用する。| SOURCE（ソース）ファイル‘makefile2.mk’はオリジナルSOURCE（ソース）ファイル‘makefile.mk’の子孫である。
| VARIANT_OF| SPDXRef-AがSPDXRef-Bの変形（同じ系統であるが、前後関係が不明のもの）であるときに使用する。|2つが少しの編集によってしか異ならないが、どちらが先であるかを決められない（信頼できる日時情報がない）場合は、SOURCE（ソース）ファイル‘makefile2.mk’はSOURCE（ソース）ファイル‘makefile.mk’の変形である。|
| DISTRIBUTION_ARTIFACT| SPDXRef-Aの頒布にSPDXRef-Bの頒布も必要であるときに使用する。| BINARY（バイナリー）ファイル‘foo.o’はARCHIVE（アーカイブ）ファイル‘bar-sources.tgz’も頒布されることを必要とする。|
| PATCH_FOR| SPDXRef-AがSPDXRef-Bに適用すべきパッチ ファイルであるときに使用する。| SOURCE（ソース）ファイル‘foo.diff’はSOURCE（ソース）ファイル‘foo.c’のパッチファイルである。|
| PATCH_APPLIED| SPDXRef-AがSPDXRef-Bに適用済みのパッチ ファイルであるときに使用する。| SOURCE（ソース）ファイル‘foo.diff’はSOURCE（ソース）ファイル‘foo-patched.c’に適用済みのパッチ ファイルである。|
| COPY_OF| SPDXRef-AがSPDXRef-Bの厳密なコピーであるときに使用する。| BINARY（バイナリー）ファイル‘alib.a’はBINARY（バイナリー）ファイル‘a2lib.a’の厳密なコピーである。|
| FILE_ADDED| SPDXRef-AがSPDXRef-Bに追加されたファイルであるときに使用する。| SOURCE（ソース）ファイル‘foo.c’はARCHIVE（アーカイブ）ファイル‘bar.tgz’に追加された。|
| FILE_DELETED| SPDXRef-AがSPDXRef-Bから削除されたファイルであるときに使用する。| SOURCE（ソース）ファイル‘foo.diff’’はパッケージARCHIVE（アーカイブ）‘bar.tgz’から削除された。|
| FILE_MODIFIED| SPDXRef-AがSPDXRef-Bを基に変更したファイルであるときに使用する。| SOURCE（ソース）ファイル‘foo.c’’はSOURCE（ソース）ファイル‘foo.orig.c’を変更して作成された。|
| EXPANDED\_FROM_ARCHIVE | SPDXRef-AがアーカイブSPDXRef-Bを拡張して作成されたときに使用する。| SOURCE（ソース）ファイル‘foo.c’は、ARCHIVE（アーカイブ）ファイル‘xyz.tgz’を拡張して作成された。|
| DYNAMIC_LINK| SPDXRef-AがSPDXRef-Bに動的にリンクするときに使用する。| APPLICATION（アプリケーション）ファイル‘myapp’はBINARY（バイナリー）ファイル‘zlib.so’に動的にリンクする。|
| STATIC_LINK| SPDXRef-AがSPDXRef-Bに静的にリンクするときに使用する。| APPLICATION（アプリケーション）ファイル‘myapp’はBINARY（バイナリー）ファイル‘zlib.a’に静的にリンクする。|
| DATA\_FILE_OF| SPDXRef-AがSPDXRef-Bで使われるデータファイルであるときに使用する。| IMAGE（イメージ）ファイル‘kitty.jpg’はAPPLICATION（アプリケーション）‘hellokitty’のデータファイルである。|
| TEST\_CASE_OF| SPDXRef-AがテストSPDXRef-Bで使われれるテスト ケースであるとき使用される。| SOURCE（ソース）ファイルtestMyCode.javaはAPPLICATION（アプリケーション） MyPackageのテストで使用するユニット テスト ファイルである。|
| BUILD\_TOOL_OF| SPDXRef-AがSPDXRef-Bをビルドするのに使われるときに使用される。| SOURCE（ソース）ファイル‘makefile.mk’はAPPLICATION（アプリケーション）‘zlib’をビルドするのに使用される。|
| DOCUMENTATION_OF| SPDXRef-AがSPDXRef-Bのドキュメンテーションを提供するときに使用する。| DOCUMENTATIONファイル‘readme.txt’はAPPLICATION（アプリケーション）‘zlib’の説明を提供する。|
| OPTIONAL\_COMPONENT_OF | SPDXRef-AがSPDXRef-Bの任意のコンポーネントであるときに使用する。| SOURCE（ソース）ファイル‘fool.c’（貢献者のディレクトリーにある）はAPPLICATION（アプリケーション）‘atthebar’のビルドに含めても含めなくてもよい。|
| METAFILE_OF| SPDXRef-AがSPDXRef-Bのメタファイルであるときに使用する。| SOURCE（ソース）ファイル‘pom.xml’はAPPLICATION（アプリケーション ‘Apache Xerces’のメタファイルである。|
| PACKAGE_OF| SPDXRef-AがSPDXRef-Bの一部としてパッケージとして使われるときに使用する。| LinuxディストリビューションはAPPLICATION（アプリケーション）パッケージgawkをディストリビューションMyLinuxDistroの一部として含む。|
| AMENDS| （最新の）SPDXRef-DOCUMENTがSPDXRef-Bに含まれるSPDX情報を修正するときに使用する。| （最新の）SPDX文書Aのバージョン2がSPDX文書Aバージョン1の訂正を含む。注：最新文書に対する予約識別子SPDXRef-DOCUMENTが必要となる。|
| PREREQUISITE_FOR| SPDXRef-AがSPDXRef-Bの前提条件であるときに使用する。|
| HAS_PREREQUISITE| SPDXRef-Aが前提条件SPDXRef-Bを有するときに使用する。 | APPLICATION（アプリケーション）‘foo.exe’ は‘bar.dll’を前提条件または依存関係として持つ。 |
| OTHER| 公式なSPDX仕様で定義されていない関係を記述するときに使用する。関係の記述はRelationship（関係）コメントフィールドに入れるべきである。| |

**7.1.2** 意図：このフィールドは、開発者視点からの、2つの識別された要素（すなわち、ファイル、パッケージ、文書）間の関係の合理的な推定である。

**7.1.3** 基数：任意、複数

\* 1つの必須ケースについては`DESCRIBES` 関係を参照

**7.1.4** データ フォーマット：

    ["DocumentRef-"[idstring]":"]SPDXID <relationship> ["DocumentRef-"[idstring]":"]SPDXID

ここで `DocumentRef-[idstring]`：[セクション 2.6](2-document-creation-information.md#2.6)で記述される外部SPDX文書への任意の参照

ここで `SPDXID` は文字、数字、`.` かつ／または `-`を含む文字列。各セクションで記載(2.3, 3.2, 4.2).

ここで`<relationship>`は、表7.1.1で記述された関係のうちの1つである。

**7.1.5** Tag: `Relationship:`

例：

    Relationship: SPDXRef-grep CONTAINS SPDXRef-make

    RelationshipComment: Package grep contains file make

    Relationship: SPDXRef-DOCUMENT AMENDS DocumentRef-SPDXA:SPDXRef-DOCUMENT

    RelationshipComment: This current document is an amendment of the SPDXA document.

**7.1.6** RDF: Property `relationship` in any SpdxElement

例：

    <SpdxElement rdf:about=”#SPDXRef-45”>
      <relationship>
        <Relationship>
          <spdx:relatedSpdxElement>
          <spdx:SpdxElement rdf:about="http://spdx.org/spdxdocs/spdx-tools-v1.2-3F2504E0-4F89-41D3-9A0C-0305E82...
          </spdx:relatedSpdxElement>
          <relationshipType>http://spdx.org/rdf/terms#relationshipType_contains</relationshipType>
        </Relationship>
      </relationship>
      ...
    </SpdxElement>

## 7.2 Relationship Comment（関係コメント） <a name="7.2"></a>

**7.2.1** 目的：このフィールドは、SPDXファイル作成者に、関係に対する一般的なコメントを記録する場所を提供する。

**7.2.2** 意図：SPDX文書の受領者に、SPDXファイル中の2つの要素間の関係に対する注意深い解析の後に決定された情報を提供する。

**7.2.3** 基数：任意、1

**7.2.4** データ フォーマット：直前に先行する関係についてのみ言及する自由形式文（複数行に渡ってもよい）

**7.2.5** Tag: `RelationshipComment:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

    A `RelationshipComment:` “Relationship:”直後の文でなければならない。

例：

    RelationshipComment: <text>パッケージ foo.tgz は実行形式barをビルドするための前提条件である。</text>

**7.2.6** RDF: Property `rdfs:comment` in class `spdx:Relationship`

例：

    <Relationship rdf:about="...">
      <rdfs:comment>
        パッケージ foo.tgz は実行形式barをビルドするための前提条件である。
      </rdfs:comment>
      ...
    </Relationship>