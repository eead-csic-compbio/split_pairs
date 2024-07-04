**split_pairs.pl** is a simple and efficient utility for pre-processing NGS sequence reads in  FASTQ and FASTA formats, suited particularly for the task of sorting pair end reads and  for modifying their headers with Perl-style regular expressions.

The arguments for the program, which can be run on Linux/MacOSX systems, are:

**USAGE INSTRUCTIONS**

<pre>
-h this message
-i input FASTA/FASTQ filename            (accepts GZIP compressed files)
-l output interleaved filename           (optional, read pairs are printed by default)
-1 output pair1 filename                 (optional, overrides -l)
-2 output pair2 filename                 (optional, overrides -l)
-s output singles filename               (optional, singles are discarded otherwise)
-p char separating pair identifiers      (optional, default: -p "/", as in HWUSI:4:1101:3600:19#ATCA/1 )
-R Perl regex to shorten headers         (optional, example: -R "(^.*?)#\w+?([12])" )
-S header substitution pattern           (optional, requires -R and must match -p, example: -S "\1/\2")
-H show first header and exit            (optional)
-B RAM buffer (Mb) while sorting         (optional, default: -B 1024M )
-T path for temporary files              (optional, default: -T /tmp )
-n do not sort input reads               (optional, reads are sorted with shell sort by default)
-z GZIP-compress outfiles with N threads (optional, requires -1 & -2 or -l, example: -z 8 )
</pre>

**split_pairs_bf** is a brute-force version of the utility, that can take full advantage of large
RAM buffers for sorting, thus being faster, at the cost of creating much larger temporary files. 
It supports these arguments:

<pre>
-h this message
-i input FASTA/FASTQ filename      (accepts GZIP compressed files)
-1 output pair1 filename
-2 output pair2 filename
-l output interleaved filename     (optional, overrides -1 and -2)
-s output singles filename         (optional, singles are discarded otherwise)
-R Perl regex to shorten headers   (optional, example: -R "(^.*?)#\w+?([12])" )
-S header substitution pattern     (optional, requires -R, example: -S "\1/\2" )
-p char separating pair numbers    (optional, default: -p "/" , as in HWUSI:4:1101:3600:1982#ATCACGA/1 )
-n do not sort input reads         (optional, by default reads are sorted with shell sort)
-H show first header and exit      (optional)
-L make one-line reads and exit    (optional, creates file actually used for sorting reads)
-B RAM buffer (Mb) while sorting   (optional, default: -B 1024M )
-T path for temporary files        (optional, default: -T /tmp )
</pre>

**EXAMPLES**

$ perl split_pairs.pl -i unsorted.fastq.gz -B 1G

$ perl split_pairs.pl -i sorted.fastq -n -l sorted.12.fq -R "(^.*?)#\w+?(/[12])" -S "\1/\2" 

$ perl split_pairs.pl -i SRR491411.fastq -R "(^SRR\d+\.\d+)\.([12])" -S "\1/\2"

$ perl split_pairs.pl -i sorted.fastq -n -1 reads1.fq -2 reads2.fq -s singles.fq -z 8

$ perl split_pairs.pl -i sorted1.9.fq.gz -p " "

**SOFTWARE DEPENDENCIES**

This software has a few dependencies which are required during compilation and run-time:

|name|description|package|
|----|-----------|-------|
|g++|C++ compiler|g++|
|lz|<zlib.h>|zlib|
|lpcrecpp|pcrecpp.h|libpcre++-dev|
|sort|terminal utility|should be installed on all systems|
|tr|terminal utility|should be installed on all systems|


On Ubuntu systems simply type: $ sudo apt-get install g++ zlib1g-dev libpcre++-dev

On RedHat/Fedora/CentOS* systems type: $ yum install yum install gcc-c++ zlib-devel pcre

**COMPILATION INSTRUCTIONS**

$ cd split_pairs_vX.Y
$ make

**CREDITS**

Bruno Contreras-Moreira, Carlos P Cantalapiedra, MaJesus Garcia Pereira, Ruben Sancho Cohen      
EEAD-CSIC 2013-16 <www.eead.csic.es/compbio>

This software is based on <http://lh3lh3.users.sourceforge.net/parsefastq.shtml> and relies 
on kseq.h by Attractive Chaos <attractor@live.co.uk> and [pigz](http://zlib.net/pigz).

**CITATION**

Contreras-Moreira B, Cantalapiedra CP, Garcia Pereira MJ, Sancho R. eead-csic-compbio/split_pairs. San Francisco: GitHub; 2016. Release v0.5. Available from: https://github.com/eead-csic-compbio/split_pairs

Or in BibTeX format:

    @misc{ContrerasMoreira2016,
      author = {Contreras-Moreira, B., Cantalapiedra, C.P., Garcia Pereira, M.J., Sancho, R.},
      title = {eead-csic-compbio/split_pairs},
      year = {2016},
      publisher = {GitHub},
      journal = {GitHub repository},
      howpublished = {\url{https://github.com/eead-csic-compbio/split_pairs}},
      release = {v0.5}
    }
