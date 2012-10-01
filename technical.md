---
layout: standard
title: Data Format
---

**Version: 0.1, Sept. 27, 2012**

This document details a data format for the publication of transactional
expenditure data. Data is published in a set of CSV files. See below for
a description of the purpose and status of each file. 

This specification is strongly inspired by the [General Transit Feed
Specification](https://developers.google.com/transit/gtfs/reference)
which is widely used for the dissemination of public transit information.

### Feed Files

This specification defines the following files along with their associated content:

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Required</th>
    <th>Purpose</th>
  </tr>
  <tr>
    <td><a href="#transactions">transactions.txt</a></td>
    <td>Required</td>
    <td>Core information about transactions in the dataset 
      (fact table).</td>
  </tr>
  <tr>
    <td><a href="#suppliers">suppliers.txt</a></td>
    <td>Required</td>
    <td>Supplier (beneficiary) information to identify the recipient of
      funds.</td>
  </tr>
  <tr>
    <td><a href="#entities">entities.txt</a></td>
    <td>Required</td>
    <td>Data regarding departments or agencies involved in
      the transactions.</td>
  </tr>
  <tr>
    <td><a href="#projects">projects.txt</a></td>
    <td>Optional</td>
    <td>Project-centric information.</td>
  </tr>
  <tr>
    <td><a href="#programmes">programmes.txt</a></td>
    <td>Optional</td>
    <td>Descriptions of government programmes authorizing transactions.</td>
  </tr>
  <tr>
    <td><a href="#accounts">accounts.txt</a></td>
    <td>Optional</td>
    <td>Account specification. Represents a
      chart of accounts for the publisher.</td>
  </tr>
  <tr>
    <td><a href="#functions">functions.txt</a></td>
    <td>Optional</td>
    <td>Taxonomy codesheet for functional classifications of expenditure</td>
  </tr>
  <tr>
    <td><a href="#economic">economic.txt</a></td>
    <td>Optional</td>
    <td>Taxonomy codesheet for economic classifications of expenditure</td>
  </tr>
  <tr>
    <td><a href="#sectors">sectors.txt</a></td>
    <td>Optional</td>
    <td>Taxonomy codesheet for sectors classifications of expenditure</td>
  </tr>
  <tr><th colspan="3">To be discussed / specified</th></tr>
  <tr>
    <td>metadata.json</td>
    <td>Required</td>
    <td>DublinCore metadata in a simple representation.</td>
  </tr>
  <tr>
    <td>indicators.json</td>
    <td>Opional</td>
    <td>Indicator measurements related to a particular transaction or
programme.</td>
  </tr>
</table>

### File Requirements 

The [file requirements](https://developers.google.com/transit/gtfs/reference#FileRequirements) for GTFS files apply to this specification:

* All files in a must be saved as comma-delimited text.
* The first line of each file must contain field names. Each subsection of the Field Definitions section corresponds to one of the files in a transit feed and lists the field names you may use in that file.
* All field names are case-sensitive.
* Field values may not contain tabs, carriage returns or new lines.
* Field values that contain quotation marks or commas must be enclosed within quotation marks. In addition, each quotation mark in the field value must be preceded with a quotation mark. This is consistent with the manner in which Microsoft Excel outputs comma-delimited (CSV) files. For more information on the CSV file format, see [http://tools.ietf.org/html/rfc4180](http://tools.ietf.org/html/rfc4180).
* The following example demonstrates how a field value would appear in a comma-delimited file:
  * Original field value: Contains "quotes", commas and text
  * Field value in CSV file: "Contains ""quotes"", commas and text"
* Field values must not contain HTML tags, comments or escape sequences.
* Remove any extra spaces between fields or field names. Many parsers consider the spaces to be part of the value, which may cause errors.
* Each line must end with a CRLF or LF linebreak character.
* Files should be encoded in UTF-8 to support all Unicode characters. Files that include the Unicode byte-order mark (BOM) character are acceptable. Please see the Unicode FAQ for more information on the BOM character and UTF-8.
* Zip the files in your feed.


### Data Types

Data in the files can have a certain type specified. The following types
are recognized: 

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Example</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>string</td>
    <td>"Some text"</td>
    <td>A text string, UTF-8.</td>
  </tr>
  <tr>
    <td>date</td>
    <td>2012-09-27</td>
    <td>A date string in <a href="http://www.w3.org/TR/NOTE-datetime">ISO 8601</a> format. This can optionally 
        be given as a date/time combination, expanding to the full
        format given in the ISO specification.</td>
  </tr>
  <tr>
    <td>money</td>
    <td>102.44</td>
    <td>A numeric financial value, without any specification of currency. Money should always be stated in single
        units, not thousands or millions. Implementors are advised to
use appropriate internal data structures to represent financial values
(e.g. decimal).<br>The number is given with a dot as
separator for decimal places and no thousands separators.</td>
  </tr>
  <tr>
    <td>identifier</td>
    <td>34</td>
    <td>Identifier are integer numbers used to refer between data files.
        They should be used in the sense of auto-incrementing primary keys.</td>
  </tr>
  <tr>
    <td>url</td>
    <td>http://spendingdata.org/resource#section</td>
    <td>A <a
href="http://www.w3.org/Addressing/URL/4_URI_Recommentations.html">fully qualified URL</a> for a resource available on the web (i.e.
via HTTP or HTTPs).</td>
  </tr>
</table>

### Glossary

* **Transaction**: most granular level of expenditure which indentifies
  a single beneficiary receiving a specified amount of funds for some 
  service, under a government programme or as an entitlement. 

### File specifications

<h4><a name="transactions">transactions.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this transaction which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal identifer or transaction reference used by the data
      publisher (can be identical to the id).
    </td>
  </tr>
  <tr>
    <td>status</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Specify the current status of this transaction. No enumeration is
      specified yet, but concise, english-language descriptions are
      recommended. Example: <a href="http://iatistandard.org/codelists/activity_status">IATI Activity Status</a>.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of the purpose and context of this transaction,
      if available.
    </td>
  </tr>
  <tr>
    <td>financial_type</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Specify the type of financial instrument underlying this transaction. No
      enumeration is specified yet, but concise, english-language descriptions
      are recommended. Example: <a href="http://iatistandard.org/codelists/finance_type">IATI Finance Type</a>.
    </td>
  </tr>
  <tr>
    <td>invoice_number</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Invoice number stated through the vendor or supplier.
    </td>
  </tr>
  <tr>
    <td>rev_exp</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Specification of whether a transaction implies government spending
      or revenue. Valid values:
      <ul>
        <li>REVENUE</li>
        <li>EXPENDITURE</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>budget_line_item</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Line item from the budget authorizing this expenditure.
    </td>
  </tr>
  <tr>
    <td>amount_budgeted</td>
    <td>money</td>
    <td>Optional</td>
    <td>
      Monetary amount initially budgeted for this transaction, including
      any taxes.
    </td>
  </tr>
  <tr>
    <td>amount_allocated</td>
    <td>money</td>
    <td>Optional</td>
    <td>
      Monetary amount allocated for expenditure for this transaction, including
      any taxes.
    </td>
  </tr>
  <tr>
    <td>amount_executed</td>
    <td>money</td>
    <td>Required</td>
    <td>
      Monetary amount actually disbursed under this transaction, including
      any taxes.
    </td>
  </tr>
  <tr>
    <td>date_budgeted</td>
    <td>date</td>
    <td>Optional</td>
    <td>
      Date when the amount_budgeted had been decided.
    </td>
  </tr>
  <tr>
    <td>date_allocated</td>
    <td>date</td>
    <td>Optional</td>
    <td>
      Date when the allocation was made.
    </td>
  </tr>
  <tr>
    <td>date_completed</td>
    <td>date</td>
    <td>Required</td>
    <td>
      Date when the transaction was completed.
    </td>
  </tr>
  <tr>
    <td>date_reported</td>
    <td>date</td>
    <td>Optional</td>
    <td>
      Date when the transaction was reported to the publishing body.
    </td>
  </tr>
  <tr>
    <td>project_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Identifier linking to the project-centric metadata in <a href="#projects">projects.txt</a>.
    </td>
  </tr>
  <tr>
    <td>entity_id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>
      Information about the government entity responsible for this transaction, 
      as described in <a href="#entities">entities.txt</a>.
    </td>
  </tr>
  <tr>
    <td>purchaser_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the government entity acting as a purchaser for this, 
      if different from the institution controlling the project.
      Described in <a href="#entities">entities.txt</a>.
    </td>
  </tr>
  <tr>
    <td>supplier_id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>
      Information about the supplier, as described in <a href="#entities">entities.txt</a>.
    </td>
  </tr>
  <tr>
    <td>programme_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the underlying government programme, as described in <a href="#programmes">programmes.txt</a>.
    </td>
  </tr>
  <tr>
    <td>account_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the account in which this transaction was registered, as described in <a href="#programmes">programmes.txt</a>.
    </td>
  </tr>
  <tr>
    <td>account_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the account in which this transaction was registered, as described in <a href="#accounts">accounts.txt</a>.
    </td>
  </tr>
  <tr>
    <td>economic_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the economic classification of this transaction, as described in <a href="#economic">economic.txt</a>.
    </td>
  </tr>
  <tr>
    <td>function_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the functional classification of this transaction, as described in <a href="#functions">functions.txt</a>.
    </td>
  </tr>
  <tr>
    <td>sector_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      Information about the sector of this transaction, as described in <a href="#sectors">sectors.txt</a>.
    </td>
  </tr>
</table>

<h4><a name="suppliers">suppliers.txt</a></h4>

Suppliers are usually assumed to be privately incorporated companies,
sole traders or not-for-profit institutions. In some cases, transactions
may detail intra-governmental exchanges of funds, in which case a 
synthetic supplier definition pointing at the actual government entity 
should be used.

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this supplier which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>entity_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      If the transaction describes intra-governmental transfers, the 
      receiving department will be identified using this identifier,
      while the remainder of the supplier record will be disregarded.
    </td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Full legal name of the supplier.
    </td>
  </tr>
  <tr>
    <td>acronym</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Acronym commonly used by the supplier.
    </td>
  </tr>
  <tr>
    <td>legal_form</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Legal form of the supplier, i.e. the company type. 
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Company code used within the purchasing government entity, e.g. 
      vendor indentification.
    </td>
  </tr>
  <tr>
    <td>tax_identification</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      (Value-added) tax identification number assigned to the supplier.
    </td>
  </tr>
  <tr>
    <td>opencorporates_uri</td>
    <td>url</td>
    <td>Optional</td>
    <td>
      Identifier used on the <a href="http://opencorporates.com">OpenCorporates</a>
      identity resolution service.
    </td>
  </tr>
  <tr>
    <td>duns_number</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Dun &amp; Bradstreet D-U-N-S number used for the supplier in the
      US.
    </td>
  </tr>
  <tr>
    <td>street</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Street part of the suppliers trading address.
    </td>
  </tr>
  <tr>
    <td>post_code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Post code part of the suppliers trading address.
    </td>
  </tr>
  <tr>
    <td>city</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      City of the suppliers trading address.
    </td>
  </tr>
  <tr>
    <td>country_name</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Country name of the suppliers trading address.
    </td>
  </tr>
  <tr>
    <td>country_code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      2-letter alphanumeric <a href="http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">ISO 3166-1</a> country identifier of the suppliers trading address.
    </td>
  </tr>
</table>

<h4><a name="entities">entities.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this governemnt entity which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>
      The name of the superior government entity, e.g. the responsible
      department, ministry or other organ. This hierarchy can have any
      depth and should be precise.
    </td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Full name of the government entity.
    </td>
  </tr>
  <tr>
    <td>acronym</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Acronym commonly used by the government entity.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Department/entity code used within the government for financial 
      purposes.
    </td>
  </tr>
  <tr>
    <td>class</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Type of the government entity, e.g. department, unit, 
      arms-length body. No taxonomy is specified at the moment, but 
      should be made available in the future.
    </td>
  </tr>
  <tr>
    <td>ministerial_level</td>
    <td>boolean</td>
    <td>Optional</td>
    <td>
      Flag to indicate this governemnt entity is at ministerial level.
    </td>
  </tr>
  <tr>
    <td>street</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Street part of the government entity's trading address.
    </td>
  </tr>
  <tr>
    <td>post_code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Post code part of the government entity's trading address.
    </td>
  </tr>
  <tr>
    <td>city</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      City of the government entity's trading address.
    </td>
  </tr>
  <tr>
    <td>country_name</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Country name of the government entity's trading address.
    </td>
  </tr>
  <tr>
    <td>country_code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      2-letter alphanumeric <a href="http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">ISO 3166-1</a> country identifier of the government entity's trading address.
    </td>
  </tr>
</table>

<h4><a name="projects">projects.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this project which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the project.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this project or activity.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of the purpose and context of this project.
    </td>
  </tr>
  <tr>
    <td>start_date</td>
    <td>date</td>
    <td>Optional</td>
    <td>
      Date when the project began or is scheduled to begin.
    </td>
  </tr>
  <tr>
    <td>end_date</td>
    <td>date</td>
    <td>Optional</td>
    <td>
      Date when the project ended or is scheduled to be complete.
    </td>
  </tr>
</table>

<h4><a name="programmes">programmes.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this programme which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>An identifier for a wider programme, into which the specified
      programme is hierarchically embedded.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the programme.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this programme.
    </td>
  </tr>
  <tr>
    <td>budget_line_item</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Line item from the budget establishing this programme.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of the purpose and context of this programme.
    </td>
  </tr>
</table>

<h4><a name="accounts">accounts.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this account which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>An identifier for a wider account, into which the specified
      account is hierarchically embedded.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the account.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this account.
    </td>
  </tr>
  <tr>
    <td>level</td>
    <td>number</td>
    <td>Optional</td>
    <td>
      Hierarchy level of this account.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of the purpose and context of this account.
    </td>
  </tr>
</table>

<h4><a name="functions">functions.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this function which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>An identifier for a wider function, into which the specified
      function is hierarchically embedded.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the function.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this function.
    </td>
  </tr>
  <tr>
    <td>level</td>
    <td>number</td>
    <td>Optional</td>
    <td>
      Hierarchy level of this function.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of this function.
    </td>
  </tr>
</table>

<h4><a name="economic">economic.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this economic type which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>An identifier for a wider economic type, into which the specified
      economic type is hierarchically embedded.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the economic type.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this economic type.
    </td>
  </tr>
  <tr>
    <td>level</td>
    <td>number</td>
    <td>Optional</td>
    <td>
      Hierarchy level of this economic type.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of this economic type.
    </td>
  </tr>
</table>

<h4><a name="sectors">sectors.txt</a></h4>

<table class="table table-bordered table-condensed table-striped">
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Required</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>id</td>
    <td>identifier</td>
    <td>Required</td>
    <td>An identifier for this sector which is unique within the
        dataset and all similar datasets released by the same publisher.</td>
  </tr>
  <tr>
    <td>parent_id</td>
    <td>identifier</td>
    <td>Optional</td>
    <td>An identifier for a wider sector, into which the specified
      sector is hierarchically embedded.</td>
  </tr>
  <tr>
    <td>name</td>
    <td>string</td>
    <td>Required</td>
    <td>
      Name of the sector.
    </td>
  </tr>
  <tr>
    <td>code</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      Internal code used to identify this sector.
    </td>
  </tr>
  <tr>
    <td>level</td>
    <td>number</td>
    <td>Optional</td>
    <td>
      Hierarchy level of this sector.
    </td>
  </tr>
  <tr>
    <td>description</td>
    <td>string</td>
    <td>Optional</td>
    <td>
      A textual description of this sector.
    </td>
  </tr>
</table>




