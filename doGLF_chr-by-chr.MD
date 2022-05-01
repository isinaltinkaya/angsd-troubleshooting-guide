#  Chromosome-by-chromosome Genotype Likelihood Estimation

If your analyses take up too much memory or if you want to speed it up, you can get genotype likelihoods per chromosomes in different jobs then merge afterwards.


## Example


### Main analysis in a loop

```
IN=${1}
for CHR in $(seq 1 22)
do
	angsd -bam ${IN} -ref ${REF} -out ${OUT} -sites ${SITES} -GL 2 -doCounts 1 -doMajorMinor 1 -doMaf 1 -doGlf 2 -r ${CHR}"
done
```

*  `-r ${CHR}`

We are using human chromosomes in the example above. Modify the `${CHR}` part to match with your species' chromosome IDs.



*  `-out ${OUT}`

Name your output files based on which chromosome was used in each loop. e.g. `-out output_chr1` will produce `output_chr1.beagle.gz`.


### After all the jobs are finished, merge the `beagle.gz` files

Copy chromosome 1 (the first chromosome in your list) as it is to get the header:

```
cp output_chr1.beagle.gz merged_output.beagle.gz
```

Continue adding the remaining chromosomes:

```
for CHR in `seq 2 22`
do
  gunzip -c output_chr${CHR}.beagle.gz | sed 1d | gzip -c
done >> merged_output.beagle.gz
```
