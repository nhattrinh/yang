ModelDiff
=========

yang.ncdiff module has a class to compute diff of two versions of a model.

A common use case is having two folders of YANG files and comparing a model in
them.

create ModelCompiler objects
----------------------------

Given a folder that holds all YANG files of a device, an instance of
ModelCompiler can be instantiated:

.. code-block:: text

    >>> from yang.ncdiff import Model, ModelCompiler, ModelDiff
    >>> compiler1 = ModelCompiler('/version1/yang')
    ...
    >>> compiler2 = ModelCompiler('/version2/yang')
    ...
    >>>

create Model objects
------------------------

.. code-block:: text

    >>> model1 = compiler1.compile('Cisco-IOS-XE-native')
    ...
    >>> model2 = compiler2.compile('Cisco-IOS-XE-native')
    ...
    >>>

create ModelDiff objects
------------------------

Simply print out the ModelDiff object:

.. code-block:: text

    >>> diff = ModelDiff(model1, model2)
    >>> bool(diff)
    True
    >>> print(diff)
    module: Cisco-IOS-XE-native
        +--rw native
           +--rw hw-module
           |  +--rw switch*     deleted
           |  |  +--rw switch-number     deleted
           |  |  +--rw usbflash1         deleted
           |  |     +--rw security    deleted
           |  |        +--rw enable   deleted
           |  |           +--rw password?   deleted
           |  +--rw slot*       deleted
           |     +--rw name        deleted
           |     +--rw shutdown?   deleted
           +--rw parser
           |  +--rw view
           |     +--rw view-name-list*
           |     |  +--rw secret
           |     |     +--rw type?    modified
    ...
    >>>


.. sectionauthor:: Jonathan Yang <yuekyang@cisco.com>
