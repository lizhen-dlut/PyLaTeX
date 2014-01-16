PyLaTeX
=======

PyLaTeX is a Python library for creating LaTeX files. The point of this library
is being an easy, but extensible interface between Python and LaTeX.


### Features

The library contains some basic features I have had the need for so far.
Currently those are:

- Document generation and compilation
- Section, table, math and package classes
- A matrix class that can compile NumPy ndarrays and matrices to LaTeX
- An escape function
- Bold and italic functions

Everything else you want you can still add to the document by adding LaTeX
formatted strings instead of classes or regular strings.


### Dependencies

- Python 3.3 (Python 3.x might work as well)
- pdflatex (only if you want to compile the tex file)
- NumPy (only if you want to convert it's matrixes)


### Installation
`pip install pylatex`


### Examples

Basics:

```python
from pylatex import Document, Section, Table
from pylatex.utils import italic

doc = Document()
section = Section('Yaay the first section, it can even be ' + italic('italic'))

table = Table('r|ccl')
table.add_hline()
table.add_row((1, 2, 3, 4))
table.add_hline(1, 2)
table.add_empty_row()
table.add_row((4, 5, 6, 7))

section.content.append(table)
doc.content.append(section)
doc.generate_pdf()
```

This code will generate this:
![Generated PDF by PyLaTeX](https://raw.github.com/JelteF/PyLaTeX/master/docs/static/screenshot.png)


Numpy:

```python
import numpy as np

from pylatex import Document, Section, Subsection, Table, Math
from pylatex.numpy import Matrix, format_vec


a = np.array([[100, 10, 20]]).T

doc = Document()
section = Section('Numpy tests')
subsection = Subsection('Array')

vec = Matrix(a)
vec_name = format_vec('a')
math = Math(data=[vec_name, '=', vec])

subsection.append(math)
section.append(subsection)

subsection = Subsection('Matrix')
M = np.matrix([[2, 3, 4],
               [0, 0, 1],
               [0, 0, 2]])
matrix = Matrix(M, mtype='b')
math = Math(data=['M=', matrix])

subsection.append(math)
section.append(subsection)


subsection = Subsection('Product')

math = Math(data=['M', vec_name, '=', Matrix(M*a)])
subsection.append(math)

section.append(subsection)

doc.append(section)
doc.generate_pdf()
```


### Future development

I will keep adding functionality I need to this library, an interface for
graphics and math will probably be added in a future version.

If you add a feature yourself, or fix a bug, please send a pull request.

You can submit issues, but it will not be my priority to fix them. My job and
education are a bit higher on the priority list.


### Support

This library is being developed for Python 3.3. It currently doesn't work for
Python 2.7, but it's mostly syntax and import changes that break it for 2.7.
It is also only tested on Linux, so it might not work on any different
platforms.

I have no intention of testing on any different platforms or with different
Python versions. I also don't have the intention to write fixes for platform or
environment specific bugs, but pull requests that fix those are always welcome.


### Copyright and License

Copyright 2014 Jelte Fennema, under [the MIT
license](https://github.com/JelteF/PyLaTeX/blob/master/LICENSE)
