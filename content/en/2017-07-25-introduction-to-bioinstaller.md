---
title: "BioInstaller | Introduction to BioInstaller"
author: "Jianfeng Li"
date: "2017-07-25"
output: rmarkdown::html_vignette
slug: introduction-to-bioinstaller
categories:
  - Computer skill
tags:
  - R
  - r-package
  - softwares
  - databases
  - downloader
  - installer

vignette: >
  %\VignetteIndexEntry{Introduction to BioInstaller}
  %\VignetteEngine{knitr::rmarkdown}
  \usepackage[utf8]{inputenc}
---



## Introduction

BioInstaller is a downloader and installer of bio-softwares and bio-databases. The inspiration for this project comes from various types of convenient package manager, such as [pip](https://pypi.python.org/pypi/pip) for Python package, `install.packages` for R package, biocLite for [Bioconductor](http://www.bioconductor.org) R package, etc.

**Why we do not have an integrated bioinformatics database and software package manager?**

In fact, there are already some tools can complete part of the work:

[Conda](https://conda.io/docs/intro.html) and [BioConda](http://bioconda.github.io) have done a lot of work and we can use them to conveniently install some of bioinformatics softwares. But there are still many problems with these package managers, such as version updating not timely, incompatible to some precompiled programs, little support for the database and other non-software files.

[docker](https://www.docker.com/) is another kind very promising tool to complete the migration of the analytical environment. But the root authority is required that it's difficult for you to always get root privileges.

Futhermore, learning how to install and compile bioinformatics softwares is still necessary, because these 'unpleasant' experience will help you to improve the ability to debug and modify programs.

As for me, when starting some NGS analysis work in a new computer or operating system, I have to spend much time and energy to
establish a complete set of softwares and dependent files and set the corresponding configuration file.

BioInstaller can help us to download, install and manage a variety of bioinformatics tools and databases more easily and systematically.

What's more, BioInstaller provides a different way to download and install your files, softwares and databases for others, more detail can be found in another vignette [Examples of Templet Configuration File](https://CRAN.R-project.org/package=BioInstaller/vignettes/write_configuration_file.html).

**Feature**:

- Extendible
- Craw the source code and version information from the original site
- One step installation or download softwares and databases (Partial dependence supported)

## Core function in BioInstaller


```r
library(BioInstaller)

# Show all avaliable softwares/dependece in default
# inst/extdata/github.toml and inst/extdata/nongithub.toml
install.bioinfo(show.all.names = TRUE)
#>   [1] "abyss"                 "asap"                 
#>   [3] "backspin"              "bamtools"             
#>   [5] "bamutil"               "bcftools"             
#>   [7] "bearscc"               "bedtools"             
#>   [9] "bowtie"                "bowtie2"              
#>  [11] "breakdancer"           "brie"                 
#>  [13] "bwa"                   "cnvkit"               
#>  [15] "cnvnator"              "delly"                
#>  [17] "fastx_toolkit"         "freebayes"            
#>  [19] "fsclvm"                "github_demo"          
#>  [21] "hisat2"                "htseq"                
#>  [23] "igraph"                "isop"                 
#>  [25] "jvarkit"               "libgtextutils"        
#>  [27] "lofreq"                "macs"                 
#>  [29] "mdseq"                 "mimosca"              
#>  [31] "oases"                 "oncotator"            
#>  [33] "outrigger"             "picard"               
#>  [35] "pindel"                "pxz"                  
#>  [37] "raceid"                "rca"                  
#>  [39] "rum"                   "samtools_old"         
#>  [41] "sclvm"                 "scnorm"               
#>  [43] "seqtk"                 "seurat"               
#>  [45] "singlesplice"          "sleuth"               
#>  [47] "somaticsniper"         "sparsehash"           
#>  [49] "speedseq"              "star"                 
#>  [51] "tmap"                  "tophat2"              
#>  [53] "tracer"                "trinityrnaseq"        
#>  [55] "varscan2"              "vcflib"               
#>  [57] "vcftools"              "vep"                  
#>  [59] "zifa"                  "annovar"              
#>  [61] "armadillo"             "bcl2fastq2"           
#>  [63] "blat"                  "bzip2"                
#>  [65] "cesa"                  "cnvnator_samtools"    
#>  [67] "curl"                  "demo_2"               
#>  [69] "edena"                 "ensemble_grch37_reffa"
#>  [71] "ensemble_grch38_reffa" "fastqc"               
#>  [73] "fatotwobit"            "fusioncatcher"        
#>  [75] "fusioncatcher_reffa"   "gatk"                 
#>  [77] "gatk_bundle"           "gmap"                 
#>  [79] "hisat2_reffa"          "htslib"               
#>  [81] "imagej"                "liftover"             
#>  [83] "lzo"                   "lzop"                 
#>  [85] "mapsplice2"            "miniconda2"           
#>  [87] "miniconda3"            "mutect"               
#>  [89] "novoalign"             "pcre"                 
#>  [91] "pigz"                  "prinseq"              
#>  [93] "r"                     "reditools"            
#>  [95] "root"                  "samstat"              
#>  [97] "samtools"              "snpeff"               
#>  [99] "solexaqa"              "sqlite"               
#> [101] "sratools"              "ssaha2"               
#> [103] "svtoolkit"             "tvc"                  
#> [105] "ucsc_reffa"            "ucsc_utils"           
#> [107] "velvet"                "xz"                   
#> [109] "zlib"

# Fetching versions of softwares
install.bioinfo("samtools", show.all.versions = TRUE)
#> INFO [2017-07-25 12:00:07] Fetching samtools versions....
#>  [1] "1.5"        "1.4.1"      "1.4"        "1.3.1"     
#>  [5] "1.3"        "1.2"        "1.1"        "1.0"       
#>  [9] "0.2.0-rc12" "0.2.0-rc11" "0.2.0-rc10" "0.2.0-rc9" 
#> [13] "0.2.0-rc8"  "0.2.0-rc7"  "0.2.0-rc6"  "0.2.0-rc5" 
#> [17] "0.2.0-rc4"  "0.2.0-rc3"  "0.2.0-rc2"  "0.2.0-rc1" 
#> [21] "0.1.20"     "0.1.19"     "0.1.18"     "0.1.17"    
#> [25] "0.1.16"     "0.1.15"     "0.1.14"     "0.1.13"    
#> [29] "0.1.12"     "master"

# Install 'demo' with debug infomation
download.dir <- sprintf("%s/demo_2", tempdir())
install.bioinfo("demo", download.dir = download.dir, verbose = TRUE)
#> INFO [2017-07-25 12:00:08] Debug:name:demo
#> INFO [2017-07-25 12:00:08] Debug:destdir:
#> INFO [2017-07-25 12:00:08] Debug:db:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/softwares_db_demo.yaml
#> INFO [2017-07-25 12:00:08] Debug:github.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/github.toml
#> INFO [2017-07-25 12:00:08] Debug:nongithub.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/nongithub.toml
#> INFO [2017-07-25 12:00:08] Fetching demo versions....
#> INFO [2017-07-25 12:00:08] Install versions:GRCh37
#> INFO [2017-07-25 12:00:08] Now start to install demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_2.
#> INFO [2017-07-25 12:00:08] Running before install steps.
#> INFO [2017-07-25 12:00:08] Now start to download demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_2.
#> INFO [2017-07-25 12:00:09] Running install steps.
#> INFO [2017-07-25 12:00:09] Running after install successful steps.
#> INFO [2017-07-25 12:00:09] Running CMD:echo 'successful!'
#> INFO [2017-07-25 12:00:09] Running change.info for demo and be saved to D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/softwares_db_demo.yaml
#> INFO [2017-07-25 12:00:09] Debug:Install by Github configuration file: 
#> INFO [2017-07-25 12:00:09] Debug:Install by Non Github configuration file: demo
#> INFO [2017-07-25 12:00:09] Installed successful list: demo
#> $fail.list
#> [1] ""
#> 
#> $success.list
#> [1] "demo"

# Download demo source code
download.dir <- sprintf("%s/demo_3", tempdir())
install.bioinfo("demo", download.dir = download.dir, download.only = TRUE, 
  verbose = TRUE)
#> INFO [2017-07-25 12:00:09] Debug:name:demo
#> INFO [2017-07-25 12:00:09] Debug:destdir:
#> INFO [2017-07-25 12:00:09] Debug:db:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/softwares_db_demo.yaml
#> INFO [2017-07-25 12:00:09] Debug:github.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/github.toml
#> INFO [2017-07-25 12:00:09] Debug:nongithub.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/nongithub.toml
#> INFO [2017-07-25 12:00:09] Fetching demo versions....
#> INFO [2017-07-25 12:00:09] Install versions:GRCh37
#> INFO [2017-07-25 12:00:09] Now start to download demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_3.
#> INFO [2017-07-25 12:00:10] demo be downloaded in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_3 successful
#> [1] TRUE

# Set download.dir rrr destdir (destdir like /usr/local
# including bin, lib, include and others), destdir will work
# if install step {{destdir}} be used
download.dir <- sprintf("%s/demo_source", tempdir())
destdir <- sprintf("%s/demo", tempdir())
install.bioinfo("demo", download.dir = download.dir, destdir = destdir)
#> INFO [2017-07-25 12:00:10] Debug:name:demo
#> INFO [2017-07-25 12:00:10] Debug:destdir:C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E/demo
#> INFO [2017-07-25 12:00:10] Debug:db:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/softwares_db_demo.yaml
#> INFO [2017-07-25 12:00:10] Debug:github.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/github.toml
#> INFO [2017-07-25 12:00:10] Debug:nongithub.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/nongithub.toml
#> INFO [2017-07-25 12:00:10] Fetching demo versions....
#> INFO [2017-07-25 12:00:10] Install versions:GRCh37
#> INFO [2017-07-25 12:00:10] Now start to install demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo.
#> INFO [2017-07-25 12:00:10] Running before install steps.
#> INFO [2017-07-25 12:00:10] Now start to download demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_source.
#> INFO [2017-07-25 12:00:11] Running install steps.
#> INFO [2017-07-25 12:00:11] Running after install successful steps.
#> INFO [2017-07-25 12:00:11] Running CMD:echo 'successful!'
#> INFO [2017-07-25 12:00:11] Running change.info for demo and be saved to D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/softwares_db_demo.yaml
#> INFO [2017-07-25 12:00:11] Debug:Install by Github configuration file: 
#> INFO [2017-07-25 12:00:11] Debug:Install by Non Github configuration file: demo
#> INFO [2017-07-25 12:00:11] Installed successful list: demo
#> $fail.list
#> [1] ""
#> 
#> $success.list
#> [1] "demo"
```

## Storing useful information of databases and softwares

It takes time to find the routes of the softwares and databases after downloading and installing them, what’s worse is that you would be in really dire straits if you didn't save the useful information. 

Fortunately, version, path, source code path and update time will be saved in BIO_SOFWARES_DB_ACTIVE database, a YAML format file, if you did that work with BioInstaller.


```r
temp.db <- tempfile()
set.biosoftwares.db(temp.db)
is.biosoftwares.db.active(temp.db)
#> [1] TRUE

# Install 'demo' quite
download.dir <- sprintf("%s/demo_1", tempdir())
install.bioinfo("demo", download.dir = download.dir, verbose = FALSE)
#> $fail.list
#> [1] ""
#> 
#> $success.list
#> [1] "demo"
config <- get.info("demo")
config
#> $installed
#> [1] TRUE
#> 
#> $source.dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1"
#> 
#> $bin_dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1\\"
#> 
#> $executable_files
#> [1] ""
#> 
#> $install.dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1"
#> 
#> $version
#> [1] "GRCh37"
#> 
#> $last.update.time
#> [1] "2017-07-25 12:00:12"
#> 
#> attr(,"config")
#> [1] "demo"
#> attr(,"configtype")
#> [1] "yaml"
#> attr(,"file")
#> [1] "C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769"

config <- configr::read.config(temp.db)
config$demo$comments <- "This is a demo."
params <- list(config.dat = config, file.path = temp.db)
do.call(configr::write.config, params)
#> [1] TRUE
get.info("demo")
#> $installed
#> [1] "TRUE"
#> 
#> $source.dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1"
#> 
#> $bin_dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1\\"
#> 
#> $executable_files
#> [1] ""
#> 
#> $install.dir
#> [1] "C:\\Users\\ljf\\AppData\\Local\\Temp\\RtmpwR4H7E\\demo_1"
#> 
#> $version
#> [1] "GRCh37"
#> 
#> $last.update.time
#> [1] "2017-07-25 12:00:12"
#> 
#> $comments
#> [1] "This is a demo."
#> 
#> attr(,"config")
#> [1] "demo"
#> attr(,"configtype")
#> [1] "ini"
#> attr(,"file")
#> [1] "C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769"
del.info("demo")
#> [1] TRUE
```

## Install softwares from local source

BioInstaller can be used to install softwares from local source. To install github softwares, a cloned directory were required, and nongithub softwares can be installed from decompressed directory or a compressed archive.


```r
download.dir <- sprintf("%s/github_demo_local", tempdir())
install.bioinfo("github_demo", download.dir = download.dir, download.only = TRUE, 
  verbose = FALSE)
#> cloning into 'C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\github_demo_local'...
#> Receiving objects:  16% (1/6),    0 kb
#> Receiving objects:  33% (2/6),    0 kb
#> Receiving objects:  50% (3/6),    0 kb
#> Receiving objects:  66% (4/6),    0 kb
#> Receiving objects:  83% (5/6),    0 kb
#> Receiving objects: 100% (6/6),    0 kb, done.
#> [1] TRUE
install.bioinfo("github_demo", local.source = download.dir)
#> INFO [2017-07-25 12:00:14] Debug:name:github_demo
#> INFO [2017-07-25 12:00:14] Debug:destdir:
#> INFO [2017-07-25 12:00:14] Debug:db:C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769
#> INFO [2017-07-25 12:00:14] Debug:github.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/github.toml
#> INFO [2017-07-25 12:00:14] Debug:nongithub.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/nongithub.toml
#> INFO [2017-07-25 12:00:14] Fetching github_demo versions....
#> INFO [2017-07-25 12:00:15] Install versions:master
#> INFO [2017-07-25 12:00:15] Now start to install github_demo in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\github_demo.
#> INFO [2017-07-25 12:00:15] Running before install steps.
#> INFO [2017-07-25 12:00:15] Running install steps.
#> INFO [2017-07-25 12:00:15] Running after install successful steps.
#> INFO [2017-07-25 12:00:15] Running CMD:echo 'successful!'
#> INFO [2017-07-25 12:00:15] Running change.info for github_demo and be saved to C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769
#> INFO [2017-07-25 12:00:15] Debug:Install by Github configuration file: github_demo
#> INFO [2017-07-25 12:00:15] Debug:Install by Non Github configuration file: 
#> INFO [2017-07-25 12:00:15] Installed successful list: github_demo
#> $fail.list
#> [1] ""
#> 
#> $success.list
#> [1] "github_demo"

download.dir <- sprintf("%s/demo_local", tempdir())
install.bioinfo("demo_2", download.dir = download.dir, download.only = TRUE, 
  verbose = FALSE)
#> [1] TRUE
install.bioinfo("demo_2", download.dir = download.dir, local.source = sprintf("%s/GRCh37_MT_ensGene.txt.gz", 
  download.dir), decompress = TRUE)
#> INFO [2017-07-25 12:00:15] Debug:name:demo_2
#> INFO [2017-07-25 12:00:15] Debug:destdir:
#> INFO [2017-07-25 12:00:15] Debug:db:C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769
#> INFO [2017-07-25 12:00:15] Debug:github.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/github.toml
#> INFO [2017-07-25 12:00:15] Debug:nongithub.cfg:D:/Program_Files/R/R-3.4.1/library/BioInstaller/extdata/nongithub.toml
#> INFO [2017-07-25 12:00:15] Fetching demo_2 versions....
#> INFO [2017-07-25 12:00:15] Install versions:GRCh37
#> INFO [2017-07-25 12:00:15] Now start to install demo_2 in C:\Users\ljf\AppData\Local\Temp\RtmpwR4H7E\demo_local.
#> INFO [2017-07-25 12:00:15] Running before install steps.
#> INFO [2017-07-25 12:00:17] Running install steps.
#> INFO [2017-07-25 12:00:17] Running after install successful steps.
#> INFO [2017-07-25 12:00:17] Running CMD:echo 'successful!'
#> INFO [2017-07-25 12:00:17] Running change.info for demo_2 and be saved to C:/Users/ljf/AppData/Local/Temp/RtmpwR4H7E/file30d082a6a7769
#> INFO [2017-07-25 12:00:17] Debug:Install by Github configuration file: 
#> INFO [2017-07-25 12:00:17] Debug:Install by Non Github configuration file: demo_2
#> INFO [2017-07-25 12:00:17] Installed successful list: demo_2
#> $fail.list
#> [1] ""
#> 
#> $success.list
#> [1] "demo_2"
```

## Craw all versions of softwares or databases

BioInstaller provide a `craw.all.version` function to try download all avaliable URL files in nongithub part.


```r
download.dir <- sprintf("%s/craw_all_versions", tempdir())
craw.all.versions("demo", download.dir = download.dir)
#> INFO [2017-07-25 12:00:17] Fetching demo versions....
```
