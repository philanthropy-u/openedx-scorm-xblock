`SCORM <https://en.wikipedia.org/wiki/Scorm>`__ XBlock for `Open edX <https://openedx.org>`__
=============================================================================================

This is an XBlock to display SCORM content within the Open edX LMS and Studio. It will save student state and report scores to the progress tab of the course.
Currently supports SCORM 1.2 and SCORM 2004 standard.

.. image:: https://github.com/overhangio/openedx-scorm-xblock/raw/master/screenshots/studio.png
    :alt: Studio view

.. image:: https://github.com/overhangio/openedx-scorm-xblock/raw/master/screenshots/lms-fullscreen.png
    :alt: Student fullscreen view

This XBlock was initially developed by `Raccoon Gang <https://raccoongang.com/>`__ and published as `edx_xblock_scorm <https://github.com/raccoongang/edx_xblock_scorm>`__. It was later improved, published on Pypi and relicensed as AGPLv3 thanks to the support of `Compliplus Ltd <https://compliplus.com/>`__.

This XBlock is not compatible with its `ancestor <https://github.com/raccoongang/edx_xblock_scorm>`__: older xblocks cannot be simply migrated to the newer one. However, this xblock can be installed next to the other one and run on the same platform for easier transition.

Installation
------------

This XBlock was designed to work out of the box with `Tutor <https://docs.tutor.overhang.io>`__ (Ironwood release). It comes bundled by default in the official Tutor releases, such that there is no need to install it manually.

    `pip install -e git+https://github.com/philanthropy-u/openedx-scorm-xblock.git@master#egg=openedx-scorm-xblock`

Usage
-----

In the Studio, go to the advanced settings of your course ("Settings" 🡒 "Advanced Settings"). In the "Advanced Module List" add "scorm". Then hit "Save changes".

Go back to your course content. In the "Add New Component" section, click "Advanced", and then "Scorm module". Click "Edit" on the newly-created module: this is where you will upload your content package. It should be a ``.zip`` file containing an ``imsmanifest.xml`` file at the root. The content of the package will be displayed in the Studio and the LMS after you click "Save".

Advanced configuration
----------------------

By default, SCORM modules will be accessible at "/scorm/" urls and static assets will be stored in "scorm" media folders -- either on S3 or in the local storage, depending on your platform configuration. To change this behaviour, modify the xblock-specific ``LOCATION`` setting::

    XBLOCK_SETTINGS["ScormXBlock"] = {
        "LOCATION": "alternatevalue",
        "SCORM_FILE_STORAGE_TYPE": "openedx.features.philu_utils.backend_storage.ScormXblockS3Storage"
    }
    
    
For setup on local machine don't use above configurations rather then add following settings in lms.envs.json and cms.envs.json::

    "XBLOCK_SETTINGS": {},
    "X_FRAME_OPTIONS": "SAMEORIGIN"

Development
-----------

Run unit tests with::

    $ NO_PREREQ_INSTALL=1 paver test_system -s lms -t openedxscorm

License
-------

This work is licensed under the terms of the `GNU Affero General Public License (AGPL) <https://github.com/overhangio/openedx-scorm-xblock/blob/master/LICENSE.txt>`_.
