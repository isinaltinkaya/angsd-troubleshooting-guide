# ANGSD Troubleshooting Guide


### 1. Replicate the issue using the most recent version of ANGSD

```
git clone https://github.com/ANGSD/angsd/; cd angsd; make
```

This will build angsd using the htslib submodule.

After building it, you can use `realpath angsd` to obtain the realpath to the angsd executable.

```
$ realpath angsd
/home/example/path/angsd/angsd
```

Use this path to replace all angsd commands in your script to make sure you are using the correct version. If you are using any utilities make sure you use the fullpath for them, too.

For example, replace 

```
angsd -out out -doMajorMinor 1 -doMaf 3 -bam bam.filelist -GL 2
realSFS pop1.saf.idx pop2.saf.idx
```

with

```
/home/example/path/angsd/angsd -out out -doMajorMinor 1 -doMaf 3 -bam bam.filelist -GL 2
/home/example/path/angsd/misc/realSFS pop1.saf.idx pop2.saf.idx
```



