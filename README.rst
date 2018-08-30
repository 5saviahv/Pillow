Pillow Wheel Builder
====================

This repository creates wheels for tagged versions of Pillow::

    git submodule init
    git submodule update Pillow
    git add Pillow
    cd Pillow
    git checkout <VERSION>
    cd ..
    git commit -m "Pillow -> <VERSION>" Pillow
    git push

.. image:: https://img.shields.io/travis/python-pillow/pillow-wheels/latest.svg
   :target: https://travis-ci.org/python-pillow/pillow-wheels
   :alt: Travis CI build status (wheels)

Archives
--------

https://github.com/python-pillow/pillow-depends contains archives for libraries
that will be built as part of the Pillow build.

In general, there is no need to put library archives there, because the
``multibuild`` scripts will download them from their respective URLs.

But, the build will look in that repository before downloading from the
URL, so if there is a library that often fails to download, or you think might
fail to download, then download it and add it to the git repository.

See the ``pre_build`` in ``config.sh`` and the ``fetch_unpack`` routine in
``multibuild/common_utils.sh`` for the logic, and the build recipes in
``multibuild/library_builders.sh`` for the filename to give to the downloaded
archive.

Dependencies
------------

NumPy
~~~~~

Check minimum NumPy versions to build against in ``.travis.yml`` file. Build against the earliest NumPy that Pillow is compatible with; see `forward, backward numpy compatibility <http://stackoverflow.com/questions/17709641/valueerror-numpy-dtype-has-the-wrong-size-try-recompiling/18369312#18369312>`_

Wheels
------

Wheels are uploaded to a `rackspace container <http://a365fff413fe338398b6-1c8a9b3114517dc5fe17b7c3f8c63a43.r19.cf2.rackcdn.com/>`_. Credentials for this container are encrypted to this specific repo in the ``.travis.yml`` file, so the upload won't work from another repository.

PyPI
~~~~

Download wheels from Rackspace::

    wget -m -A 'Pillow-<VERSION>*' \
    http://a365fff413fe338398b6-1c8a9b3114517dc5fe17b7c3f8c63a43.r19.cf2.rackcdn.com

Upload wheels to PyPI::

    cd a365fff413fe338398b6-1c8a9b3114517dc5fe17b7c3f8c63a43.r19.cf2.rackcdn.com
    twine upload Pillow-<VERSION>*