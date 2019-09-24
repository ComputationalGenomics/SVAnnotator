# SVAnnotator
SVannotator was developed to alleviate the cumbersome annotation process of structural variants (SV). It uses outputs from SV callers to transform SV events into a human-interpretable format such as “exon skipping.”

## Prerequisite

- python 3.7
- GTF file, which should be compatible with your SV file.  
  - [GRCh37 GTF](https://grch37.ensembl.org/info/data/ftp/index.html)
  - [GRCh38 GTF](https://useast.ensembl.org/info/data/ftp/index.html)
- COSMIC census gene  file or your choice of cancer genes in which genes are listed in the first column in a tab separated text file.
  - [COSMIC Cancer Census](https://cancer.sanger.ac.uk/census)
- cytogenetic band file
  - [GRCh37 ](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=2ahUKEwjT3Zy5oufkAhXSTd8KHVGrAz4QFjAAegQIARAB&url=http%3A%2F%2Fhgdownload.cse.ucsc.edu%2FgoldenPath%2Fhg19%2Fdatabase%2FcytoBand.txt.gz&usg=AOvVaw2QixLNOieNknVjoDtCNt9K)
  - [GRCh38 ](http://hgdownload.cse.ucsc.edu/goldenpath/hg38/database/cytoBand.txt.gz) 

## Installation

### Download SVAnnotator binary files

Depending on python in your system, select appropriate byte code compiled python files.

### Build database

You need GTF file, census gene file, and cytogenetic band files of your choice of genome assembly version to build an SVAnnotator database.

```
python SVAnnotator_create_DB_1.0.0.cpython-37.pyc <gtf> <census gene> <cytogenetic>
```

should generate SVAnnotator.db

## Usage

```
python SVAnnotator_1.0.0.cpython-37.pyc SVAnnotator.db <input file> <output file>
```

## Input

SVAnnotator uses tab separated text files with coordinates, strand orientations, and types of event as inputs. Headers must start with ‘#’ if any. Most SV callers provide with ranges rather than chromosomal position for break points; however, SVAnnotator cannot handle the range and users need to pick a position.  Also, it is important to remove false positives which originate from alignment issues in low complexity regions and other reasons.

1. Breakpoint 1 chromosome
2. Breakpoint 1 position
3. Breakpoint 2 chromosome
4. Breakpoint 2 position
5. Strand 1 orientation: + or -
6. Strand 2 orientation: + or -
7. SV type must be one of DEL, DUP, INV, or TRA

## Output

SVAnnotator analysis provides information on breakpoints with coordinates and cytogenetic band in an eXtensible Markup Language (XML) file. If a breakpoint falls in a transcript, information about whether it lies in an exonic or intronic region is shown. For fusions, 5 prime and 3 prime genes are identified. Likewise, for dysfunctional fusions, genes are displayed without order assignment. For exon skipping events, internal tandem duplications (ITDs), deletions, and deletion-insertion events, the information for each transcript is provided. More details are found in the XML schema in [SVAnnotator.xsd](https://github.com/ComputationalGenomics/SVAnnotator/blob/master/SVAnnotator.xsd).

## Test

A test [input file](https://github.com/ComputationalGenomics/SVAnnotator/blob/master/SVAnnotator_test.txt) and corresponding [output xml](https://github.com/ComputationalGenomics/SVAnnotator/blob/master/SVAnnotator_test_out.xml) are in the directory.

## Author

Takahiko Koyama tkoyama@us.ibm.com

## License

Please, refer to the [license](https://github.com/ComputationalGenomics/SVAnnotator/blob/master/license.txt) in the directory.

## Citing SVAnnotator

Currently, a paper is under submission. Once it gets published. This section will be updated.
