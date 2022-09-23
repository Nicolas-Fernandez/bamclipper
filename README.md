BAMClipper
==========
Remove gene-specific primer sequences from SAM/BAM alignments of PCR amplicons by soft-clipping


### Dependencies, as tested on 64-bit macOS Monterey v.12.3.1
* [SAMtools](http://www.htslib.org/download/) (at least version 1.3.1)
* [GNU Parallel](http://www.gnu.org/software/parallel/) (at least version 20130522)

### Usage
`bamclipper.sh` soft-clips gene-specific primers from BAM alignment file based on *genomic coordinates* of primer pairs in BEDPE format.

```shell
./bamclipper.sh -b _BAM_ -p _BEDPE_ [-n _NTHREAD_] [-s _SAMTOOLS_] [-g _GNUPARALLEL_] [-u _UPSTREAM_] [-d _DOWNSTREAM_] [-o _OUTPUT_]
```
Given a BAM file called **_NAME_.bam**, a new BAM file (**_NAME_.primerclipped.bam**) and its associated index (**_NAME_.primerclipped.bam.bai**) will be generated in the current working directory.

_Notes_: For the sake of performance and simplicity, soft-clipping is performed solely based on genomic coordinates without involving the underlying sequence. Reference sequence names and coordinates of BAM and BEDPE are assumed to be derived from identical reference sequences (e.g. hg19).

*Required arguments*
- **-b** _FILE_: indexed alignments BAM and BAI files
- **-p** _FILE_: primer pair locations in BEDPE file format
_http://bedtools.readthedocs.io/en/latest/content/general-usage.html#bedpe-format_

*Options*
- **-n** _INT_: number of threads for clipprimer.pl (the workhorse Perl script of BAMClipper) and samtools sort [1]
- **-s** _FILE_: path to samtools executable [samtools]
- **-g** _FILE_: path to gnu parallel executable [parallel]
- **-u** _INT_: number of nucleotide upstream to 5' most nucleotide of primer (in addition to 5' most nucleotide of primer) for assigning alignments to primers based on the alignment starting position. [1]
- **-d** _INT_: number of nucleotide downstream to 5' most nucleotide of primer (in addition to 5' most nucleotide of primer) for assigning alignments to primers based on the alignment starting position. [5]
- **-o** _DIR_: path to write output [current directory]


Citations
---------

Version 1.1.3 (Conda release)
-----------------------------
Nicolas FERNANDEZ NUNEZ - https://github.com/Nicolas-Fernandez - Research Institute for Development (IRD) - nicolas.fernandez@ird.fr


Version 1.1.2 (Output option)
-----------------------------
Charles VAN GOETHEM - https://github.com/Char-Al - Montpellier University Hospital (CHU) - charles.van.goethem@gmail.com


Version 1.0 to 1.1.1 (Original work)
------------------------------------
Tommy AU - https://github.com/tommyau - Hong Kong Genome Institute

Au CH, Ho DN, Kwong A, Chan TL and Ma ESK, 2017. [BAMClipper: removing primers from alignments to minimize false-negative mutations in amplicon next-generation sequencing](http://www.nature.com/articles/s41598-017-01703-6). _Scientific Reports_ 7:1567  (doi:10.1038/s41598-017-01703-6)

Fork from https://github.com/tommyau/bamclipper
