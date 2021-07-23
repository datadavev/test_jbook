---
title: Test JBook

---
# Test JBook

Example of simple jupyter book.

Source
:https://github.com/datadavev/test_jbook

Rendered
:https://datadavev.github.io/test_jbook/

## Setup:

```
mkvirtualenv jupyterbook
pip install jupyter-book
pip install pyld
git clone https://github.com/datadavev/test_jbook.git
cd test_jbook
jupyter-book build .
mv _build/html docs
touch docs/.nojekyll
open docs/index.html
```
