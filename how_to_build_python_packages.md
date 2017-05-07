# How to build python packages memo
# author: ksnt

\:smile: enojoyable!

## Directory Structure
```
package_directory_name<br>
|--package_name <br>
|  |--__init__.py <br>
|  |--sample.py <br>
|--README.md <br>
|--setup.py <br>
|--setup.cfg <br>
|--LICENSE.txt <br>
|--.gitignore <br>
```

## Sample Source Code

\_\_init\_\_.py
```
from .sample import method1
from .sample import method2
```

sample.py
```
#!/usr/bin/env python
# -*- coding: utf-8 -*-
def method1():
    print("method1")
def method2():
    print("method2")
```

setup.py
```
from setuptools import setup,find_packages

setup(name='package_name',
      version='0.1',
      description='Something you like',
      url='your_project_url',
      author='Author Name',
      author_email='your_account@mail.com',
      license='MIT',
      packages=find_packages(),
      zip_safe=False       
    )
```

README.md
```
Write something about your projet
```

setup.cfg
```
[metadata]
description-file = README.md
```   

.gitignore
```
# Compiled python modules.
*.pyc

# Setuptools distribution folder.
/dist/

# Python egg metadata, regenerated from source files by setuptools.
/*.egg-info
```

LICENSE.txt (MIT License here)
```
Copyright YEAR YOUR NAME

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
```

## Upload

1.Setup.<br>
$python3 setup.py sdist <br>

2.Upload all files to a repository in Github. (Use "git push")


## Install and Remove from Github

Install <br>
$sudo pip install -U git+https://github.com/ksnt/package_directory_name.git <br>

Remove <br>
$sudo pip uninstall package_name

