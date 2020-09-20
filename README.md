# PRAWNS: Pan-genome representation of whole genomes tool

Given a collection of whole genomes for the isolates of a bacterial species or species complex (similar genomes), the tool generates an efficient pan-genome representation for the corresponding isolates. The input genomes could be draft assemblies or complete genomes. The generated pan-genome provides a concise list of structural variants identified across these isolates, which can then be used in a downstream analysis. In addition to the detection of structural variants, the pan-genome also locates the variants that are collocated across multiple isolates - such paired occurrences and the separation between the corresponding structural variants are also provided which can aide the downstream analysis.

### Dependencies
1. Python 3.5 or later
2. C++11 or later

### Installation:
```bash
git clone https://github.com/KiranJavkar/PRAWNS.git
cd PRAWNS
make
```

### Running the command:
```
python run_prawns.py input.csv
```
Where ```input.csv``` comprises of upto 3 columns: assembly_name, fasta_file_path, oriented_links_file_path (optional, needed if ```--use_oriented_links True```)

```
-bash-4.2$ python run_prawns.py -h
usage: run_prawns.py [-h] -i INPUT [-n [NCORES]] [-K [KMER_LEN]]
                     [-p [MIN_PERC]] [-l [USE_ORIENTED_LINKS]]
                     [-b [MIN_GROUP_BLOCKS]] [-M [MAX_METABLOCK_MISMATCH]]
                     [-s [MIN_BLOCK_SIZE]] [-R [MAX_PAIRING_RANGE]] [-m [MEM]]
                     [-g [GENOME_LEN]]

PRAWNS: Pan-genome representation of whole genomes tool

optional arguments:
  -h, --help            show this help message and exit
  -i INPUT, --input INPUT
                        Input csv file
  -n [NCORES], --ncores [NCORES]
                        Number of cores to be used (default: 8)
  -K [KMER_LEN], --kmer_len [KMER_LEN]
                        Length of kmers (default: 25)
  -p [MIN_PERC], --min_perc [MIN_PERC]
                        Minimum % of genomes a variant would be present in
                        (default: 5.0)
  -l [USE_ORIENTED_LINKS], --use_oriented_links [USE_ORIENTED_LINKS]
                        Use MetaCarvel oriented links; if True, 3rd column in
                        input csv should be path to oriented links of
                        corresponding assembly (default: False)
  -b [MIN_GROUP_BLOCKS], --min_group_blocks [MIN_GROUP_BLOCKS]
                        Minimum number of exact matching regions (blocks) that
                        can be grouped into metablocks across the genomes
                        (default: 3)
  -M [MAX_METABLOCK_MISMATCH], --max_metablock_mismatch [MAX_METABLOCK_MISMATCH]
                        Maximum number of mismatches permitted to allow merger
                        and extension of metablocks across the genomes
                        (default: 25)
  -s [MIN_BLOCK_SIZE], --min_block_size [MIN_BLOCK_SIZE]
                        Smallest size of a block that is to be retained as a
                        structural variant (default: 50)
  -R [MAX_PAIRING_RANGE], --max_pairing_range [MAX_PAIRING_RANGE]
                        Maximum number of bases between the structural
                        variants from a genome for paired analysis (default:
                        100)
  -m [MEM], --mem [MEM]
                        Upper limit for RAM memory usage. Can be in
                        mb/MB/gb/GB/tb/TB (case insensitive), default unit is
                        MB. (default: 36000MB)
  -g [GENOME_LEN], --genome_len [GENOME_LEN]
                        Average genome length. Can be in k/K/m/M/g/G (case
                        insensitive), default unit is M, i.e. 1x10^6 nt.
                        (default: 4M)
```

The oriented links can be obtained by running [MetaCarvel](https://github.com/marbl/MetaCarvel) with `--keep True`. In addition to this, we recommend using `--bsize` argument to have higher confidence for the oriented links obtained for the sequenced isolate under consideration.

### Description of the output files:
--TO BE UPDATED--
-- metablock_coords
-- metablock_presence_absence
-- similarly for block
-- pair_presence_absence
-- intrapair_separation

To get the exact fasta sequence of a variant from a particular genome, run the following command:
`./kmer_variant_coords_fasta_display.o <PRAWNS_results_dir>/all_assembly_filepaths <genome_number(0-indexed)> <start_coordinate(from the corresponding variant's csv file)> <end_coordinate>`

E.g.: `./kmer_variant_coords_fasta_display.o PRAWNS_results/all_assembly_filepaths.txt 0 2818695 2818729`

<!-- If you use PRAWNS for your work, please cite it: -->

NOTE: This tool is still under active development and may produce errors while running. Please report any error encountered as a github issue so that we can fix it during the development. For any questions, please email kjavkar@umd.edu
