Welcome to ngspyce's documentation!
===================================

.. toctree::
    :maxdepth: 2
    :caption: Contents:

Introduction
============

This is a library that allows Python applications to talk to
`Ngspice <http://ngspice.sourceforge.net/>`_, an engine for simulating electronic
circuits. Currently it supports sending commands to the engine and reading the
results into numpy arrays, for plotting and analysis. Future goals include
voltage and current sources defined by Python functions, and the possibility of
stepping through a simulation in order to inspect results and modify the
circuit mid-run.

Getting libngspice
==================

This library requires ``libngspice``.

On **Linux**, this means you have to download the
`source package for ngspice <http://ngspice.sourceforge.net/download.html>`_
and compile it like this: ::

    ./configure --with-ngshared
    make
    sudo make install

On **OSX**, ``libngspice`` can be installed with brew. Note that the ngspice
package does not supply the required shared libraries.

On **Windows**, ``ngspyce`` currently assumes that ``ngspice.dll`` is installed in
``C:\Spice\bin_dll`` (32-bit Python) or ``C:\Spice64\bin_dll`` (64-bit Python).
Go to `Ngspice Download <http://ngspice.sourceforge.net/download.html>`_ and
choose one of the packages (such as ``ngspice-26plus-scope-inpcom-6-64.7z``)
that contains ``ngspice.dll``, and extract it to ``C:\``.

Basic Usage
===========

>>> import ngspyce as ns

Load a circuit:

>>> ns.circ('''
... v1 b 0 dc 3
... r1 b a 1k
... r2 a 0 2k''')

Run analyses

>>> ns.operating_point()
{'v1#branch': array([-0.001]), 'a': array([ 2.]), 'b': array([ 3.])}
>>> ns.save('a')
>>> ns.dc('v1', 3, 9, 3)
{'a': array([ 2.,  4.,  6.]), 'v-sweep': array([ 3.,  6.,  9.]), 'v1': array([3, 6, 9])}

Making netlists
===============

One fast way to produce SPICE netlists is to draw the schematic with
`GSchem <http://www.geda-project.org/>`_ and then export a netlist with

    gnetlist -g spice-sdb schematic.sch -o netlist.net


Command reference
=================

For details on simulation commands, check out the
`Ngspice manual <http://ngspice.sourceforge.net/docs/ngspice-manual.pdf>`_.

Circuit loading and modification
################################
.. autofunction:: ngspyce.circ
.. autofunction:: ngspyce.source
.. autofunction:: ngspyce.alter_model
.. autofunction:: ngspyce.alter

Analyses
########
.. autofunction:: ngspyce.ac
.. autofunction:: ngspyce.dc
.. autofunction:: ngspyce.operating_point

Retrieving results
##################
.. autofunction:: ngspyce.vectors
.. autofunction:: ngspyce.save
.. autofunction:: ngspyce.plots
.. autofunction:: ngspyce.vector
.. autofunction:: ngspyce.vector_names
.. autofunction:: ngspyce.destroy

Circuit information
###################
.. autofunction:: ngspyce.model_parameters
.. autofunction:: ngspyce.device_state

Sending arbitrary commands
##########################
.. autofunction:: ngspyce.cmd

Engine information
##################
.. autofunction:: ngspyce.xspice_enabled

Utility functions
#################
.. autofunction:: ngspyce.decibel
.. autofunction:: ngspyce.linear_sweep

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
