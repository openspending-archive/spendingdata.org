---
layout: standard
title: Technical Specification
---

The primary goal of this specification is to be **useful**: we want to offer a format that can 
be easily generated from commonly-used financial management systems and, most of all, a format 
that helps by end-users - whether they are tech-literate developers or data journalists whose
skills may be very limited.

A good example for a **pragmatic specification** is the [General Transit Feed Specification](https://developers.google.com/transit/gtfs/reference) by Google, which is widely used to share timetable and route information between public transport providers and data re-users (originally Google Maps).

<h3>What is transactional spending data?</h3>

Spending data in this document refers to transactional information as evidence of individual (or lightly aggregated) payments of government to a supplier or other recipient. This is different 
it from budgetary information, in which high-level, aggregate figures describe projected or executed
spending allocated under programmes or objectives.

<h3>What aspects of the data will be covered by the standard?</h3>

The standard will combine two parts: the **core specification** and additional **modules**. The core will include instructions on the packaging of spending datasets to combine data and metadata, a minimal set of required metadata attributes and a modeling system in which modules can be expressed. Modules then extend the standard to cover additional concerns, such as the identification of geographic relations, organisations (such as suppliers) and the unified expression of classification schemes.

<img src="https://docs.google.com/drawings/pub?id=1G17c02V_7d_1hUAWcYseM_aWm32Cyk_RX8DGLfJLnK0&amp;w=620&amp;h=465">

<h3>What will be covered by the core specification?</h3>

* Container format for dataset packaging
* Instructions on the use of CSV (RFC 4180)
* Best practices regarding publication form, interval and licensing.

<h3>What initial concepts/modules should there be?</h3>

* The most common type of reference data will be **classifications and taxonomies**. We'll aim to include ways to specify and use classification schemes, including metadata (such as whether a scheme is an insititutional, economic or function classification). We will also aim to collect mappings/spines that map country- or region-specific classifications to internationally recognized taxonomies like [COFOG](http://unstats.un.org/unsd/cr/registry/regcst.asp?Cl=4).
* **Entities, such as corporate and other suppliers, public bodies and government divisions need to be assigned unique identifiers (URIs)**. While [freely usable identifiers for companies](http://opencorporates.com/) are beginning to be available, for other entities such reference data is missing. We'll provide guidance on the coinage of identifiers and attempt to link to relevant databases.
* Support for **geographic identifiers**, both in terms of precise location (i.e. geocoding) and specifying administrative regions to which funds have been allocated. 
* **Procurement and awards data** describing the process in which the funds were allocated, as well as the **contractual terms** covering the expenditure. 

<h3>What other modules should there be?</h3>

Of course, the information expressed in these core modules is just a part of the data that may be available to augment expenditure information. Other important aspects in the future will include: 

* Information related to the options for public participation in the planning and allocation of expenditure. 
* What else? Send us your ideas! 

<h3>Does the standard cover legal aspects?</h3>

The standard does not contain a direct legal component, but governments and organisations that release data in the specified format must also supply a license which is in accordance with the [open definition](http://opendefinition.org/) and thus enables free and non-discriminatory re-use of the information.

<h3>What are the components of the technical specification?</h3>

The specification will contain two parts: the **core specification** and additional **modules**. The core will include instructions on the packaging of spending datasets to combine data and metadata, a minimal set of required metadata attributes and a modeling system in which modules can be expressed. The modules themselves will specify and document well-known DSPL concept which can then be re-used across different datasets.

<h3>What file formats are used?</h3>

The format will be **[Comma Separated Values (CSV)](http://tools.ietf.org/html/rfc4180) for the data and [JavaScript Object Notation (JSON)](http://json.org/) for metadata**. The deciding argument for CSV is its universal tool support, both for export from all major databases and import into common tools, such as spreadsheet applications. Data and metadata documents will be **combined into a Zipfile container**.

<h3>How is metadata represented?</h3>

We're planning to use a [simple metadata dictionary](http://www.dataprotocols.org/en/latest/data-packages.html#metadata). 

<h3>Open Issues</h3>

* **Currency conversion**: do we want to specify a base currency (e.g. 2000 US Dollars or SDR) in which fact table data will be provided?
