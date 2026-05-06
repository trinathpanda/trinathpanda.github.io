---
layout: post
title: 'Getting Started with the dsjson Python Package'
date: 2025-10-04 00:00:00 +0000
categories: [Python, dsjson, Python Package]
tags: [python, dsjson, dataset-json, cdisc, clinical-data]
---

## Introduction
Dataset-JSON is a new CDISC standard for data exchange. It’s lightweight, machine-readable, and FDA-supported. This stands against the limitations of the SAS XPT format.  

If you are wondering *“Why JSON?”* then I highly recommend you read this [Blog Post](https://trinathp.wixsite.com/trinath-panda-24/post/dataset-json-the-future-of-clinical-data-exchange).  

I welcome your feedback. If you spot a bug, would like to see a new feature, or if any documentation is unclear — submit an issue through GitHub right [here](https://github.com/trinath-p/DSJSON-PY/issues).  

In this post, we’ll walk through a small example dataset and a specification file, and show how to work with them using `dsjson`.  

---

## Example Dataset and Specification
I have created a synthetic patient demographic dataset: 

| PatientID	| Age |	Sex | BirthDate |
|-----------|-----|-----|-----------|
| P001 | 25 | M | 2025-01-15 |
| P002 | 34 | F | 2025-02-10 |
| P003 | 29 | M | 2025-03-05 |
| P004 | 42 | F | 2025-04-20 |
| P005 | 31 | M | 2025-05-18 |

Here is the sample dataset specification:  

| Variable Name | Label | Type | Length | Codelist/Format |
|---------------|-------|------|--------|-----------------|
| PatientID | Patient Identifier | Char | 8 | N/A |
| Age | Age (Years) | Num | 3 | N/A |
| Sex | Sex |Char | 1 | N/A |
| BirthDate | Date of Birth | Char | 10 | YYYY-MM-DD |

---

## Installation

You can install `dsjson` with `pip`

``` terminal
pip install dsjson
```

---

## DSJSON in action

### Create the dataset in Pandas

Let's create the above dataset in Python as a dataframe,

``` python
import pandas as pd
from dsjson import to_dataset_json, extract_labels, make_column_metadata

data = {
    "PatientID": ["P001","P002","P003","P004","P005"],
    "Age": [25,34,29,42,31],
    "Sex": ["M","F","M","F","M"],
    "BirthDate": ["2025-01-15","2025-02-10","2025-03-05","2025-04-20","2025-05-18"]
}

df = pd.DataFrame(data)
print(df)

# Result:
#   PatientID  Age Sex   BirthDate
# 0      P001   25   M  2025-01-15
# 1      P002   34   F  2025-02-10
# 2      P003   29   M  2025-03-05
# 3      P004   42   F  2025-04-20
# 4      P005   31   M  2025-05-18
```

---

### Create column metadata for the Data

Since we already have a column specification (in CSV or Excel), we can use it directly.
The `extract_labels` function will read the labels from the specification file.
The variable length is automatically calculated from the maximum observed value in the dataframe.

``` python

spec_file = "the path of the specification file"

# Extract variable labels from the specification file 
variable_labels = extract_labels(spec_path=spec_file, sheet_name="Sheet1", variable_name_col="Variable Name", variable_label_col="Label")

print(variable_labels)

# Result:
# {'PatientID': 'Patient Identifier', 'Age': 'Age (Years)', 'Sex': 'Sex', 'BirthDate': 'Date of Birth'}

# Combine all metadata and create column metadata
colum_metadata = make_column_metadata(df=df, variable_labels=variable_labels, domain="DM")

print(colum_metadata)

# Result
#            itemOID       name               label dataType  length  keySequence
# 0  IT.DM.PatientID  PatientID  Patient Identifier   string       4            1
# 1        IT.DM.Age        Age         Age (Years)  integer       2            2
# 2        IT.DM.Sex        Sex                 Sex   string       1            3
# 3  IT.DM.BirthDate  BirthDate       Date of Birth   string      10            4
```

---

### Write to Dataset-JSON

The main function of the dsjson package simplifies writing top-level metadata.
It automatically creates the `datasetJSONCreationDateTime` and maps required/optional metadata fields.

``` python

dm = to_dataset_json(
    data_df=df,
    columns_df=colum_metadata,
    name="DM",
    label="Demographics",
    itemGroupOID="IG.DM",
    originator="xyz",
    sourceSystem_name="python",
    sourceSystem_version="3.13.7",
    fileOID="SDTM_DM",
    studyOID="abc",
    metaDataRef="asd",
    metaDataVersionOID="1.0"
    )

with open(r"C:\Downloads\dm.json", "w") as f:
    json.dump(dm, f, indent=4)

```

---

Here is the final dataset-JSON:
``` json
{
    "datasetJSONCreationDateTime": "2025-10-03T19:28:08.870176",
    "datasetJSONVersion": "1.1",
    "fileOID": "SDTM_DM",
    "originator": "xyz",
    "sourceSystem": {
        "name": "python",
        "version": "3.13.7"
    },
    "studyOID": "abc",
    "metaDataVersionOID": "1.0",
    "metaDataRef": "asd",
    "itemGroupOID": "IG.DM",
    "records": 5,
    "name": "DM",
    "label": "Demographics",
    "columns": [
        {
            "itemOID": "IT.DM.PatientID",
            "name": "PatientID",
            "label": "Patient Identifier",
            "dataType": "string",
            "length": 4,
            "keySequence": 1
        },
        {
            "itemOID": "IT.DM.Age",
            "name": "Age",
            "label": "Age (Years)",
            "dataType": "integer",
            "length": 2,
            "keySequence": 2
        },
        {
            "itemOID": "IT.DM.Sex",
            "name": "Sex",
            "label": "Sex",
            "dataType": "string",
            "length": 1,
            "keySequence": 3
        },
        {
            "itemOID": "IT.DM.BirthDate",
            "name": "BirthDate",
            "label": "Date of Birth",
            "dataType": "string",
            "length": 10,
            "keySequence": 4
        }
    ],
    "rows": [
        [
            "P001",
            25,
            "M",
            "2025-01-15"
        ],
        [
            "P002",
            34,
            "F",
            "2025-02-10"
        ],
        [
            "P003",
            29,
            "M",
            "2025-03-05"
        ],
        [
            "P004",
            42,
            "F",
            "2025-04-20"
        ],
        [
            "P005",
            31,
            "M",
            "2025-05-18"
        ]
    ]
}
```

---

## Wrap-up

* Dataset-JSON is the future of data exchange in clinical research.
* With `dsjson`, you can go from raw data to Dataset-JSON in just a few steps.
* Coming next: how to read a Dataset-JSON file back into two dataframes (data + metadata).

🔗 GitHub Repo – [DSJSON-PY](https://github.com/trinath-p/DSJSON-PY.git)



