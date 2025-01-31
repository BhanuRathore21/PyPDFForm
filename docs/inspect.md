# Inspect a PDF form

After a PDF form is prepared, PyPDFForm can be used to inspect names of all its widgets so that the data 
that's needed to fill it can be determined. There are several different methods this can be done with and feel free 
to choose the way that fits your needs the most.

This section of the documentation will use 
[this PDF](https://github.com/BhanuRathore21/PyPDFForm/raw/master/pdf_samples/sample_template.pdf) as an example.

## Generate a preview PDF

The first method of inspecting a PDF form is to generate a preview document. Each `PdfWrapper` object contains an 
attribute `.preview` which is a file stream that can be written to any disk file or memory buffer. Consider the 
following snippet:

```python
from PyPDFForm import PdfWrapper

preview_stream = PdfWrapper("sample_template.pdf").preview

with open("output.pdf", "wb+") as output:
    output.write(preview_stream)
```

The generated preview PDF will have the name of each widget labeled on top of it in red.

## Generate a JSON schema that describes a PDF form

The dictionary that's used to fill a PDF form can be described using a JSON schema. For example:

```python
import json

from PyPDFForm import PdfWrapper

pdf_form_schema = PdfWrapper("sample_template.pdf").schema

print(json.dumps(pdf_form_schema, indent=4, sort_keys=True))
```

The above snippet will yield the following output:

```json
{
    "properties": {
        "check": {
            "type": "boolean"
        },
        "check_2": {
            "type": "boolean"
        },
        "check_3": {
            "type": "boolean"
        },
        "test": {
            "type": "string"
        },
        "test_2": {
            "type": "string"
        },
        "test_3": {
            "type": "string"
        }
    },
    "type": "object"
}
```

In this case `sample_template.pdf` has three text fields named `test`, `test_2`, and `test_3` because they all have 
a type of `string`. It also has three checkboxes `check`, `check_2`, and `check_3` due to their `boolean` type.

The JSON schema generated by PyPDFForm can be used to validate against the data you use to fill a PDF form.

## Generate sample data

Lastly, PyPDFForm can generate some sample data that can be directly used to fill a PDF form:

```python
from pprint import pprint

from PyPDFForm import PdfWrapper

pprint(PdfWrapper("sample_template.pdf").sample_data)
```

The above snippet will give you a sample dictionary:

```sh
{'check': True,
 'check_2': True,
 'check_3': True,
 'test': 'test',
 'test_2': 'test_2',
 'test_3': 'test_3'}
```
