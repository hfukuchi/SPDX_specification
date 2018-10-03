# 6 Other Licensing Information Detected（検出された他ライセンス情報）

このセクションは、検出、宣言あるいは結論されたライセンスがSPDXライセンスリストに掲載されていない場合に使用する。リストの最新バージョンは以下を参照：http://spdx.org/licenses/. SPDXライセンスリスト[Appendix I](appendix-I-SPDX-license-list.md)でも参照できる。

パッケージで検出されたすべての個別ライセンスやライセンス情報への参照で、SPDXライセンスリストにないものに対しては、それぞれ個別のインスタンスを作成するべきである。各ライセンスインスタンスは、以下のフィールドを持つべきである。

フィールド：

## 6.1 License Identifier（ライセンス識別子） <a name="6.1"></a>

**6.1.1** 目的：SPDXライセンスリストに掲載されていないライセンスを参照する局所的な一意の識別子を提供する。この一意の識別子は、SPDXファイルのパッケージとファイルセクション（セクション[3](3-package-information.md) と [4](4-file-information.md)）で使用可能である。

**6.1.2** 意図：SPDXライセンスリストに掲載されていないライセンスのための、人間に可読な簡易形式識別子を作成する。この識別子はSPDXファイル内で一意であるべきである。SPDXの以前のバージョンでは、参照は連続する番号であることが要求されたが、バージョン1.2では、作成者は、人間が覚えやすく頭の中で位置づけしやすいように参照を指定することができる。

**6.1.3** 基数：条件付き（必須、1）　ライセンスがSPDXライセンスリストに掲載されていない場合

**6.1.4** データ フォーマット："LicenseRef-"`[idstring]`

ここで

`[idstring]` は、文字、数字、`.` かつ／または `-`を含む一意の文字列。

**6.1.5** Tag: `LicenseID:`

例：

    LicenseID: LicenseRef-1

    LicenseID: LicenseRef-Beerware-4.2

**6.1.6** RDF: Property `spdx:licenseID` in class `spdx:ExtractedLicensingInfo`

例：

    <ExtractedLicensingInfo rdf:about="licenseRef-1">
 <licenseId>LicenseRef-1</licenseId>
 </ExtractedLicensingInfo>

    <ExtractedLicensingInfo rdf:about="licenseRef-Beerware-4.2">
 <licenseId>LicenseRef-Beerware-4.2</licenseId>
 </ExtractedLicensingInfo>

# 6.2 Extracted Text（抽出されたテキスト） <a name="6.2"></a>

**6.2.1** 目的：パッケージから抽出されたライセンス参照の実際のテキストや、ライセンス識別子に関連するファイルを将来の解析のために提供する。

**6.2.2** 意図：パッケージで検出された実際のテキストや、SPDXライセンスリストに掲載されていないライセンスに関するファイルを提供する。

**6.2.3** 基数：条件付き（必須、1）　アサインされたライセンス識別子がある場合

**6.2.4** データ フォーマット：自由形式文（複数行に渡ってもよい）

**6.2.5** Tag: `ExtractedText:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例1（ライセンスに対する簡易参照だけがファイルにある場合）：

    ExtractedText: <text>This software is licensed under the Beer License.</text>

例2（ファイルにライセンス全文がある場合）

    ExtractedText: <text>"THE WHISKEY-WARE LICENSE": whiskeyfan@example.com wrote this file. As long as you retain this notice you can do whatever you want with this stuff. If we meet some day, and you think this stuff is worth it, you can buy me a bottle of whiskey in return </text>

**6.2.6** RDF: Property `spdx:extractedText` in class `spdx:ExtractedLicensingInfo`

例1（ライセンスに対する簡易参照だけがファイルにある場合）：

    <ExtractedLicensingInfo rdf:about="licenseRef-Whiskeyware">
 <licenseId>LicenseRef-Whiskeyware</licenseId>
 <extractedText>This software is licensed under the WHISKEY-WARE LICENSE.</extractedText>
 </ExtractedLicensingInfo>

例2（ファイルにライセンス全文がある場合）

    <ExtractedLicensingInfo rdf:about="licenseRef-Whiskeyware">
 <licenseId>LicenseRef-Whiskeyware</licenseId>
 <extractedText>""THE WHISKEY-WARE LICENSE": whiskeyfan@example.com wrote this file. As long as you retain this notice you can do whatever you want with this stuff. If we meet some day, and you think this stuff is worth it, you can buy me a bottle of whiskey in return.</extractedText>
 </ExtractedLicensingInfo>

# 6.3 License Name <a name="6.3"></a>

**6.3.1** Purpose: Provide a common name of the license that is not on the SPDX list.

Use `NOASSERTION` If there is no common name or it is not known.

**6.3.2** Intent: Provides a human readable name suitable for use as a title or label of the license when showing compact lists of licenses from the SPDX data to humans.

**6.3.3** Cardinality: Conditional (mandatory, one) if license is not on SPDX License List.

**6.3.4** Data Format: Single line of text | `NOASSERTION`.

**6.3.5** Tag: `LicenseName:`

例：

    LicenseName: Whiskey-Ware License

**6.3.6** RDF: Property `spdx:licenseName` in class `spdx:ExtractedLicensingInfo`

例：

    <ExtractedLicensingInfo rdf:about="licenseRef-Whiskey-Ware">
 <name>Whiskey-Ware License </name>
 </ExtractedLicensingInfo>


# 6.4 License Cross Reference <a name="6.4"></a>

**6.4.1** Purpose: Provide a pointer to the official source of a license that is not included in the SPDX License List, that is referenced by the License Identifier.

**6.4.2** Intent: Canonical source for a license currently not on the SPDX License List.

**6.4.3** Cardinality: Conditional (optional, one or more) if license is not on SPDX License List.

**6.4.4** Data Format: Uniform Resource Locator

**6.4.5** Tag: `LicenseCrossReference:`

例：

    LicenseCrossReference: http://people.freebsd.org/~phk/

**6.4.6** RDF: Property `rdfs:seeAlso` in class `spdx:ExtractedLicensingInfo`

例：

    <ExtractedLicensingInfo rdf:about="licenseRef-1">
 <rdfs:seeAlso>http://people.freebsd.org/~phk/</rdfs:seeAlso>
 </ExtractedLicensingInfo>

# 6.5 License Comment <a name="6.5"></a>

**6.5.1** Purpose: This field provides a place for the SPDX file creator to record any general comments about the license.

**6.5.2** Intent: Here, the intent is to provide the recipient of the SPDX file with more information determined after careful analysis of a license, or addition cross references.

**6.5.3** Cardinality: Optional, one.

**6.5.4** Data Format: Free form text that can span multiple lines

**6.5.5** Tag: `LicenseComment:`

`tag:value`フォーマットでは、これは `<text>...</text>`.で分離される。

例：

    LicenseComment: <text>The Whiskey-Ware License has a couple of other standard variants.</text>

**6.5.6** RDF: Property `rdfs:comment` in class `spdx:ExtractedLicensingInfo`

例：

    <ExtractedLicensingInfo rdf:about="licenseRef-1">
 <rdfs:comment> The Whiskey-Ware License has a couple of other standard variants.</rdfs:comment>
 </ExtractedLicensingInfo>