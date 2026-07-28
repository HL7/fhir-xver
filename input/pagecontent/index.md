The Cross-Version Extensions for FHIR (XVer) project provides a set of packages that define extensions, profiles, and value sets for cross-version compatibility in FHIR. These packages are designed to support the validation and interoperability of FHIR resources across different versions.

### About This Guide

Cross-version extension content is generated via a combination of automatic differential detection and manual editing.

For details or questions, please reach out on [Zulip](https://chat.fhir.org/#narrow/channel/426854-FHIR-cross-version-issues) or
to the FHIR Infrastructure WorkGroup.

Frequently Asked Questions and related guidance can be found on [FAQs Page](faqs.html)

### Goals

* Ability to use elements from another version of FHIR
* Encode information **added** in a *newer* version of FHIR
    * Community identified additional data that is needed
    * Need to provide a consistent way of representing it in an earlier version of FHIR
* Encode information **removed** in a *newer* version of FHIR
    * Community decided data was no longer necessary
    * Need to provide a consistent way of representing it in a later version of FHIR
    * Version migration requires interoperability between versions and cannot break old expectations
    * Scenarios where data needs to round-trip conversion between different versions

### Cross Version Packages

There are two types of cross-version packages that are generated from the specifications:
* the packages specific to a FHIR version pair that contain definitions, and
* convenience packages for validators.

The main cross-version packages are built against two FHIR versions, a *source* version and a *target* version. For example, in
order to use elements from FHIR R5 as extensions in FHIR R4, the *source* version is FHIR R5 and the *target* version is FHIR
R4. The package names are based on the pairs: `hl7.fhir.uv.xver-[source].[target]` (e.g., `hl7.fhir.uv.xver-r5.r4`).

The following table lists the current generated combinations with links to the packages that are published. Note that packages
to target DSTU2 are not planned and packages to and from R6 are pending R6 publication.

|          | DSTU2 Content | STU3 Content | R4 Content | R4B Content | R5 Content | R6 Content |
|----------|---------------------------|---------------------------|---------------------------|----------------------------|---------------------------|---------------------------|
| In DSTU2 | - | ~~`hl7.fhir.uv.xver-r3.r2`~~ | ~~`hl7.fhir.uv.xver-r4.r2`~~ | ~~`hl7.fhir.uv.xver-r4b.r2`~~ | ~~`hl7.fhir.uv.xver-r5.r2`~~ | ~~`hl7.fhir.uv.xver-r6.r2`~~ |
| In STU3  | [`hl7.fhir.uv.xver-r2.r3`](https://hl7.org/fhir/uv/xver-r2.r3/)   | -                                                                | [`hl7.fhir.uv.xver-r4.r3`](https://hl7.org/fhir/uv/xver-r4.r3)   | [`hl7.fhir.uv.xver-r4b.r3`](https://hl7.org/fhir/uv/xver-r4b.r3)  | [`hl7.fhir.uv.xver-r5.r3`](https://hl7.org/fhir/uv/xver-r5.r3)   | `hl7.fhir.uv.xver-r6.r3`  |
| In R4    | [`hl7.fhir.uv.xver-r2.r4`](https://hl7.org/fhir/uv/xver-r2.r4/)   | [`hl7.fhir.uv.xver-r3.r4`](https://hl7.org/fhir/uv/xver-r3.r4)   | -                                                                | [`hl7.fhir.uv.xver-r4b.r4`](https://hl7.org/fhir/uv/xver-r4b.r4)  | [`hl7.fhir.uv.xver-r5.r4`](https://hl7.org/fhir/uv/xver-r5.r4)   | `hl7.fhir.uv.xver-r6.r4`  |
| In R4B   | [`hl7.fhir.uv.xver-r2.r4b`](https://hl7.org/fhir/uv/xver-r2.r4b/) | [`hl7.fhir.uv.xver-r3.r4b`](https://hl7.org/fhir/uv/xver-r3.r4b) | [`hl7.fhir.uv.xver-r4.r4b`](https://hl7.org/fhir/uv/xver-r4.r4b) | -                                                                 | [`hl7.fhir.uv.xver-r5.r4b`](https://hl7.org/fhir/uv/xver-r5.r4b) | `hl7.fhir.uv.xver-r6.r4b` |
| In R5    | [`hl7.fhir.uv.xver-r2.r5`](https://hl7.org/fhir/uv/xver-r2.r5/)   | [`hl7.fhir.uv.xver-r3.r5`](https://hl7.org/fhir/uv/xver-r3.r5)   | [`hl7.fhir.uv.xver-r4.r5`](https://hl7.org/fhir/uv/xver-r4.r5)   | [`hl7.fhir.uv.xver-r4b.r5`](https://hl7.org/fhir/uv/xver-r4b.r5)  | -                                                                | `hl7.fhir.uv.xver-r6.r5`  |
| In R6    | `hl7.fhir.uv.xver-r2.r6`   | `hl7.fhir.uv.xver-r3.r6`  | `hl7.fhir.uv.xver-r4.r6`  | `hl7.fhir.uv.xver-r4b.r6`  | `hl7.fhir.uv.xver-r5.r6`  | -                         |



### Known Limitations

* Not 100% coverage of all elements in all versions
    * `Resource` type elements are excluded (e.g., R5:`Bundle.issues`)
* Mappings are generally between adjacent versions, so "back-and-forth" conversions may be needlessly verbose
* Large / infinite value sets (e.g., UCUM, LOINC, MIME) are excluded and assumed 'equivalent' across versions
* Mapping elements that split into multiple elements has a lot of complications that are out-of-scope for this package, but should be noted when using it.
    E.g., when mapping from a single `CodeableReference` element to `CodeableConcept` and `Reference` elements, decisions must be made about any existing extensions, etc.

### Intellectual Property Statements

{% include ip-statements-en.xhtml %}