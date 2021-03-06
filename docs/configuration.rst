.. _configuration:

Configuration
=============

The only configuration you have to do is to build your request. ``find_agg`` works with a JSON header file enclosing your requirements. Please use the command-line help to find the embedded template (see :ref:`usage`).

``find_agg`` uses a combination of HTTP requests or XML paths to check if an aggregation exists. The aggregation URLs/paths are rebuilt following **ALL** requirements from your JSON file in a sense of **AND** conditions/logical operators with one element of each facets. Consequently, all fields in the JSON header file are required.


Build your request
******************

Edit your ``requirements.json`` file defining your requested experiments, ensembles and variables according to the `CMIP5 vocabulary <http://cmip-pcmdi.llnl.gov/cmip5/data_description.html>`_ and keeping the correct `JSON syntax <http://www.w3schools.com/json/json_syntax.asp>`_ (see template below):

.. code-block:: json

   {
      "variables":
         {
         "pr":  ["mon", "atmos", "Amon"],
         "tas": ["mon", "atmos", "Amon"]
         },
      "experiments": ["piControl", "1pctCO2", "rcp26", "rcp45", "rcp85"],
      "ensembles":   ["r1i1p1", "r2i1p1"]

   }

``variables`` declares the required variables with their `CMIP5 name <http://cmip-pcmdi.llnl.gov/cmip5/docs/cmip5_data_reference_syntax.pdf>`_ and
corresponding tuple ``["frequency", "realm", "CMOR table"]`` in that order. Requesting several frequencies
or `CMOR tables <https://pcmdi.github.io/cmor-site/>`_ for the same variable requires as much lines. See following example:

.. code-block:: json

   {
       "variables":
          {
          "tas": ["day", "atmos", "day"],
          "tas": ["mon", "atmos", "Amon"]
          }
   }

.. note::

   ``experiments`` lists the required experiments coma-separated.
   ``ensembles`` lists the required ensembles coma-separated.

.. warning::

   ``find_agg`` supports Unix wildcards only for ensembles/members: ``"ensembles": ["r[12]i1p1"]`` or ``"ensembles": ["*"]``.

.. warning::

   Those three JSON attributes (i.e., ``variables``, ``experiments`` and ``ensembles`` are mandatory and no other attributes are allowed.