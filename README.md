# V8 + testthat crash

Setup, run this from within this repository so that the "package" gets mounted into the container:

```
docker pull wch1/r-debug
docker run -v $PWD:/src:ro -it --rm \
       --security-opt seccomp=unconfined \
       wch1/r-debug
apt-get update && apt-get install -y libv8-dev
RDcsan -e 'install.packages(c("testthat", "V8"))'
RDcsan -e 'testthat::test_local("/src")' # crash :(
```

See https://github.com/jeroen/V8/issues/128 for more information.
