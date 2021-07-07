# Test JBook

Example of simple jupyter book.

See: https://github.com/datadavev/test_jbook

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
