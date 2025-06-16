---
title: "Installation of Other Ordinary Software"
excerpt: "This is used to record the installation of other ordinary software used in molecular simulations"
collection: software
---

## Installation of pymol
<pre>
Dependencies:
	PyMOL-2.5.8_appveyor647-Linux-x86_64-py39.tar.bz2
</pre>
```r
tar -jxf PyMOL-2.5.8_appveyor647-Linux-x86_64-py39.tar.bz2
export PATH=$PATH:/soft/pymol
export OMP_NUM_THREADS=32

```

## Installation of VMD
<pre>
Dependencies:
	vmd-1.9.4a55.bin.LINUXAMD64-CUDA102-OptiX650-OSPRay185.opengl.tar.gz
</pre>
```r
tar -xvf vmd-1.9.4a55.bin.LINUXAMD64-CUDA102-OptiX650-OSPRay185.opengl.tar.gz
cd vmd-1.9.4a55
./configure LINUXAMD64
cd src
```
then change the installation directory /usr/local/lib/vmd to /soft/lib/vmd
change the /usr/local/bin to soft/vmd/bin
```r
make install
export PATH=$PATH:/soft/vmd-1.9.4a55/bin
```
## Installation of Multiwfn
<pre>
Dependencies:
	Multiwfn_3.8_dev_bin_Linux.zip, Xbin.tgz, motif-2.3.4-1.x86_64_0.rpm
</pre>
```r
tar zxf Xbin.tgz
unzip Multiwfn_3.8_dev_bin_Linux.zip
rpm2cpio motif-2.3.4-1.x86_64_0.rpm | cpio -div
```
then change the src
```r
# For Memory (remove the the stack limit)
export OMP_STACKSIZE=200M
ulimit -s unlimited
 
#Multiwfn
export Multiwfnpath=/share/home/soft/Multiwfn_3.8_dev_bin_Linux
export PATH=$PATH:/share/home/soft/Multiwfn_3.8_dev_bin_Linux
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/share/home/soft/usr/lib64
```
then copy lib64 of Xbin to the lib64 of motif
chomod 777 Multiwfn

## Installation of molaris
<pre>
Dependencies:
	Chen_huge.tgz, molaris_chen.tgz
</pre>
```r
tar xvf Chen_huge.tgz
tar xvf molaris_chen.tgz

```
then substitude molaris_hpc9.15_huge with Chen
then create molaris_rc under soft file

```r
export MOLARIS_PATH=/soft/molaris
export PATH="$MOLARIS_PATH/bin:$PATH"
export LD_LIBRARY_PATH=/soft/molaris/lib
export AMINO_LIB=/soft/molaris/lib/amino98.lib
export PARM_LIB=/share/home/grp-hiraoh/honghuizhang/soft/molaris/lib/parm.lib
export EVB_LIB=/soft/molaris/lib/evb.lib
export SOLVENT_OPT=/soft/molaris/lib/solvent.opt
export OUT_DIR=.

```
then add the environment variable to bash_rpofile
```r
source /share/home/grp-hiraoh/honghuizhang/soft/molaris_rc
```

test with run.lsf
```r
#!/bin/bash
#
#BSUB -J JOB
#BSUB -R "span[hosts=1]"
#BSUB -W 8:00
#BSUB -o stdout_%J.out
#BSUB -e stderr_%J.err
source ~/.bash_profile

export LD_LIBRARY_PATH=g/soft/molaris/lib
module load intel/2019.5 mpi/intel/2019.5 gcc/8.3.0


~/soft/molaris/bin/molaris_hpc9.15_huge <convert.inp> convert.log

```
