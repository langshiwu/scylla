Scylla: An Intelligent Proxy Pool for Humanities™
==================================================

.. toctree::
    :maxdepth: 3
    :caption: Contents:
           modules

An intelligent proxy pool for humanities, only supports Python 3.6. Key
features:

-  Automatic proxy ip crawling and validation
-  Easy-to-use JSON API
-  Simple but beautiful web-based user interface (eg. geographical
   distribution of proxies)
-  Get started with only **1 command** minimally
-  Straightforward programmable API
-  Headless browser crawling

对于偏好中文的用户，请阅读 `中文文档`_\ 。For those who prefer to use Chinese, please read the `Chinese Documentation`_


Get started
-----------

Installation
""""""""""""

Install with Docker (highly recommended)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: shell

  docker run -d -p 8899:8899 -v /var/www/scylla:/var/www/scylla --name scylla wildcat/scylla:latest

Install directly via pip
^^^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

   pip install scylla
   scylla --help
   scylla # Run the cralwer and web server for JSON API

Install from source
^^^^^^^^^^^^^^^^^^^^^^^

.. code:: bash

   git clone https://github.com/imWildCat/scylla.git
   cd scylla

   pip install -r requirements.txt

   npm install # or yarn install
   make build-assets

   python -m scylla

Usage
"""""

This is an example of running a service locally (``localhost``), using port ``8899``.

Note: You might have to wait for 1 to 2 minutes in order to wait for the crawler get some proxy ips for the first time you use Scylla. 


JSON API
^^^^^^^^^^^^^^^^^^

Proxy IP List
~~~~~~~~~~~~~~~~~~~~

.. code:: shell

    http://localhost:8899/api/v1/proxies

Optional URL parameters:

========== ============= =================================================================
Parameters Default value Description
========== ============= =================================================================
page       ``1``         The page number
limit      ``20``        The number of proxies shown on each page
anonymous  ``any``       Show anonymous proxies or not. Possible values：``true``, only anonymous proxies; ``false``, only transparent proxies
countries  None          Filter proxies for specific countries. Format example: ``US``, or multi-countries: ``US,GB``
========== ============= =================================================================

Sample result:

.. code:: json

    {
        "proxies": [{
            "id": 3661,
            "ip": "118.114.77.47",
            "port": 8080,
            "is_valid": true,
            "created_at": 1527312259,
            "updated_at": 1527351023,
            "latency": 250.9789636882,
            "stability": 1.0,
            "is_anonymous": true,
            "location": "29.3416,104.7770",
            "organization": "AS4134 CHINANET-BACKBONE",
            "region": "Sichuan",
            "country": "CN",
            "city": "Zigong"
        }, {
            "id": 3657,
            "ip": "39.104.57.121",
            "port": 8080,
            "is_valid": true,
            "created_at": 1527312253,
            "updated_at": 1527351021,
            "latency": 189.1011954867,
            "stability": 0.2,
            "is_anonymous": true,
            "location": null,
            "organization": null,
            "region": null,
            "country": null,
            "city": null
        },
        ...
        ],
        "count": 1025,
        "per_page": 20,
        "page": 1,
        "total_page": 52
    }

System Statistics
~~~~~~~~~~~~~~~~~

.. code:: shell

    http://localhost:8899/api/v1/stats

Sample result:

.. code:: json

    {
        "median": 181.2566407083,
        "valid_count": 1780,
        "total_count": 9528,
        "mean": 174.3290085201
    }

Web UI
^^^^^^^^^^^^^^^^^^

Open ``http://localhost:8899`` in your browser to see the Web UI of this project.

Proxy IP List
~~~~~~~~~~~~~~~~~~~~

.. code:: shell

    http://localhost:8899/

Screenshot:

|screenshot-proxy-list|

Globally Geographical Distribution Map
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code:: shell

    http://localhost:8899/#/geo

Screenshot:

|screenshot-geo-distribution|

API Documentation
-----------------

Please read :ref:`modindex`. 

Roadmap
--------------

Please see `Projects`_.

Development and Contribution
----------------------------

.. code:: bash

   git clone https://github.com/imWildCat/scylla.git
   cd scylla

   pip install -r requirements.txt

   npm install # or `yarn install`
   make build-assets

Testing
-------

If you wish to run tests locally, the commands are shown below:

.. code:: bash

   pip install -r tests/requirements-test.txt
   pytest -n 15 tests

You are welcomed to add more test cases to this project, increasing the robustness of this project.

Naming of This Project
----------------------
`Scylla`_ is derived from the name of a group of memory chips in the American TV series, `Prison Break`_. This project was named after this American TV series to pay tribute to it.

License
-------

Apache License 2.0. For more details, please read the
`LICENSE`_ file.


.. _Projects: https://github.com/imWildCat/scylla/projects
.. _LICENSE: https://github.com/imWildCat/scylla/blob/master/LICENSE
.. _Travis CI: https://travis-ci.org/imWildCat/scylla
.. _Scylla: http://prisonbreak.wikia.com/wiki/Scylla
.. _Prison Break: https://en.wikipedia.org/wiki/Prison_Break
.. _中文文档: https://scylla.wildcat.io/zh/latest/
.. _Chinese Documentation: https://scylla.wildcat.io/zh/latest/

.. |screenshot-geo-distribution| image:: https://user-images.githubusercontent.com/2396817/40578442-13a8491c-610c-11e8-8340-50097f29fdad.png
.. |screenshot-proxy-list| image:: https://user-images.githubusercontent.com/2396817/40578443-13bcbbd6-610c-11e8-85d5-1a11b66bf5d4.png


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
