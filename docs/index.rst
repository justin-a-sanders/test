======
HiCRep
======

HiCRep is a python implementation of the R package with the same name. It provides a tool for assessing the reproducibility of Hi-C datasets based on the algorithm published by `Yang et al. <https://pubmed.ncbi.nlm.nih.gov/28855260/>`_
In brief, data is first smoothed to reduce the effects of noise and bias and then stratified by contact distance to adjust for the distance dependency of Hi-C datasets. These strata are compared between samples to calculate the stratum-adjusted correlation coefficient (SCC). The SCC is a value between -1 and 1 and can be interpreted the same way you would a standard correlation. 


This implementation takes a pair of Hi-C data sets in Cooler format (.cool for single binsize or .mcool formultiple binsizes) and computes the HiCRep SCC scores for each pair of chromosomes between the two data sets. It can be run either as a command line tool of through a python API. 

Installation
============
To install hicrep you will need python version 3.7.6 or greater. You can check your current python version with:

.. code-block:: bash

   $ python3 --version

Additionally, hicrep has the following dependencies:

- `NumPy <https://numpy.org/>`_
- `SciPy <https://www.scipy.org/>`_
- `cooler <https://cooler.readthedocs.io/en/latest/datamodel.html>`_
- `pandas <https://pandas.pydata.org/>`_
- `h5py <https://www.h5py.org/>`_
- `statsmodels <https://www.statsmodels.org/stable/index.html>`_

We recommend using pip to install hicrep, which will install the package along with all of it's dependencies. 

.. code-block:: bash

   $ pip install hicrep

Once hicrep is installed, you can interact with it either through the command line or as a python module.

CLI Guide
=========

hicrep can be run from the command line with:

.. program:: hicrep
.. code-block:: shell

    hicrep cool1 cool2 outfile [OPTIONS] 

.. rubric:: Arguments

.. option:: cool1

    The first Hi-C contact matrix in .cool or .mcool format [required]

.. option:: cool2

    The second Hi-C contact matrix in .cool or .mcool format [required]

.. option:: outfile

    A path to an output file to write the SCC scores for each chromosome to [required]

.. rubric:: Options

.. option:: -h , --help

    See a list of expected arguments to hicrep

.. option:: --binsize <BINSIZE>

    The binsize you want to use from a .mcool file. Default is -1, meaning that the inputs are .cool files with a single precomputed binsize

.. option:: --h, <H>

    Used to set the size of the sliding 2D window used for smoothing the contact matrix. Size will be 1 + 2 * H bins.

.. option:: --dBPMax <DBPMAX>

    Only consider contacts at most this number of bp away from the diagonal. Defaults to -1, meaning the entire contact matrix is used. 

.. option:: --bDownSample

    When set, hicrep will down sample the input with more contact counts to the the same number of counts as the other input with less contact counts. If not set, the input matrices will be normalized by dividing the counts by their respective total number of contacts.


API 
====
