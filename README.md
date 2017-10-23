Core ML Community Tools
=======================

Core ML community tools contains all supporting tools for CoreML model
conversion and validation. This includes Scikit Learn, LIBSVM, Caffe,
Keras and XGBoost.


We recommend using virtualenv to use, install, or build coremltools. Be
sure to install virtualenv using your system pip.

```shell
pip install virtualenv
```

Installation
------------

The method for installing *coremltools* follows the
[standard python package installation steps](https://packaging.python.org/installing/).
To create a Python virtual environment called `pythonenv` follow these steps:

```shell
# Create a folder for your virtualenv
mkdir mlvirtualenv
cd mlvirtualenv

# Create a Python virtual environment for your CoreML project
virtualenv pythonenv
```

To activate your new virtual environment and install `coremltools` in this environment, follow these steps:
```
# Active your virtual environment
source pythonenv/bin/active

# Install coremltools in the new virtual environment, pythonenv
(pythonenv) pip install -U coremltools
```

The package [documentation](https://apple.github.io/coremltools) contains
more details on how to use coremltools.

Dependencies
------------

*coremltools* has the following dependencies:

- numpy (1.12.1+)
- protobuf (3.1.0+)

In addition, it has the following soft dependencies that are only needed when
you are converting models of these formats:

- Keras (1.2.2, 2.0.4+) with Tensorflow (1.0.x, 1.1.x)
- Xgboost (0.6+)
- scikit-learn (0.15+)
- libSVM


Building from source
--------------------
To build the project, you need [CMake](https://cmake.org) to configure the project

```shell
cmake .
```

after which you can use make to build the project

```shell
make -j4
```

Building Installable Wheel
---------------------------
To make a wheel/egg that you can distribute, you can do the following

```shell
make dist 
```

Running Unit Tests
-------------------
To run the unit tests, from the repo root, run the following command:

```shell
make test
```

To add a new unit test, add it to the coremltools/test folder. Make sure you
name the file with a 'test' as the prefix.

Additionally, running unit-tests would require more packages (like
libsvm)

```shell
pip install numpy scikit-learn
```

To install libsvm

```shell
git clone https://github.com/cjlin1/libsvm.git
cd libsvm/
make
cd python/
make
```

To make sure you can run libsvm python bindings everywhere, you need the
following command, replacing <LIBSVM_PATH> with the path to the root of
your repository.

```shell
export PYTHONPATH=${PYTHONPATH}:<LIBSVM_PATH>/python
```

To install xgboost

```shell
git clone --recursive https://github.com/dmlc/xgboost
cd xgboost; cp make/minimum.mk ./config.mk; make -j4
cd python-package; python setup.py develop --user
```

To install keras (Version >= 2.0)

```shell
pip install keras tensorflow
```

If you'd like to use the old keras version, you can:

```shell
pip install keras==1.2.2 tensorflow
```


Building Documentation
----------------------
First install all external dependencies.

```shell
pip install Sphinx==1.5.3 sphinx-rtd-theme==0.2.4 numpydoc
pip install -e git+git://github.com/michaeljones/sphinx-to-github.git#egg=sphinx-to-github
```

You also must have the *coremltools* package install, see the *Building* section.

Then from the root of the repository:

```shell
cd docs
make html
open _build/html/index.html
```