README for workset directory

# Introduction
The public version of the worksets is hosted by the [HathiTrust Research Center](http://analytics.hathitrust.org/) (HTRC) at <https://analytics.hathitrust.org/worksets/biblicon/Boom%20and%20related%20texts>, <https://analytics.hathitrust.org/worksets/biblicon/Indigenismo>, <https://analytics.hathitrust.org/worksets/biblicon/Mexican%20Rev.%20Narrative%20Canon>, <https://analytics.hathitrust.org/worksets/biblicon/Modernismo%20Fiction>, <https://analytics.hathitrust.org/worksets/biblicon/Modernismo%20Novels>, <https://analytics.hathitrust.org/worksets/biblicon/Narcoliterature>, <https://analytics.hathitrust.org/worksets/biblicon/Colombia_narrative%20about%20violence>.

The `workset` directory contains multiple data files with metadata about the workset and its volumes. Details about each file, its format, and structure are included below:

## `scwared-spanish-american-fiction-Boom.csv`
## `scwared-spanish-american-fiction-Indigenismo.csv`
## `scwared-spanish-american-fiction-Mexican-Rev.csv`
## `scwared-spanish-american-fiction-Modernismo-Fiction.csv`
## `scwared-spanish-american-fiction-Modernismo-Novels.csv`
## `scwared-spanish-american-fiction-Narcoliterature.csv`
## `scwared-spanish-american-fiction-Violencia.csv`

This is a simple CSV file listing the volume ID and some additional metadata for each volume in the workset. The CSV file may be edited by removing and adding volume, and the edited file may used as the basis for a new workset. The full CSV file or simply a text file with a list of volume IDs may be uploaded to <https://analytics.hathitrust.org/uploadworkset> to create a new workset.

The columns in the CSV file are:

- id (volume identifier)
- title 
- year (year of publication)
- language (volume language represented as ISO-369-3 language code) 
- authors

Example:

| id | title | year | language | authors |
|:---|:---   |:---  |:---      |:---     |
| mdp.39015008882774 | The Buenos Aires affair / Manuel Puig. | 1973 | spa | Puig, Manuel |
| inu.30000027285851 | La consagracion de la primavera / Alejo Carpentier. | 1989 | spa | Carpentier, Alejo 1904-1980 |
| txu.059173026562827 | El beso de la mujer aran?a / Manuel Puig. | 1988 | spa | Puig, Manuel |
| mdp.39015027201717 | En alg?n valle de l?grimas / Jos? Revueltas. | 1979 | spa | Revueltas, Jos? 1914-1976 |
| uc1.32106018901717 | El lugar sin li?mites / Jose? Donoso. | 1987 | spa | Donoso, Jose? 1924- |

## `scwared-spanish-american-fiction-Boom.json`
## `scwared-spanish-american-fiction-Indigenismo.json`
## `scwared-spanish-american-fiction-Mexican-Rev.json`
## `scwared-spanish-american-fiction-Modernismo-Fiction.json`
## `scwared-spanish-american-fiction-Modernismo-Novels.json`
## `scwared-spanish-american-fiction-Narcoliterature.json`
## `scwared-spanish-american-fiction-Violencia.json`

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

