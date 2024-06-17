# readxAOD-script

To build Athena and run the scripts needed to run

```
git clone https://github.com/jackkraus/readxAOD-script.git;
mv readxAOD-script/package_filters.txt .;
lsetup "asetup 25.0.8,Athena" ; 
mkdir athena-25.0.8 && cd athena-25.0.8; 
mv ../package_filters.txt .; 
git clone https://gitlab.cern.ch/akraus/athena.git; 
cd athena; 
git remote add upstream https://:@gitlab.cern.ch:8443/atlas/athena.git ;
git fetch --all;
git checkout jacks-test-branch
cd ..;
```

then run the build scripts
```
mkdir build && cd build ;
cmake -DATLAS_PACKAGE_FILTER_FILE=../package_filters.txt ../athena/Projects/WorkDir >& cmakelog;
make -j >& makelog;
```
don't forget to source:
```
source x86_64-el9-gcc13-opt/setup.sh;
```


**Navigate to a directory to run the following scripts:**

```
mkdir ../run && cd ../run;
```


Run the write script
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Write >& JacksWriteAlgo_log.txt;
```
then run the read script: 
```
python -m AthenaPoolExampleAlgorithms.AthenaPoolExample_Read  >& JacksReadAlgo_log.txt;
```
