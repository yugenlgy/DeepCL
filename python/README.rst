.. raw:: html

   <!-- START doctoc generated TOC please keep comment here to allow auto update -->
   <!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

**Table of Contents** *generated with
`DocToc <https://github.com/thlorenz/doctoc>`__*

-  `PyDeepCL <#pyclconvolve>`__
-  `How to use <#how-to-use>`__
-  `Notes on how the wrapper works <#notes-on-how-the-wrapper-works>`__
-  `To install from pip <#to-install-from-pip>`__
-  `To build directly <#to-build-directly>`__
-  `Pre-requisites: <#pre-requisites>`__

   -  `Compilers <#compilers>`__
   -  `Python packages <#python-packages>`__

-  `To build: <#to-build>`__
-  `Considerations for Python wrapper
   developers <#considerations-for-python-wrapper-developers>`__
-  `To build, obsolete method <#to-build-obsolete-method>`__

.. raw:: html

   <!-- END doctoc generated TOC please keep comment here to allow auto update -->

PyDeepCL
========

Python wrapper for `DeepCL <https://github.com/hughperkins/DeepCL>`__

How to use
==========

See `test\_clconvolve.py <python/test_clconvolve.py>`__ for an example
of:

-  creating a network, with several layers
-  loading mnist data
-  training the network using a higher-level interface (``NetLearner``)

For examples of using lower-level entrypoints, see
`test\_lowlevel.py <https://github.com/hughperkins/DeepCL/blob/master/python/test_lowlevel.py>`__:

-  creating layers directly
-  running epochs and forward/backprop directly

Notes on how the wrapper works
==============================

-  `cDeepCL.pxd <https://github.com/hughperkins/DeepCL/blob/master/python/cDeepCL.pxd>`__
   contains the definitions of the underlying DeepCL c++ libraries
   classes
-  `PyDeepCL.pyx <https://github.com/hughperkins/DeepCL/blob/master/python/PyDeepCL.pyx>`__
   contains Cython wrapper classes around the underlying c++ classes
-  `setup.py <https://github.com/hughperkins/DeepCL/blob/master/python/setup.py>`__
   is a setup file for compiling the ``PyDeepCL.pyx`` Cython file

To install from pip
===================

.. code:: bash

    pip install DeepCL 

-  related pypi page: https://pypi.python.org/pypi/DeepCL

To build directly
=================

Pre-requisites:
---------------

Compilers
~~~~~~~~~

-  on Windows:
-  Python 2.7 build: need `Visual Studio 2008 for Python
   2.7 <http://www.microsoft.com/en-us/download/details.aspx?id=44266>`__
   from Microsoft
-  Python 3.4 build: need Visual Studio 2010, eg `Visual C++ 2010
   Express <https://www.visualstudio.com/downloads/download-visual-studio-vs#DownloadFamilies_4>`__

Python packages
~~~~~~~~~~~~~~~

-  Need the following python packages installed, eg via ``pip install``:
-  cython

To build:
---------

.. code:: bash

    cd python
    python setup.py build_ext -i

Considerations for Python wrapper developers
============================================

-  By default, cython disables ctrl-c, so need to handle this ourselves
   somehow, eg see ``NetLearner.learn`` for an example
-  To handle ctrl-c, we need to use ``nogil``, which means we cant use
   the ``except +`` syntax, I think, hence need to handle this ourselves
   too :-) see again \`Netlearner.learn for an example
