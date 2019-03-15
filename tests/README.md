To run tests for now, you have to build the parent docker and the child docker.
Alternatively you can use mundialis/grass-py3-pdal as parent

```
docker build -t grass-py3-pdal .
docker build -t grass-py3-pdal-test ./tests
```

For test development, run it:

```
docker run -it --rm --name grass-py3-pdal-test --entrypoint "/bin/bash" grass-py3-pdal-test
```
Or mount the GRASS GIS source code into the docker:
```
PATH_TO_GRASS_GIS_SRC=repos/grass-ci

docker run -it --rm --name grass-py3-pdal-test \
    -v $HOME/$PATH_TO_GRASS_GIS_SRC/lib/python/gunittest:/src/grass_build/dist.x86_64-pc-linux-gnu/etc/python/grass/gunittest/ \
    -v $HOME/$PATH_TO_GRASS_GIS_SRC/lib/python/gunittest:/src/grass_build/lib/python/gunittest/ \
    --entrypoint "/bin/bash" grass-py3-pdal-test

```

If you need to build the test docker often, add the test data from "https://grass.osgeo.org/sampledata/north_carolina/nc_spm_08_grass7.tar.gz" to your local checkout inside tests/tmp and incomment to use it in the Dockerfile:

```
# ADD https://grass.osgeo.org/sampledata/north_carolina/nc_spm_08_grass7.tar.gz /grassdata/tests/
COPY tmp/nc_spm_08_grass7.tar.gz /grassdata/tests/
```

run tests inside the docker with:
```
cd /src/grass_build/testsuite/examples
bash test_framework_GRASS_GIS_with_NC.sh test_framework_NC.conf
```

there is an experimental test list to use for testing tests in "https://github.com/mmacata/grass-ci/tree/test-list" (open PR https://github.com/GRASS-GIS/grass-ci/pull/4). If you use this as GRASS_GIS_SRC, you can run the same command and it will only run tests for the list you specify in tests/test_framework_NC.conf
