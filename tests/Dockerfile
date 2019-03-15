FROM aocd

ADD https://grass.osgeo.org/sampledata/north_carolina/nc_spm_08_grass7.tar.gz /grassdata/tests/
# COPY tmp/nc_spm_08_grass7.tar.gz /grassdata/tests/
WORKDIR /grassdata/tests/
RUN tar xfz nc_spm_08_grass7.tar.gz

# temporary hacks for tests
ADD tmp/core.py /src/grass_build/dist.x86_64-pc-linux-gnu/etc/python/grass/script/core.py
ADD tmp/reporters.py /src/grass_build/dist.x86_64-pc-linux-gnu/etc/python/grass/gunittest/reporters.py

# temporary hacks, see https://github.com/GRASS-GIS/grass-ci/pull/4
# ADD testlist/invoker.py /src/grass_build/dist.x86_64-pc-linux-gnu/etc/python/grass/gunittest/invoker.py
# ADD testlist/main.py /src/grass_build/dist.x86_64-pc-linux-gnu/etc/python/grass/gunittest/main.py
# ADD testlist/multirunner.py /src/grass_build/lib/python/gunittest/multirunner.py

ADD test_framework_NC.conf /src/grass_build/testsuite/examples/
ADD testlist/test_framework_GRASS_GIS_with_NC.sh /src/grass_build/testsuite/examples/test_framework_GRASS_GIS_with_NC.sh
ADD testlist/test.list /src/grass_build/testsuite/examples/

WORKDIR /src/grass_build/testsuite/examples
# RUN bash test_framework_GRASS_GIS_with_NC.sh test_framework_NC.conf
