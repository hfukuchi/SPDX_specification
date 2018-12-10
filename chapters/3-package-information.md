# 3 Package Information（パッケージ情報）

記述されるパッケージごとに1つのパッケージ情報インスタンスが必要である。パッケージは、サブ パッケージを含むことができるが、このセクションの情報はリストされたパッケージのコンテンツ全体への参照について説明する。SPDX 2.0を使う場合には、ファイル セットを包含するパッケージは必ずしも必要ではない。

基数：任意、1以上

`tag:value` フォーマットでは、パッケージとファイルの置かれる順番は構文的に重要である。

新しいパッケージ情報セクションは、[パッケージ名](#3.1) フィールドで示される。
ファイルがある場合、すべてのパッケージ情報フィールドは、[ファイル セクション](4-file-information.md)開始前にすべてグループ化されなければならない。
パッケージに含まれるすべてのファイルは、適用可能なパッケージ情報に直接従わなければならない。
新しいパッケージ情報セクションは、（PackageNameを通じて）他のパッケージ開始を示す。
サブパッケージをパッケージ情報セクション中で入れ子にするべきではない。分離するべきである。明確にするためにRelationshipを使うべきである。to clarify.
パッケージのAnnotations（注釈）とRelationships（関係）は、パッケージ情報の後で、ファイル情報の前に置かれる。

フィールド：

## 3.1 Package Name（パッケージ名） <a name="3.1"></a>

**3.1.1** 目的：[Package Originator](#3.6)（パッケージ原作者）によって与えられたパッケージのフルネームを特定する。

**3.1.2** 意図：各パッケージの名前は、パッケージを保守するために使用される重要で慣習的な技術識別子である。

**3.1.3** 基数：必須、1

**3.1.4** データ フォーマット：1行の文

**3.1.5** Tag: `PackageName:`

    例：

    PackageName: glibc

**3.1.6** RDF: property `spdx:name` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <name>glibc</name>
    </Package>

## 3.2 Package SPDX Identifier（パッケージSPDX識別子） <a name="3.2"></a>

**3.2.1** 目的：他の要素から参照されるSPDX文書内の各要素を一意に特定する。これらは、内部から参照され、SPDX文書識別子と組み合わせて外部からも参照される。

**3.2.2** 意図：SPDX文書内に、同一パッケージの複数バージョンがありうる。各要素は、一意に参照できる必要があるので、要素間の関係は明確に示すことができる。

**3.2.3** 基数：必須、1

**3.2.4** データ フォーマット： "SPDXRef-"`[idstring]`

ここで `[idstring]` は一意の文字、数字、`.` かつ／または`-`を含む文字列。

**3.2.5** Tag: `SPDXID:`

    例：

    SPDXID: SPDXRef-1

**3.2.6** RDF: 要素のURIは、以下のフォームに従う：

    [SPDX DocumentNamespace]#[SPDX Identifier]

      SPDX Document Namespace（SPDX文書名前空間）の定義については[セクション 2.5](2-document-creation-information.md#2.5) を参照。SPDX Identifier（SPDX識別子）の定義については[セクション 2.3](2-document-creation-information.md#2.3)を参照。

    `xml:base`を利用した例：

      <rdf:RDF xml:base="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349A1B">
          ...
          <Package rdf:ID="SPDXRef-1">
              ...
          </Package>
      </rdf:RDF>

    URIを使用した例：

    <Package rdf:about="http://acme.com/spdxdocs/acmeproj/v1.2/1BE2A4FF-5F1A-48D3-8483-28A9B0349A1B">
        ...
    </Package>

## 3.3 Package Version（パッケージ バージョン） <a name="3.3"></a>

**3.3.1** 目的：パッケージのバージョンを特定する。

**3.3.2** 意図：パッケージへのバージョン付けは、パッケージの特定とパッケージ バージョンの後での変更を示すのに役立つ。

**3.3.3** 基数：任意、1

**3.3.4** データ フォーマット：1行の文

**3.3.5** Tag: `PackageVersion:`

    例：

    PackageVersion: 2.11.1

**3.3.6** RDF: property `spdx:versionInfo` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <versionInfo>2.11.1</versionInfo>
        ...
    </Package>

## 3.4 Package File Name（パッケージ ファイル名） <a name="3.4"></a>

**3.4.1** 目的：実際のファイル名やパッケージとして扱われるディレクトリのパスを提供する。適用可能な場合、これには、ファイル名の一部として使われるパッケージング手法や圧縮手法も含まれる。

**3.4.2** 意図：パッケージを含む圧縮ファイルの実ファイル名は、パッケージ識別情報と一緒に含まれる必要がある重要な技術要素である。サブディレクトリ内のファイルセットのようなグルーピングがパッケージとして扱われる場合には、サブディレクトリ名を提供するのが適切である。サブディレクトリ名は、`./`.に続く。構文については、[RFC 3986][rfc3986]を参照。

**3.4.3** 基数：任意、1

**3.4.4** データ フォーマット：1行の文

**3.4.5** Tag: `PackageFileName:`

    例：

    PackageFileName: glibc-2.11.1.tar.gz

    例（サブディレクトリをパッケージとして扱う）：

    PackageFileName: ./myrootdir/mysubdir1

**3.4.6** RDF: property `spdx:packageFileName` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <packageFileName>glibc 2.11.1.tar.gz</packageFileName>
        ...
    </Package>

    例（サブディレクトリをパッケージとして扱う）：

    <Package rdf:about="...">
        ...
        <packageFileName>./myrootdir/mysubdir1</packageFileName>
        ...
    </Package>

## 3.5 Package Supplier（パッケージ提供者） <a name="3.5"></a>

**3.5.1** 目的：SPDXファイルで特定されたパッケージ／ディレクトリの実際の頒布元を特定する。これは、パッケージ原作者と同じ場合も異なる場合もありうる。Package Supplier（パッケージ提供者）の名前は、ウェブサイトではなく、組織か認識されている著者でなければならない。たとえば、[SourceForge][] はウェブサイト ホストであり、提供者ではない。http://sourceforge.net/projects/bridge/の提供者は“[The Linux Foundation][LinuxFoundation]”である。

以下の場合には`NOASSERTION`を使用する。：

(i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

(ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

(iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.5.2** 意図：このフィールドは、パッケージ内コードの頒布点を理解するのを助ける。このフィールドは、ダウンストリーム パッケージ受領者がSPDXファイルの情報やパッケージの内容についての曖昧さや懸念を直接伝えるのを確実にする。

**3.5.3** 基数：任意、1

**3.5.4** データ フォーマット：以下のキーワードが後続する1行の文  | `NOASSERTION`

* `Person:` 人名および任意で `(<email>)`を付加
* `Organization:` 組織名および任意で`(<email>)`を付加

**3.5.5** Tag: `PackageSupplier:`

    例：

    PackageSupplier: Person: Jane Doe (jane.doe@example.com)

**3.5.6** RDF: property `spdx:supplier` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <supplier>Person: Jane Doe (jane.doe@example.com)</supplier>
        ...
    </Package>

## 3.6 Package Originator （パッケージ原作者）<a name="3.6"></a>

**3.6.1** 目的：SPDXファイルで特定されるパッケージがPackage Supplier（パッケージ供給者）（[セクション 3.5](#3.5) 参照）で記述されたのとは別の人や組織が原作者である場合、このフィールドはパッケージが最初に誰からあるいはどこから来たのかを特定する。ある場合には、パッケージ供給者とは別の第3者が、パッケージを作成し最初に頒布していることがある。たとえば、SPDXファイルは[glibc][] パッケージとそのパッケージ供給者[Red Hat][RedHat] を特定するが、パッケージ原作者は[Free Software Foundation][FSF] である。

以下の場合には`NOASSERTION`を使用する。：

(i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

(ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

(iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.6.2** 意図：このフィールドは、パッケージ中のオリジナル コードの頒布点を理解するのを助ける。このフィールドは、ダウンストリーム パッケージ受領者がSPDXファイルの情報やパッケージの内容についての曖昧さや懸念を直接伝えるのを確実にする。

**3.6.3** 基数：任意、1

**3.6.4** データ フォーマット：以下のキーワードが後続する1行の文  | `NOASSERTION`

* `Person:` 人名および任意で `(<email>)`を付加
* `Organization:` 組織名および任意で`(<email>)`を付加

**3.6.5** Tag: `PackageOriginator:`

    例：

    PackageOriginator: Organization: ExampleCodeInspect (contact@example.com)

**3.6.6** RDF: property `spdx:originator` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <originator>Organization: ExampleCodeInspect (contact@example.com)</originator>
    </Package>

## 3.7 Package Download Location （パッケージ ダウンロード位置）<a name="3.7"></a>

**3.7.1** 目的：このセクションは、SPDXファイル作成時にパッケージが置かれていたダウンロードUniversal Resource Locator (URL)またはバージョン コントロール システム（VCS）内の位置を特定する。

使用法：

* `NONE`　ダウンロード位置が一切ない場合
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

    (ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

    (iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.7.2** 意図：参照されているパッケージと全く同じものをどこからどのようにダウンロードするかは、検証と追跡のための重要なデータである。

**3.7.3** 基数：必須、1

**3.7.4** データフォーマット： uniform resource locator（URL）| VCS location | `NONE` | `NOASSERTION`

バージョン コントロールされたファイルに対するVCS位置構文はURLと似ている：

    <vcs_tool>+<transport>://<host_name>[/<path_to_repository>][@<revision_tag_or_branch>][#<sub_path>]

このVCS位置簡易表記（[pip][pip-vcs] 20150220時点 からヒントを受け採用している) は、[Git][], [Mercurial][], [Subversion][] および [Bazaar][]などのバージョン コントロール システム内の位置参照をサポートする。URL接頭子：`git+`, `hg+`, `bzr+`, `svn+` とSSHやHTTPのようなトランスポート スキーム を使ってVCSツール タイプを特定する。

サブパス、ブランチ名、コミット ハッシュ、リビジョン、タグ名を指定することが推奨される。コミットには`@` デリミター、サブパスには`#` デリミターを使ってサポートしている。

`<host_name>`にユーザー名やパスワードを使用することは、サポートされていないし、エラーと認識するべきである。URLやVCSリポジトリへのユーザー アクセス制御は、SPDX文書の外部で処理しなければならない。

VCS位置簡潔表記では、`<host_name>`, `<path_to_repository>` の中の最後のスラッシュは重要でない。`<sub_path>` の中の最初と最後のスラッシュは重要でない。

**3.7.5** Tag: `PackageDownloadLocation:`

    あいまいなときの例：

    PackageDownloadLocation: NOASSERTION

    PackageDownloadLocation: NONE

    URLの例：

    PackageDownloadLocation: http://ftp.gnu.org/gnu/glibc/glibc-ports-2.15.tar.gz

    [Git][]の例：

SPDXがサポートするスキーム：SPDX supported schemes are: `git`, `git+git`, `git+https`, `git+http`, and `git+ssh`. `git` と `git+git` は同じである。

サポートする形式は以下である：

    PackageDownloadLocation: git://git.myproject.org/MyProject

    PackageDownloadLocation: git+https://git.myproject.org/MyProject.git

    PackageDownloadLocation: git+http://git.myproject.org/MyProject

    PackageDownloadLocation: git+ssh://git.myproject.org/MyProject.git

    PackageDownloadLocation: git+git://git.myproject.org/MyProject

    PackageDownloadLocation: git+git@git.myproject.org:MyProject

リポジトリ内のファイルやディレクトリへのサブパスを指定するために、`#`デリミターを使用する：

    PackageDownloadLocation: git://git.myproject.org/MyProject#src/somefile.c

    PackageDownloadLocation: git+https://git.myproject.org/MyProject#src/Class.java

ブランチ名、コミット ハッシュおよびタグ名を指定するために、`@`デリミターを使用する：

    PackageDownloadLocation: git://git.myproject.org/MyProject.git@master

    PackageDownloadLocation: git+https://git.myproject.org/MyProject.git@v1.0

    PackageDownloadLocation: git://git.myproject.org/MyProject.git@da39a3ee5e6b4b0d3255bfef95601890afd80709

サブパス、ブランチ名、コミット ハッシュは結合できる：

    PackageDownloadLocation: git+https://git.myproject.org/MyProject.git@master#/src/MyClass.cpp

    PackageDownloadLocation: git+https://git.myproject.org/MyProject@da39a3ee5e6b4b0d3255bfef95601890afd80709#lib/variable.rb

    [Mercurial][]の例:

SPDXがサポートするスキーム：`hg+http`, `hg+https`, `hg+static-http`, and `hg+ssh`

サポートしている形式：

    PackageDownloadLocation: hg+http://hg.myproject.org/MyProject

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject

    PackageDownloadLocation: hg+ssh://hg.myproject.org/MyProject

リポジトリ内のファイルやディレクトリへのサブパスを指定するために、`#`デリミターを使用する：

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject#src/somefile.c

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject#src/Class.java

ブランチ名、コミット ハッシュ、タグ名を渡すために、`@`デリミターを使用する：

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@da39a3ee5e6b

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@2019

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@v1.0

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@special_feature

サブパス、ブランチ名、コミット ハッシュは結合できる：

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@master#/src/MyClass.cpp

    PackageDownloadLocation: hg+https://hg.myproject.org/MyProject@da39a3ee5e6b#lib/variable.rb

[Subversion][]の例：

SPDXがサポートするスキーム：`svn`, `svn+svn`, `svn+http`, `svn+https`, `svn+ssh`. `svn` と `svn+svn` は同じである。

サポートしている形式：

    PackageDownloadLocation: svn://svn.myproject.org/svn/MyProject

    PackageDownloadLocation: svn+svn://svn.myproject.org/svn/MyProject

    PackageDownloadLocation: svn+http://svn.myproject.org/svn/MyProject/trunk

    PackageDownloadLocation: svn+https://svn.myproject.org/svn/MyProject/trunk

リポジトリ内のファイルやディレクトリへのサブパスを指定するために、`#`デリミターを使用する：

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject#src/somefile.c

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject#src/Class.java

URLパスはサブパスを含むことができるので、このサポートはSVNにとってはそれほど重要でない。この二つの形式は同じである：

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject/trunk#src/somefile.c

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject/trunk/src/somefile.c

`@` デリミターを使ってリビジョンを指定できる：

    PackageDownloadLocation: svn+https://svn.myproject.org/svn/MyProject/trunk@2019

サブパスとリビジョンは結合できる：

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject@123#/src/MyClass.cpp

    PackageDownloadLocation: svn+https://svn.myproject.org/MyProject/trunk@1234#lib/variable/variable.rb

[Bazaar][]の例：

SPDXがサポートするスキーム：`bzr+http`, `bzr+https`, `bzr+ssh`, `bzr+sftp`, `bzr+ftp`, and `bzr+lp`.

サポートしている形式：

    PackageDownloadLocation: bzr+https://bzr.myproject.org/MyProject/trunk

    PackageDownloadLocation: bzr+http://bzr.myproject.org/MyProject/trunk

    PackageDownloadLocation: bzr+sftp://myproject.org/MyProject/trunk

    PackageDownloadLocation: bzr+ssh://myproject.org/MyProject/trunk

    PackageDownloadLocation: bzr+ftp://myproject.org/MyProject/trunk

    PackageDownloadLocation: bzr+lp:MyProject

リポジトリ内のファイルやディレクトリへのサブパスを指定するために、`#`デリミターを使用する：

    PackageDownloadLocation: bzr+https://bzr.myproject.org/MyProject/trunk#src/somefile.c

    PackageDownloadLocation: bzr+https://bzr.myproject.org/MyProject/trunk#src/Class.java

`@` デリミターを使ってリビジョンやタグを指定できる：

    PackageDownloadLocation: bzr+https://bzr.myproject.org/MyProject/trunk@2019

    PackageDownloadLocation: bzr+http://bzr.myproject.org/MyProject/trunk@v1.0

サブパスとリビジョンは結合できる：

    PackageDownloadLocation: bzr+https://bzr.myproject.org/MyProject/trunk@2019#src/somefile.c

**3.7.6** RDF: property `spdx:downloadLocation` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <downloadLocation>http://ftp.gnu.org/gnu/glibc/glibc-ports-2.15.tar.gz</downloadLocation>
    </Package>

    <Package rdf:about="...">
        <downloadLocation>
            git+https://git.myproject.org/MyProject.git@v10.0#src/lib.c
        </downloadLocation>
    </Package>

    <Package rdf:about="...">
        <downloadLocation rdf:resource="http://spdx.org/rdf/terms#noassertion"/>
    </Package>

    <Package rdf:about="...">
        <downloadLocation rdf:resource="http://spdx.org/rdf/terms#none"/>
    </Package>

## 3.8 Files Analyzed（解析したファイル） <a name="3.8"></a>

**3.8.1** 目的：このパッケージのファイルが入手可能であるか、またはSPDX文書作成時に解析対象になっていたかを示す。`false`の場合、パッケージは、メタデータや、プロジェクト、製品、生成物、頒布またはコンポーネントを参照するURIを示す。`false`にセットされた場合には、パッケージは一切ファイルを含んではいけない。

**3.8.2** 意図：パッケージは、SPDX文書の外部にあるプロジェクト、製品、作成物、頒布あるいはコンポーネントを参照できる。

    いくつかの例：

    外部製品のバンドル：パッケージAは、パッケージとその依存物に関するメタデータであってもよい。それは製品やプロジェクトに換券するパッケージへの参照をゆるく集めたリストでもよい。ビルドや実行することで、副次的にもっと多くのパッケージや依存物を見つけるかもしれない。参照されたパッケージは、それ自体でSPDX文書を持つことができる。このケースでは、パッケージAのFile Analyzed属性は`false`となる。パッケージAは、可能なすべての関係の中で参照されたパッケージを含むSPDX文書へのExternal Document References（外部文書参照）を含む。Relationships（関係）セクションは、SPDX文書や含まれるSPDX要素をパッケージAのスコープ内の依存関係ごとに適切な構文で関係づける。
    外部製品へのパッケージ関係：Package Aは、Package Bとの間でSTATIC_LINK関係を持つことができるが、Package Bのバイナリー表現は、ビルド プロセスによって与えられるので、Package Aのファイル リストには含まれない。このケースでは、Package BのFilesAnalyzed属性はfalse、他のすべての属性は後で定義される制限にしなければならない。Package AとPackage Bの関係は、[セクション 7](7-relationships-between-SPDX-elements.md).で説明する方法で記述できる。
    外部製品から派生したファイル：Package Aは、外部製品から派生した複数のファイルを含む。これらのファイルとプロジェクトの関係を記述するのに`artifactOf*`属性（セクション4.9­4.11）を使うより、外部プロジェクトは他のパッケージPackage Bで表現する。Package Bの[`FilesAnalyzed`](#3.8) 属性は`false`にする。バイナリーファイルは、Package Bと関係を持つ。（セクション6）これは、外部プロジェクトを1つのSPDX識別子（Package Bの識別子）で表現することを可能にする。それは、また、外部プロジェクトと各ファイルの関係を詳細に表現することを可能にする。

**3.8.3** 基数：任意、1（省略した場合、デフォルト値`true`が想定される）

**3.8.4** データ フォーマット：Boolean

**3.8.5** Tag: `FilesAnalyzed`

    例：

    FilesAnalyzed: false

**3.8.6** RDF: property `spdx:filesAnalyzed` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <filesAnalyzed>false</filesAnalyzed>
        ...
    </Package>

## 3.9 Package Verification Code （パッケージ検証コード）<a name="3.9"></a>

**3.9.1** 目的：このフィールドは、各パッケージを構成し、このSPDXファイル中のデータと関連する実際のファイル（SPDXファイルがパッケージに含まれている場合には、SPDXファイルは除く）を基にしたパッケージの特定コンテンツを指定する独立再現メカニズムを提供する。この識別子は、オリジナルパッケージに含まれていたファイルが変更されたことを受領者によって確認できるようにするとともに、パッケージの一部としてSPDXファイルを挿入することを可能にする。

**3.9.2** 意図：各パッケージに含まれるファイルに基づいた一意の識別子を提供する。これは、SPDXファイルが参照する特定のパッケージのバージョンや変更間の混乱を減らす。これは、識別子を変更することなく、パッケージにSPDXファイルを挿入することが可能になる。

**3.9.3** 基数：必須、1　[`FilesAnalyzed`](#3.8)  が`true` か省略された場合、　0（省略しなければならない）  `FilesAnalyzed` が `false`の場合

**3.9.4** アルゴリズム：

    verificationcode = 0
    filelist = templist = “”
    for all files in the package {
      if file is an “excludes” file, skip it /* exclude SPDX analysis file(s) */
            append templist with “SHA1(file)/n”
    }
    sort templist in ascending order by SHA1 value
    filelist = templist with "/n"s removed. /* ordered sequence of SHA1 values with no separators */
    verificationcode = SHA1(filelist)

    Where SHA1(file) applies a SHA1 algorithm on the contents of file and returns the result in lowercase hexadecimal digits.

    Required sort order: '0','1','2','3','4','5','6','7','8','9','a','b','c','d','e','f' (ASCII order)

**3.9.5** データ フォーマット：小文字16進数40桁で表現された160ビットバイナリの1行文。

**3.9.6** Tag: `PackageVerificationCode:` (and optionally `(excludes: FileName)`)

`FileName` is specified in [section 4.1](4-file-information.md#4.1).

    例：

    PackageVerificationCode: d6a770ba38583ed4bb4525bd96e50461655d2758 (excludes: ./package.spdx)

**3.9.7** RDF: `spdx:packageVerificationCodeValue`, `spdx:packageVerificationCodeExcludedFile` in class `spdx:PackageVerificationCode` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <packageVerificationCode>
            <PackageVerificationCode>
                <packageVerificationCodeValue>
                    d6a770ba38583ed4bb4525bd96e50461655d2758
                </packageVerificationCodeValue>
                <packageVerificationCodeExcludedFile>
                    ./package.spdx
                </packageVerificationCodeExcludedFile>
            </PackageVerificationCode>
        </packageVerificationCode>
   </Package>

## 3.10 Package Checksum（パッケージ チェックサム） <a name="3.10"></a>

**3.10.1** 目的：このフィールドは、このSPDXファイル中のデータと関連するパッケージを一意に特定できる独立再現メカニズムを提供する。この識別子は、オリジナル パッケージに含まれるファイルが変更されたかどうかを受領者によって確認できるようにする。SPDXファイルがパッケージに含まれる場合には、この値は計算されるべきではない。[SHA-1][] アルゴリズムが、チェックサム計算にデフォルトで使用される。 

**3.10.2** 意図：パッケージの一意の識別子を提供することで、SPDXファイルが参照する特定のパッケージのバージョンや変更間の混乱が軽減されるはずである。

**3.10.3** 基数：任意、1以上

**3.10.4** 使用可能なアルゴリズム：[`SHA1`][SHA-1], [`SHA256`][SHA-256], [`MD5`][MD5]

**3.10.5** データフォーマット：3つの要素からなる。アルゴリズム識別子（`SHA1`）、コロン `:`、小文字16進数で表現されたビット値（アルゴリズムの出力）。

**3.10.6** Tag: `PackageChecksum:`

    例：

    PackageChecksum: SHA1: 85ed0817af83a24ad8da68c2b5094de69833983c

    PackageChecksum: SHA256: 11b6d3ee554eedf79299905a98f9b9a04e498210b59f15094c916c91d150efcd

    PackageChecksum: MD5: 624c1abb3664f4b35547e7c73864ad24

**3.10.7** RDF: properties `spdx:algorithm`, `spdx:checksumValue` in class `spdx:checksum` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <checksum>
            <Checksum>
                <algorithm rdf:resource="http://spdx.org/rdf/terms#checksumAlgorithm_sha1"/>
                <checksumValue>85ed0817af83a24ad8da68c2b5094de69833983c</checksumValue>
            </Checksum>
        </checksum>
        <checksum>
            <Checksum>
                <algorithm rdf:resource="http://spdx.org/rdf/terms#checksumAlgorithm_sha256"/>
                <checksumValue>
                    11b6d3ee554eedf79299905a98f9b9a04e498210b59f15094c916c91d150efcd
                </checksumValue>
            </Checksum>
        </checksum>
        <checksum>
            <Checksum>
                <algorithm rdf:resource="http://spdx.org/rdf/terms#checksumAlgorithm_md5"/>
                <checksumValue>624c1abb3664f4b35547e7c73864ad24</checksumValue>
            </Checksum>
        </checksum>
    </Package>

## 3.11 Package Home Page（パッケージ ホーム ページ） <a name="3.11"></a>

**3.11.1** 目的：このフィールドは、SPDXファイル作成者にパッケージのホームページ用のウェブサイトを記録する場所を提供する。このリンクは、SPDXファイル作成者によって参照されたパッケージに対する情報にも使える。

使用法：

* `NONE` パッケージ ホームページが無い場合：
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

    (ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

    (iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.11.2** これによって、追加情報を探しているSPDXファイル受領者は、探す手間とパッケージと関連するプロジェクト ホームページ間の整合性を確認する手間を省略できる。

**3.11.3** 基数：任意、1

**3.11.4** データフォーマット： uniform resource locator（URL） | `NONE` | `NOASSERTION`

**3.11.5** Tag: `PackageHomePage:`

    例：

    PackageHomePage: http://ftp.gnu.org/gnu/glibc

**3.11.6** RDF: property `doap:homepage` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        <doap:homepage >http://ftp.gnu.org/gnu/glibc/</doap:homepage></Package>

## 3.12 Source Information（ソース情報） <a name="3.12"></a>

**3.12.1** 目的：SPDXファイル作成者に関連する背景情報やオリジナル パッケージに関する追加コメントを記録する場所を提供する。たとえば、このフィールドには、パッケージがソースコード管理システムから引き出されたとか、再パッケージされたというコメントを記載してもよい。

**3.12.2** 意図：SPDXファイル作成者は、変則的な事項やオリジナル パッケージを確定での発見などの追加コメントを提供できる。

**3.12.3** 基数：任意、1

**3.12.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

`tag:value` フォーマットでは、これは`<text>...</text>`で分離される。

**3.12.5** Tag: `PackageSourceInfo:`

    例：

    PackageSourceInfo: <text>uses glibc-2_11-branch from git://sourceware.org/git/glibc.git.</text>

**3.12.6** RDF: `spdx:sourceInfo`

    例：

    <Package rdf:about="...">
        ...
        <sourceInfo>uses glibc-2_11-branch from git://sourceware.org/git/glibc.git.</sourceInfo>
        ...
    </Package>

## 3.13 Concluded License （結論されたライセンス）<a name="3.13"></a>

**3.13.1** 目的：SPDXファイル作成者がパッケージに適用されると結論したライセンスを与える。ライセンスを決定できない場合には代替値を与える。

このフィールドへの記入は以下に限られる：

* [Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なSPDXライセンス表現：
* `NONE`　SPDXファイル作成者が、このパッケージに適用できるライセンスが無いと結論した場合；
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、特定を試みたが、対象を合理的に決定できなかった；

    (ii) SPDXファイル作成者が、このフィールドを決定しようと試みなかった；

    (iii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

もし、Concluded License（結論されたライセンス）が[Declared License（宣言されたライセンス）](#3.15)と異なる場合、Comments on License（ライセンスへのコメント、[(セクション 3.16)](#3.16).）フィールドに説明を記載すべきである。`NOASSERTION`に関しては、Comments on License（ライセンスへのコメント、[(セクション 3.16)](#3.16) ）フィールドに説明を記載した方が良い。

**3.13.2** 意図：SPDXファイル作成者がパッケージ内のライセンス情報や他の客観的情報（たとえばCOPYINGファイル）とスキャンツール結果とを合わせて解析を行い、パッケージに適用されるライセンスは何かについて合理的に客観性のある結論に到達すること。

**3.13.3** 基数：必須、1

**3.13.4** データフォーマット： `<SPDX License Expression>` | `NONE` | `NOASSERTION`

ここで

`<SPDX License Expression>` は、[Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なPDXライセンス表現。

**3.13.5** Tag: `PackageLicenseConcluded:`

    例：

    PackageLicenseConcluded: LGPL-2.0

    例：

    PackageLicenseConcluded: (LGPL-2.0 OR LicenseRef-3)

**3.13.6** RDF: property `spdx:licenseConcluded` in `class spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <licenseConcluded rdf:resource="http://spdx.org/licenses/LGPL-2.0" />
        ...
    </Package>

    例：

    <Package rdf:about="...">
        ...
        <licenseConcluded>
            <DisjunctiveLicenseSet>
                <member rdf:resource="http://spdx.org/licenses/LGPL-2.0" />
                <member rdf:resource="LicenseRef-3" />
            </DisjunctiveLicenseSet>
        </licenseConcluded>
        ...
    </Package>

## 3.14 All Licenses Information from Files （ファイルからの全ライセンス情報）<a name="3.14"></a>

**3.14.1** 目的：このフィールドはパッケージ内で発見された全ライセンスのリストを含む。ライセンス間の関係（結合、分離）はこのフィールドでは特定されない？それは、単に、見つかったすべてのライセンスをリストしたものである。

このフィールドへの記入は以下に限られる：

* 検出されたライセンスがSPDXライセンス リストにある場合には、SPDXライセンス リスト簡易形式識別子；
* ライセンスがSPDXライセンス リストにない場合には、LicenseRef-[idstring] で示すユーザー定義参照；
* `NONE` どのファイルからもライセンスが検出されない場合；
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、このフィールドを決定しようと試みなかった。；

    (ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.14.2** 意図：実際のファイルかで検出される全ライセンス情報を把握すること。

**3.14.3** **3.9.3** 基数：必須、1以上　[`FilesAnalyzed`](#3.8)  が`true` か省略された場合、　0（省略しなければならない）  `FilesAnalyzed` が `false`の場合

**3.14.4** データ フォーマット： [`<shortIdentifier>`](appendix-I-SPDX-license-list.md#I.1) |
 ["DocumentRef-"`[idstring]`:]"LicenseRef-"`[idstring]` |
 `NONE` | `NOASSERTION`

ここで

* "DocumentRef-"`[idstring]` は、[セクション 2.6](2-document-creation-information.md#2.6)で記述される外部SPDX文書への任意の参照
* `[idstring]` は、文字、数字、`.`, or `-`を含む一意の文字列。

**3.14.5** Tag: `PackageLicenseInfoFromFiles:`

    例：

    PackageLicenseInfoFromFiles: GPL-2.0

    PackageLicenseInfoFromFiles: LicenseRef-1

    PackageLicenseInfoFromFiles: LicenseRef-2

**3.14.6** RDF: property `spdx:licenseInfoFromFiles` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <licenseInfoFromFiles rdf:resource="https://spdx.org/licenses/GPL-2.0" />
        <licenseInfoFromFiles rdf:resource="#LicenseRef-1" />
        <licenseInfoFromFiles rdf:resource="#LicenseRef-2" />
        ...
    </Package>

## 3.15 Declared License（宣言されたライセンス） <a name="3.15"></a>

**3.15.1** 目的：パッケージの作者によって宣言されたライセンスがリストされる。サードパーティ リポジトリから受け取ったライセンス情報など、パッケージ作者によって作成されていないライセンス情報は、このフィールドに記載すべきではない。

このフィールドへの記入は以下に限られる：

* [Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なSPDXライセンス表現：
* `NONE` パッケージがライセンス情報を何も含まない場合；
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、このフィールドを決定しようと試みなかった。；

    (ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.15.2** 意図：これは、ソースコード パッケージに含まれる1つ以上のファイル（たとえば、COPYINGファイル）にテキストで記載されたライセンスである。このフィールドは、パッケージ ウェブサイトのような外部ソースからライセンス情報を取り込むことを意図していない。そういう情報は、Concluded License（結論されたライセンス、 [(section 3.13)](#3.13)）に記載することができる。パッケージ レベルでマルチ ライセンスが宣言されている場合は、このフィールドは、複数のDeclared Licenses（宣言されたライセンス）を含むことができる。

**3.15.3** 基数：必須、1

**3.15.4** データフォーマット： `<SPDX License Expression>` | `NONE` | `NOASSERTION`

ここで

* `<SPDX License Expression>` は、[Appendix IV](appendix-IV-SPDX-license-expressions.md)で定義された有効なPDXライセンス表現。

**3.15.5** Tag: `PackageLicenseDeclared:`

    例：

    PackageLicenseDeclared: LGPL-2.0

    例：

    PackageLicenseDeclared: (LGPL-2.0 AND LicenseRef-3)

**3.15.6** RDF: property `spdx:licenseDeclared` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <licenseDeclared rdf:resource="http://spdx.org/licenses/LGPL-2.0" />
        ...
    </Package>


    例：

    <Package rdf:about="...">
        ...
        <licenseDeclared>
            <ConjunctiveLicenseSet>
                <member rdf:resource="http://spdx.org/licenses/LGPL-2.0" />
                <member rdf:resource="#LicenseRef-3" />
            </ConjunctiveLicenseSet>
        </licenseDeclared>
        ...
    </Package>

## 3.16 Comments on License ライセンスへのコメント）<a name="3.16"></a>

**3.16.1** 目的：このフィールドは、SPDXファイル作成者が関連する背景情報やパッケージに対する結論されたライセンスに至った解析について記録する場所を提供する。もし、Concluded License（結論されたライセンス）がDeclared License（宣言されたライセンス）と異なる場合、Comments on License（ライセンスへのコメント）フィールドに説明を記載すべきである。Concluded License（結論されたライセンス）が `NOASSERTION`の場合にも、説明を記載することが望まれる。

**3.16.2** 意図：SPDXファイルの受領者に、Concluded License（結論されたライセンス）がファイルやソースコード パッケージからのライセンス情報と一致しない場合や`NOASSERTION`が設定されている場合に、Concluded License（結論されたライセンス）はどのように決定されたかの詳細説明、または、パッケージのライセンスを決定するのに有用な情報を提供する。

**3.16.3** 基数：任意、1

**3.16.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

`tag:value` フォーマットでは、これは`<text>...</text>`で分離される。

RDFでは、`<licenseComment>`で分離される。

**3.16.5** Tag: `PackageLicenseComments:`

    例：

    PackageLicenseComments: <text>The license for this project changed with the release of version 1.4.
      The version of the project included here post-dates the license change.</text>

**3.16.6** RDF: property `spdx:licenseComments` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <licenseComments>
            このパッケージは、ソースとバイナリー形式で出荷された。
            バイナリーは、gcc 4.5.1 で生成され、互換性のあるランタイム ライブラリー システムとリンクすることが期待される。
        </licenseComments>
        ...
    </Package>

## 3.17 Copyright Text （著作権テキスト）<a name="3.17"></a>

**3.17.1** 目的：パッケージの著作権保有者と日付を特定する。これは、パッケージ情報ファイルから取り出した自由形式のテキスト フィールドである。このフィールドへの記入は以下に限られる：

* 不完全なものも含めて、著作権表記に関連するすべてのテキスト
* `NONE` パッケージが著作権情報を何も含まない場合；
* `NOASSERTION` 以下の場合：

    (i) SPDXファイル作成者が、このフィールドを決定しようと試みなかった。；

    (ii) SPDXファイル作成者が、意図的に情報を提供しなかった（特に意味がないことを、そうすることで暗示するべきである）。

**3.17.2** 意図：パッケージのすべての著作権表記を記録する。

**3.17.3** 基数：必須、1

**3.17.4** データ フォーマット：自由形式文（複数行に渡ってもよい） | `NONE` | `NOASSERTION`

**3.17.5** Tag: `PackageCopyrightText:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

    例：

    PackageCopyrightText: <text>Copyright 2008-2010 John Smith</text>

**3.17.6** RDF: property `spdx:copyrightText` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <copyrightText>Copyright 2008-2010 John Smith</copyrightText>
        ...
    </Package>

## 3.18 Package Summary Description（パッケージ要約記述） <a name="3.18"></a>

**3.18.1** 目的：このフィールドはパッケージの簡単な記述である。

**3.18.2** 意図：SPDXファイル作成者が、実際のパッケージのソースコードをパースしなくてもパッケージの機能や用途がわかる簡潔な情報を提供できること。

**3.18.3** 基数：任意、1

**3.18.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**3.18.5** Tag: `PackageSummary:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

    例：

    PackageSummary: <text>GNU C library.</text>

**3.18.6** RDF: property `spdx:summary` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <summary>GNU C library.</summary>
        ...
    </Package>

## 3.19 Package Detailed Description（パッケージ要約記述） <a name="3.19"></a>

**3.19.1** 目的：このフィールドはパッケージのより詳細な記述である。これはパッケージ自体から取り出されたものである。

**3.19.2** 意図：SPDXファイル受領者に、パッケージの機能、予期される用途や実装についての詳細な技術説明を提供する。このフィールドは前バージョンのパッケージからの改善についての記述も含む。

**3.19.3** 基数：任意、1

**3.19.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**3.19.5** Tag: `PackageDescription:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

    例：

    PackageDescription: <text>The GNU C Library defines functions that are specified by the ISO C standard,
    as well as additional features specific to POSIX and other derivatives of the Unix operating system,
    and extensions specific to GNU systems.</text>

3.19.6  RDF:  property `spdx:description` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <description>
            The GNU C Library defines functions that are specified by the
            ISO C standard, as well as additional features specific to POSIX and other
            derivatives of the Unix operating system, and extensions specific to GNU systems.
        </description>
        ...
    </Package>

## 3.20 Package Comment（パッケージ コメント） <a name="3.20"></a>

**3.20.1** 目的：このフィールドは、SPDXファイル作成者に、対象パッケージの一般的なコメントを記録する場所を提供する。

**3.20.2** 意図：SPDX文書の受領者に注意深いパッケージ解析の後に決定された情報を提供する。

**3.20.3** 基数：任意、1

**3.20.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**3.20.5** Tag: `PackageComment:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

    例：

    PackageComment: <text>The package includes several sub-packages; see Relationship information.</text>

**3.20.6** RDF: property `rdfs:comment` in class `spdx:Package`

    例：

    <Package rdf:about="...">
        ...
        <rdfs:comment>
            The package includes several sub-packages; see Relationship information.
        </rdfs:comment>
        ...
    </Package>

## 3.21 External Reference（外部参照） <a name="3.21"></a>

**3.21.1** 目的： External Reference（外部参照）は、パッケージが追加情報、メタデータ、要素列挙（Enumeration）、あるいは、パッケージに関連すると考えられるダウンロード可能なコンテンツについての外部ソースへ参照できるようにする。

**3.21.2** 意図：情報、メタデータ、要素列挙（Enumeration）、あるいは、パッケージと既知の脆弱性を関連させる構造的な命名スキームのようなパッケージに関連すると考えられるコンテンツに関する外部ソースを提示する。

**3.21.3** 基数：任意、1以上

**3.21.4** データフォーマット：`<category> <type> <locator>`

ここで

* `<category>` is `SECURITY` | `PACKAGE-MANAGER` | `OTHER`
* `<type>` は、[Appendix VI](appendix-VI-external-repository-identifiers.md)にリストされたタイプ。

`<locator>`  は、パッケージ特有の情報、メタデータ、目的の場所にあるコンテンツにアクセスするためのスペースを含まない一意の文字列。locator の形式は`<type>`によって定義される制限である。

**3.21.5** Tag: `ExternalRef:`

    例：

    ExternalRef: SECURITY cpe23Type cpe:2.3:a:pivotal_software:spring_framework:4.1.0:*:*:*:*:*:*:*

    ExternalRef: OTHER LocationRef-acmeforge acmecorp/acmenator/4.1.3-alpha

**3.21.6** RDF: property `target` in class `spdx:ExternalRef` in class `spdx:Package`

    例（リストされた位置）：

    <spdx:Packagerdf:about="...">
        ...
        <spdx:externalRef>
            <spdx:ExternalRef>
                <spdx:referenceCategory rdf:resouce="http://spdx.org/rdf/terms#referenceCategory_packageManager" />
                <spdx:referenceType rdf:resource="http://spdx.org/rdf/refeferences/maven-central" />
                <spdx:referenceLocator>org.apache.commons:commons-lang:3.2.1</spdx:referenceLocator>
            </spdx:ExternalRef>
        </spdx:externalRef>
        ...
    </spdx:package>

    例（リストされない位置）：

    <spdx:Package rdf:about="...">
        ...
        <spdx:externalRef>
            <spdx:ExternalRef>
                <spdx:referenceCategory rdf:resource="http://spdx.org/rdf/terms#referenceCategory_other" />
                <spdx:referenceType rdf:resource="http://spdx.org/spdxdocs/spdx-tools-v1.2-3F2504E0-4F89-41D3-9A0C-0305E82...LocationRef-acmeforge" />
                <spdx:referenceLocator>acmecorp/acmenator/4.1.3-alpha</spdx:referenceLocator>
            </spdx:ExternalRef>
        </spdx:externalRef>
        ...
    </spdx:package>

リストされない位置のreferenceType値は、SPDX文書名前空間（[セクション 2.5](2-document-creation-information.md#2.5)）と後続の  `#`  と[3.21.4](#3.21).で定義されるカテゴリーから構成される。

## 3.22 External Reference Comment（外部参照コメント） <a name="3.22"></a>

**3.22.1** 目的：参照の目的と対象についての人間が可読な情報を提供する。

**3.22.2** 意図：人間の受領者に、参照が存在する理由、どういう情報、コンテンツ、メタデータが抽出可能であるかを知らせる。パッケージ内のファイルのartifactOf値と対象との関係は、ここで説明される必要がある。参照がBINARY（バイナリー）の場合は、参照とPackageDownloadLocationとの関係が説明される必要がある。参照がSOURCE（ソース）の場合は、参照とPackageDownloadLocationとSourceInformationとの関係が説明される必要がある。

**3.22.3** 基数：各[External Reference（外部参照）][#3.21).に対して条件付き（任意、1）

**3.22.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

`tag:value` フォーマットでは`<text>...</text>`で分離され、[External Reference（外部参照）](#3.21) に後続することが期待されるので、連想できる。

RDFでは、`<ExternalRefComment>`で分離される。

**3.22.5** Tag: `ExternalRefComment:`

    例：

    ExternalRefComment: <text>NIST National Vulnerability Database (NVD) describes
    security vulnerabilities (CVEs) which affect Vendor Product Version
    acmecorp:acmenator:6.6.6.</text>

**3.22.6** RDF: Property `rdfs:comment` in class `spdx:ExternalRef` in class `spdx:Package`

    <spdx:Package rdf:about="...">
        ...
        <spdx:externalRef>
            <spdx:ExternalRef>
                <spdx:referenceCategory rdf:resouce="http://spdx.org/rdf/terms#referenceCategory_packageManager" />
                <spdx:referenceType rdf:resource="http://spdx.org/rdf/refeferences/maven-central" />
                <spdx:referenceLocator>org.apache.commons:commons-lang:3.2.1</spdx:referenceLocator>
                <rdfs:comment>
                    NIST National Vulnerability Database (NVD) describes
                    security vulnerabilities (CVEs) which affect Vendor Product Version
                    acmecorp:acmenator:6.6.6
                </rdfs:comment>
            </spdx:ExternalRef>
        </spdx:externalRef>
        ...
    </spdx:package>


[Bazaar]: http://bazaar.canonical.com/
[FSF]: http://www.fsf.org/
[Git]: https://git-scm.com/
[glibc]: https://www.gnu.org/software/libc/
[LinuxFoundation]: https://www.linuxfoundation.org/
[MD5]: https://tools.ietf.org/html/rfc1321
[Mercurial]: https://www.mercurial-scm.org/
[pip-vcs]: https://pip.pypa.io/en/latest/reference/pip_install.html#vcs-support
[Red Hat]: https://www.redhat.com/
[rfc3986]: https://tools.ietf.org/html/rfc3986
[SHA-1]: https://tools.ietf.org/html/rfc3174
[SHA-256]: https://tools.ietf.org/html/rfc6234
[SourceForge]: https://sourceforge.net/
[Subversion]: https://subversion.apache.org/
