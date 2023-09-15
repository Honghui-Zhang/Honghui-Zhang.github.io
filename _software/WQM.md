---
title: "Installation of VASP"
excerpt: "The Vienna Ab initio Simulation Package (VASP) is a computer program for atomic scale materials modelling, e.g. electronic structure calculations and quantum-mechanical molecular dynamics, from first principles."
collection: software
---
<img src='https://honghui-alice.github.io/Honghui_Zhang.github.io/images/vasp.jpg' alt='Profile Image' height='400' width='400'><br/>

## Requirements
<pre>
Dependencies:
	intel, gcc, fftw, mpi
	
Suggests: 
    intel2019.5, gcc9.2.0, fftw3.3.8-intel-sigle-avx512-impi, mpi/openmpi3.1.4_gcc, HPC_kit
</pre>

## Installation

You can install the HPC_kit with:

```r
wget https://registrationcenter-download.intel.com/akdlm/IRC_NAS/0722521a-34b5-4c41-af3f-d5d14e88248d/l_HPCKit_p_2023.2.0.49440_offline.sh
chmod 777 l_HPCKit_p_2023.2.0.49440_offline.sh
./l_HPCKit_p_2023.2.0.49440_offline.sh
source ~/intel/oneapi/setvars.sh

```
now we can mpiifort

then inshall chemshell with: 

``` r
tar xvf vasp.5.4.4.tar.gz
cd vasp.5.4.4/
cp  ./arch/makefile.include.linux_intel  makefile.include
module load intel/2019.5 fftw/3.3.8-intel-single-avx512-impi gcc/9.2.0 mpi/openmpi/3.1.4_gcc
make 
export PATH=$PATH:~/soft/vasp.5.4.4/bin

```
## Test
``` r
tar xvf Oatom.tgz
cd Oatom/

```
run vasp with vasp_run.lsf:
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

module load fftw/3.3.8-intel-single-avx512-impi intel/2019.5 gcc/9.2.0 mpi/openmpi/3.1.4_gcc

vasp_std
```


## Citations
[1] G. Kresse and J. Hafner, Phys. Rev. B 47, 558 (1993); ibid. 49, 14251 (1994).

[2] G. Kresse and J. Furthmüller, Comput. Mat. Sci. 6, 15 (1996).

[3] G. Kresse and J. Furthmüller, Phys. Rev. B 54, 11169 (1996).