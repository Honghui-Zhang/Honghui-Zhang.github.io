---
title: "Installation of CP2K"
excerpt: "CP2K is a quantum chemistry and solid state physics software package that can perform atomistic simulations of solid state, liquid, molecular, periodic, material, crystal, and biological systems. "
collection: software
---
<img src='https://honghui-alice.github.io/Honghui_Zhang.github.io/images/CP2K.png' alt='Profile Image' height='350' width='350'><br/>

## Requirements
<pre>
Dependencies:
	fftw, intel, gcc, cuda, python
	
Suggests: 
    fftw3.3.8, inter2019.5, gcc8.3.0 cuda10.1 python3.7.5
</pre>

## Installation

``` r
tar xvf cp2k-2023.2.tar.bz2
cd cp2k-2022.1/
cd tools/toolchain/
module load fftw/3.3.8 intel/2019.5 gcc/8.3.0 cuda/10.1 python/3.7.5
./install_cp2k_toolchain.sh --with-libxsmm=install --with-openblas=no --with-fftw=system  --enable-cuda --gpu-ver=P100 --no-check-certificate
make -j 112 ARCH=local_cuda VERSION=sdbg test
tar xvf static_calculation.tgz 

```
There may be error in spglib installation
``` r
==================== Installing spglib ====================
ERROR: (./scripts/stage7/install_spglib.sh) failed to download https://github.com/atztogo/spglib/archive/v1.16.2.tar.gz

```
just download the spglib and put it in the folder: cp2k-2022.1/tools/toolchain/build

run CP2K with CP2K_run.lsf:
``` r
#
#!/bin/bash
#
#BSUB -J JOB
#BSUB -n 40 ### ask for number of cores (default: 1)
#BSUB –R “span[hosts=2]” ### ask for 1 cores per node
#BSUB -W 8:00 ### set walltimelimit: hh:mm
#BSUB -o stdout_%J.out### Specify the output and error file. %J is the job-id
#BSUB -e stderr_%J.err### -o and -e mean append, -ooand -eomean overwrite

module load fftw/3.3.8 intel/2019.5 gcc/8.3.0 python/3.7.5

 /share/home/grp-baichen/zhanghonghui/soft/cp2k-2022.1/exe/local/cp2k.sopt -o Si_bulk8.out Si_bulk8.inp &
```

## Citations
[1] Thomas D. K"uhne, Iannuzzi M, Del Ben M, Rybkin VV, Seewald P, Stein F, et al. CP2K: An electronic structure and molecular dynamics software package - Quickstep: Efficient and accurate electronic structure calculations. *The Journal of Chemical Physics*. 2020 May;152(19):194103. 