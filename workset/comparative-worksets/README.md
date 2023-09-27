README for comparative worksets directory

# Introduction
The public version of the worksets is hosted by the [HathiTrust Research Center](http://analytics.hathitrust.org/) (HTRC) at <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionArgentina>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionBolivia>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionChile>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionColombia>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionCuba>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionEcuador>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionMexico>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionPeru>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionPuertoRico>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionUruguay>, <https://analytics.hathitrust.org/worksets/isabella/SCWAReD-UnsortedFictionVenezuela>.

The `workset` directory contains multiple data files with metadata about the workset and its volumes. Details about each file, its format, and structure are included below.



# `scwared-unsorted-fiction-argentina.csv`
# `scwared-unsorted-fiction-bolivia.csv`
# `scwared-unsorted-fiction-chile.csv`
# `scwared-unsorted-fiction-colombia.csv`
# `scwared-unsorted-fiction-cuba.csv`
# `scwared-unsorted-fiction-mexico.csv`
# `scwared-unsorted-fiction-peru.csv`
# `scwared-unsorted-fiction-puertorico.csv`
# `scwared-unsorted-fiction-uruguay.csv`
# `scwared-unsorted-fiction-venezuela.csv`

This is a simple CSV file listing the volume ID and some additional metadata for each volume in the workset. The CSV file may be edited by removing and adding volume, and the edited file may used as the basis for a new workset. The full CSV file or simply a text file with a list of volume IDs may be uploaded to <https://analytics.hathitrust.org/uploadworkset> to create a new workset.

The columns in the CSV file are:

- id (volume identifier)
- title 
- year (year of publication)
- language (volume language represented as ISO-369-3 language code) <!-- is this correct? -->
- authors

Example:

| id | title | year | language | authors |
|:---|:---   |:---  |:---      |:---     |
| txu.059173024462719 | Una nube llamada Helena; [ensayos] | 1958 | spa | Lanuza, JoseÃÅ Luis, 1903- |
| uc1.$b774760 | Advenimiento, | 1947 | spa | Capdevila, Arturo, 1889-1967. |
| txu.059173026715098 | El derrumbe / | 1985 | spa | Yudicello, Lucio, 1950- |
| uva.x000516455 | El rat√≥n; novela. | 1970 | spa | Nella Castro, Ant√≥nio. |
| txu.059173000710656 | De antiheÃÅroes y guerras / | 1993 | spa | Mantel, A. R. (Antonio RauÃÅl) |

# `scwared-unsorted-fiction-argentina.json`
# `scwared-unsorted-fiction-bolivia.json`
# `scwared-unsorted-fiction-chile.json`
# `scwared-unsorted-fiction-colombia.json`
# `scwared-unsorted-fiction-cuba.json`
# `scwared-unsorted-fiction-mexico.json`
# `scwared-unsorted-fiction-peru.json`
# `scwared-unsorted-fiction-puertorico.json`
# `scwared-unsorted-fiction-uruguay.json`
# `scwared-unsorted-fiction-venezuela.json`

This is a [JSON-LD](https://json-ld.org) file with some basic metadata about the workset itself, including `title`, `description`, `id`, creation date (`created`), `creator`, `contributor`, and number of volumes (`extent`). Also included is a list of workset volume IDs as persistent links to the item in the [HathiTrust Digital Library](https://hathitrust.org). Here is an example of the list of volumes:

```
"gathers": [
        {"id": "http://hdl.handle.net/2027/txu.059173026574393"},
        {"id": "http://hdl.handle.net/2027/txu.059173026736892"},
        {"id": "http://hdl.handle.net/2027/txu.059173023793492"},
        {"id": "http://hdl.handle.net/2027/txu.059173024468760"},
        {"id": "http://hdl.handle.net/2027/txu.059173001165383"},
        …
        {"id": "http://hdl.handle.net/2027/txu.059173023790009"},
        {"id": "http://hdl.handle.net/2027/pst.000004885726"},
        {"id": "http://hdl.handle.net/2027/txu.059173028010300"}
    ]
```
Here is detailed information about each field in the workset JSON-LD:

|property | range | type | cardinality | description |
|:--- |:--- |:---  |:--- |:--- |
id | rdfs:Resource | URL | 1 | The URL that resolves to this document |
type | rdfs:Resource | URL | 1 | The URL representing an HTRC Workset |
created | xsd:date | date (YYYY-MM-DD) | 1 | The unary property describing the date on which the Collection was created. |
extent | xsd:integer | integer > 0 | 1 | The unary property describing the amount of content gathered into a Collection. |
gathers | rdfs:Resource | URL | 1 or more | The relationship between a Collection and an item (Handle URL) that has been gathered into it. |
creator | dcterms:Agent | URL or string | 0 or more | The relationship between a Collection and one or more agents responsible for its creation. (New Worksets don't have this value because HT no longer includes this info when sending Collections, but some older Worksets were created when HT was still sending over the info. JSON-LD files for SCWAReD worksets have been edited to include creator details.) |
contributor | dcterms:Agent | URL or string | 0 or more | The property naming non-creator agent(s) responsible for contributing to creation of the collection. (Some worksets don't have this value, as contributor is reserved for worksets created with HTRC collaborators) |
title | xsd:string | string | 1 | The unary property that captures a string value that names the Collection. |
intendedForUse | rdfs:Resource | URL | 1 or more | This relationship captures the research context in which the creator(s) intend the Collection to be used in. A Workset MUST have at least one htrc:intendedForUse relation which names the HathiTrust Research Center as a research context. A Workset MAY have additional named research contexts through additional htrc:intendedForUse relations. These contexts may be as broad as other named research centers or as narrow as particular algorithms or machine workflows. However, current workset generation tools do not allow adding additional intendedForUse values, so you can expect this to only ever have the HTRC value. |
description | rdfs:Resource or rdfs:Literal | URL or string | 0 or 1 | The relationship between the Collection and another resource or string of text that describes the Collection in natural language. |
hasCriterion | rdfs:Resource or rdfs:Literal | URL or string | 0 or more | This relationship captures the criterion or criteria by which the Collection creator(s) selected resources to gather into it. |
hasResearchMotivation | rdfs:Resource or rdfs:Literal | URL or string | 0 or more | This relationship captures the motivating question(s) that the Collection's creator(s) intended the Workset to help answer. |
modified | xsd:date | date (YYYY-MM-DD) | 0 or 1 | The unary property describing the date on which the Collection was most recently modified. A Workset MUST have exactly 1 dcterms:modified property with a range of xsd:date if and only if it has last been modified on a different date than the one reflected by its created date. Otherwise, a Workset MAY have 0 dcterms:modified properties (reflecting the state of affairs of having not yet been modified). |
publisher | dcterms:Agent | URL or string | 0 or more | The relationship between a Collection and an agent who publishes it in some context. In the case of publically shared Worksets in the HTRC context, this publisher will typically be HTRC. Private Worksets remain unpublished. A Workset MAY have 1 or more dcterms:publisher relationships, of which, at least one will typically be HTRC. |
hasVisibility |  | string | 1 | The unary property that sets a Workset to be 'public' or 'private'. Only worksets where htrc:hasVisiblity is set to 'public' are available through the API. |

|prefix | base URL |
|:--- |:--- |
dcterms | http://purl.org/dc/terms/ |
rdfs | http://www.w3.org/2000/01/rdf-schema# |
xsd | http://www.w3.org/2001/XMLSchema# |


Unlike the CSV file described above, the JSON file may not be uploaded directly in HTRC’s existing tools to create a new workset; however, the JSON file is the canonical source of metadata and volume IDs for the workset.