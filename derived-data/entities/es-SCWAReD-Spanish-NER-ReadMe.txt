## How we generated the entity files
The entity files for each Spanish-language SCWAReD workset were generated using a custom, fine-tuned large language model, via [spaCy's Transformer](https://spacy.io/api/transformer) implementation. We benchmarked multiple Spanish-language transformer models, but ended up settling on an English-language model (`en_core_web_trf 3.3.0`) fine-tuned for our Spanish data, as it yielded the highest accuracy. We are working on a research paper detailing these findings, and will link to it here once it is published. Large language models, especially when fine-tuned for the specific data of use, generate state-of-the-art named entity recognition (NER) results with a high level of accuracy. The data was accessed and the NER pipeline was implemented using [HTRC Data Capsule](https://htrc.atlassian.net/wiki/spaces/COM/pages/43286886/HTRC+Data+Capsule+Environment) environment, with many of the books being subject to copyright, which prevents their full text from being shared and accessed directly.

For more specific technical documentation, see the "Technical documentation and reproducibility" section below.

## How to read the entity files
Each entity file has the following columns:

| Column Label     | Description |
| ----------- | ----------- |
| vol_id    | The HathiTrust ID for the source volume      |
| page   | The page on which the entity appears       |
| sentence_id   | The ID for the sentence on that page in which the entity appears        |
| ent_id   | An ID given to each unique entity, per volume        |
| entity   | The entity string, as it appears in text      |
| entity_type   | The entity type (or tag) produced by our algorithm        |
| start_char   | The number, by page, of the first character in the entity string      |
| end_char  | The number, by page, of the last character in the entity string      |

The entity types produced are standard based on the NER implementation, with the en_core_web_trf model, upon which our custom model is based, producing the following tags:

| Entity Label    | Description |
| ----------- | ----------- |
| CARDINAL   | Numerals not covered by other labels |
| DATE   | Dates, absolute ("May 1") or relative ("tomorrow")|
| EVENT   | Named events, such as wars, natural disasters, or sporting events |
| FAC   | Facilities, such as buildings, ports, roads |
| GPE   | Geopolitical entities, such as countries, states |
| LANGUAGE   | Named languages, real or fictional |
| LAW   | Named laws and law documents |
| LOC   | Non-GPE locations, including natural locations (oceans, mountains) |
| MONEY   | Monetary values with units |
| NORP   | Nationalities, religious or political groups |
| ORDINAL   | A number defining a position in a series (such as "first" or "second" |
| ORG   | Organizations, like companies or agencies |
| PERCENT   | Percentages, with % |
| PERSON   | Named people, real or fictional |
| PRODUCT   | Non-service products, like objects, vehicles, etc. |
| QUANTITY   | Measurements (e.g. weight, distance) |
| TIME   | Times mentioned smaller than 1 day |
| WORK_OF_ART   | Titles of named works of art |

Entities are available per-volume (via files with an HTID as their filename) or via workset (via files with a fileame corresponding to a SCWAReD workset).

## Technical documentation and reproducibility
The pipeline was developed on Linux (Ubuntu, version 2020.07) with Anaconda environment for Python. The extracted results from this project were generated using a custom spaCy transformer model, fine-tuned from a base `en_core_web_trf 3.3.0` transformer model. The initial Anaconda environment requirements can be found in `es-conda-env-cuda117.yml`. The additional pip requirements can be found in `es-pip-env-cuda117.txt`. We separate the two requirements to avoid dependency conflicts and make sure the environment is consistent on different system

Make sure you have downloaded the model along with this repository using git lfs to support large file download. (More info about git lfs: https://git-lfs.com/)

To install git lfs and pull the large files
```
git lfs install
git lfs pull
```


1. If it doesn't exist yet, create anaconda environment tor run spacy transformers model using
```
conda env create -f conda-env-cuda117.yml
```
This will create a Python environment named spacy-cuda117 that will allow the extraction execution.
The environment will be perfectly running with NVIDIA GPU available and the cuda driver 11.7 installed to access the full power.
Otherwise, the environment should still be runnable with CPU only processing.

2. Activate  the environment
```
conda activate spacy-cuda117
```

3. Make sure the anaconda environment is active by looking at the bash prompt, it should mentioned the environment like this
```
(spacy-cuda117) [someuser@somesystem en_ner]$
```
In this activated cuda117 environment and install pip requirements by executing
```
pip install --no-deps -r pip-env-cuda117.txt
```
Make sure the --no-deps is included to force installation without looking at dependency since we are using a specific library required for cuda driver 11.7

4. The data should be placed on scwared-spanish-data folder. In this scwared spanish datasets, we also have categorized the input volumes into sub-genre where each datasets will be placed under the folder representing the sub-genre.
We used compressed zip format in this case as our input data. If one want to perform this pipeline on HTRC analytics data capsule, they can modified extraction scripts or compressed the volume folder into a zip where one zip represents one volume.

5. Run the extraction script using ipython for interactivity with the bash prompt, this will read all the zip files in the scwared_data folder and create a csv file in the scwared-spanish-custom folder for each sub-genre folder represented on the input folder. This model only have 4 output classes for now: PER (Person), LOC (Location), ORG (Organization), and MISC (Miscelaneous) More info on training this custom model can be found at datasets folder.
```
ipython es-NER-Spacy.py
```

6. Besides the custom model, we also have prepared scripts for extracting entities using the Spacy en-core-web-trf 3.3.0 model that supposedly can help detect other entities that are not captured by the Spanish custom model. The output of this model will be created under scwared-spanish-enmodel
```
ipython es-NER-Spacy.py
```