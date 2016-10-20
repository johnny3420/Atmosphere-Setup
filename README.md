# Atmosphere-Setup

## Installation notes for Maloof-Biof v10

## All programs are the most update versions at time of creation

### start with image "Ubuntu 14.04.2 XFCE Base"

### General installs

```
apt-get update
apt-get upgrade

apt-get install python3-all --install-suggests
apt-get install python3-numpy python3-scipy
apt-get install python3-dev python-dev python-numpy python-scipy python-support
apt-get install python-pip python3-pip
apt-get install python-biopython python-biopython-doc python-biopython-sql
apt-get install muscle clustalw mafft emboss blast2 probcons
apt-get install bioperl
#note this installed lots of bioinf packages including bwa, bowtie, hmmer, miscule, mafft, tcoffee, and much more
apt-get install openmpi-bin libopenmpi-dev
apt-get install ncbi-blast+ ncbi-blast+-legacy
apt-get install mysql-client mysql-server #password = Bioinformatics
apt-get install eclipse
apt-get install libcurl4-openssl-dev #needed for bioconductor 
apt-get install libgl1-mesa-dev #for rgl
apt-get install libglu1-mesa-dev #for rgl
apt-get install libmysqlclient-dev #for R mysql
apt-get install git
```

### R (3.3.1)

```
echo 'deb https://cran.cnr.berkeley.edu/bin/linux/ubuntu trusty/' >> /etc/apt/sources.list
apt-get update
apt-get install r-base
apt-get install r-base-dev
```

#### Inside R

```
source("http://bioconductor.org/biocLite.R")
biocLite()
biocLite(c('dichromat', 'ggplot2', 'gtable', 'labeling', 'memoise', 'munsell', 'scales', 'AnnotationDbi', 'BSgenome', 'BayesPeak', 'BiasedUrn', 'Biobase', 'BiocInstaller', 'Biostrings', 'Category', 'DBI', 'DESeq', 'DynDoc', 'EBarrays', 'GO.db', 'GOstats', 'GSEABase', 'GenomicFeatures', 'GenomicRanges', 'IRanges', 'KEGG.db', 'KernSmooth', 'MASS', 'Matrix', 'RBGL', 'RColorBrewer', 'RCurl', 'RMySQL', 'RSQLite', 'RankProd', 'Rcpp', 'Rmpi', 'Rsamtools', 'ShortRead', 'TreeSim', 'VennDiagram', 'XML', 'affy', 'affyPLM', 'affyQCReport', 'affydata', 'affyio', 'annaffy', 'annotate', 'ape', 'arabidopsis.db0', 'ath1121501.db', 'baySeq', 'biomaRt', 'bitops', 'caTools', 'colorspace', 'digest', 'doMC', 'edgeR', 'fdrtool', 'foreach', 'foreign', 'gcrma', 'gee', 'geiger', 'genefilter', 'geneplotter', 'ggplot2', 'goseq',  'hgu95av2.db', 'hopach', 'hwriter', 'igraph', 'iterators', 'itertools', 'lattice', 'latticeExtra', 'limma', 'lme4', 'marray', 'mgcv', 'msm', 'multtest', 'mvtnorm', 'nlme', 'nnet', 'org.At.tair.db', 'ouch', 'phangorn', 'phylobase', 'plyr', 'pmc', 'preprocessCore', 'proto', 'qtl', 'quadprog', 'qvalue', 'reshape', 'reshape2', 'rpart', 'rtracklayer', 'seqLogo', 'seqinr', 'simpleaffy', 'snow', 'snowFT', 'snowfall', 'stringr', 'subplex', 'vsn', 'xtable', 'zlibbioc', 'manipulate'))

install.packages(c("genetics","igraph","lmerTest")) ### Mirror 44

install.packages(c("pvclust","gplots","cluster","LDheatmap","scatterplot3d"))

biocLite(c("igraph","WGCNA","lmerTest","Rsubread"))
biocLite("BiocUpgrade")
```

## Placing packages into /usr/Bio_Packages
### R Studio Server

```
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/rstudio-server-0.99.903-amd64.deb
sudo gdebi rstudio-server-0.99.903-amd64.deb
mv rstudio-server-0.99.903-amd64.deb /usr/local/src
```

### BWA
#### Remove outdated and put newest

```
sudo apt-get remove bwa
cd /usr/local/src
git clone https://github.com/lh3/bwa.git
cd bwa; make
cd /usr//local/bin
ln -s /usr/local/src/bwa/bwa
```

### Bowtie
#### Remove outdated and put newest

```
apt-get remove bowtie
cd /usr/local/src
wget https://downloads.sourceforge.net/project/bowtie-bio/bowtie/1.1.2/bowtie-1.1.2-linux-x86_64.zip
unzip bowtie-1.1.2-linux-x86_64.zip
cd /usr/local/bin
ln -sf ../src/bowtie-1.1.2/bowtie ./
```

### Bowtie2

```
cd /usr/local/src
wget https://downloads.sourceforge.net/project/bowtie-bio/bowtie2/2.2.9/bowtie2-2.2.9-linux-x86_64.zip
unzip bowtie2-2.2.9-linux-x86_64.zip
cd /usr/local/bin
cp -sf ../src/bowtie2-2.2.9/bowtie2* ./
```

### blat

```
cd /usr/local/src
wget https://users.soe.ucsc.edu/~kent/src/blatSrc35.zip
unzip blatSrc35.zip
cd blatSrc
nano inc/common.mk #Change BINDIR=${HOME}/bin/${MACHTYPE} to BINDIR=/usr/local/bin
MACHTYPE=x86_64
export MACHTYPE
make
```

### cufflinks

```

cd /usr/local/src
wget http://cole-trapnell-lab.github.io/cufflinks/assets/downloads/cufflinks-2.2.1.Linux_x86_64.tar.gz
tar -xvzf cufflinks-2.2.1.Linux_x86_64.tar.gz
cd /usr/local/bin
cp -sf ../src/cufflinks-2.2.1.Linux_x86_64/cuff* ./
cp -sf ../src/cufflinks-2.2.1.Linux_x86_64/g* ./
```

### fastQC

```
cd /usr/local/src
wget www.bioinformatics.babraham.ac.uk/projects/fastqc/fastqc_v0.11.5.zip
cd FastQC/
chmod 0755 fastqc
cd /usr/local/bin
cp -s ../src/FastQC/fastqc ./
```

### Update Java, some programs require 1.8

```
add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
#Setting/confirming Java 8 as default
sudo update-alternatives --config java ## select java-8
sudo update-alternatives --config javac ## select java-8
java -version
```

### GATK 3.6 
Download from http://www.broadinstitute.org/gatk/

```
cd /usr/local/src
mkdir GenomeAnalysisTK
mv ~/GenomeAnalysisTK-3.4-46.tar.bz2 /usr/local/src/GenomeAnalysisTK
cd GenomeAnalysisTK
bunzip2 GenomeAnalysisTK-3.6.tar.bz2
tar -xvf GenomeAnalysisTK-3.6.tar
cd /usr/local/bin
### created sh called GenomeAnalysisTK with chmod 755 
### allows GenomeAnalysisTK to be invoked without including "java -jar /path/to/GenomeAnalysisTK"
```

### IGV

```
cd /usr/local/src
wget data.broadinstitute.org/igv/projects/downloads/IGV_2.3.83.zip
