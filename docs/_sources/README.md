# Test JBook

Example of simple jupyter book.


## Setup:

```
mkvirtualenv jupyterbook
pip install jupyter-book
pip install pyld
git clone https://github.com/datadavev/test_jbook.git
cd test_jbook
jupyter-book build .
open _build/html/index.html
```
