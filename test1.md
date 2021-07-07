---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
kernelspec:
  display_name: Python 3
  language: python
  name: python3
execution:
  allow_errors: true
---

# Test Page

Reference segment of external file.

```{literalinclude} test1.jsonld
:linenos:
```

Include selection of lines:

```{literalinclude} test1.jsonld
:linenos:
:lines: 2-5
```

Include selection of lines and emphasize 2 lines:

```{literalinclude} test1.jsonld
:linenos:
:lines: 2-10
:emphasize-lines: 4,7
```

Sadly, I have not found a way to format text output directly:

```{code-cell}
:tags: [hide-input]

import json
import pyld
import os
import requests

SO_CONTEXT = {
    "http://schema.org": "jsonldcontext.jsonld",
    "http://schema.org/": "jsonldcontext.jsonld",
    "https://schema.org": "jsonldcontext.jsonld",
    "https://schema.org/": "jsonldcontext.jsonld",
}

if not os.path.exists("jsonldcontext.jsonld"):
    with open("jsonldcontext.jsonld", "w") as outf:
        outf.write(requests.get("https://schema.org/docs/jsonldcontext.jsonld").text)

def localDocumentLoader(context_map={}):

    def localDocumentLoaderImpl(url, options={}):
        _url = url.lower().strip()
        doc = context_map.get(_url, None)
        if not doc is None:
            res = {
                "contextUrl": None,
                "documentUrl": "https://schema.org/docs/jsonldcontext.jsonld",
                "contentType": "application/ld+json",
                "document": json.load(open(doc, "r")),
            }
            return res
        loader = pyld.jsonld.requests_document_loader()
        return loader(url)
    
    return localDocumentLoaderImpl
    

with open("test1.jsonld") as inf:
    doc = json.load(inf)
options = {"documentLoader": localDocumentLoader(context_map=SO_CONTEXT)}
expanded = pyld.jsonld.expand(doc, options)
print(json.dumps(expanded, indent=2))
with open("tmp.jsonld", "w") as outf:
    json.dump(expanded, outf, indent=2)
```

Except by writing to a file and including:

```{literalinclude} tmp.jsonld
:linenos:
:emphasize-lines: 3
```


