---
title: "Installation of Chemshell"
excerpt: "ChemShell is a script-based chemistry code focusing on hybrid QM/MM calculations with support for standard quantum chemical or force field calculations."
collection: software
---
<img src='https://honghui-zhang.github.io/images/chemshell.png' alt='Profile Image' height='400' width='400'><br/>

## Requirements
<pre>
Dependencies:
	tcl, mpiifort, mpich
	
Suggests: 
    tcl8.5.11, HPC_kit, mpich3.3.2
</pre>

## Installation
You can install tcl with:
```r
tar xvf tcl8.6.13-src.tar.gz 
cd tcl8.6.13/unix
./configure --prefix=/path/tcl8.6.13
make
make install

```

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
tar -xvzf chemsh-3.7.0.tar.gz
cd chemshell-3.7.0/src/config
module load mpi/mpich/3.3.2
export CC=mpicc
export F77=mpifort
export F90=mpifort
export COMPILER_IS_GFORTRAN=1
export TCLROOT=/path/tcl8.5.11
export LIBTCL=/path/tcl8.5.11/lib/libtcl8.6.so
./configure --with-mpi
cd ..
make

```
## Test
``` r
cd examples/
./run_validation.tcsh
../scripts/chemsh -p 4 validate_buildbot.chm

```

## Citations
[1] ChemShell, a Computational Chemistry Shell, www.chemshell.org

[2] QUASI: A general purpose implementation of the QM/MM approach and its application to problems in catalysis, P. Sherwood, A. H. de Vries, M. F. Guest, G. Schreckenbach, C. R. A. Catlow, S. A. French, A. A. Sokol, S. T. Bromley, W. Thiel, A. J. Turner, S. Billeter, F. Terstegen, S. Thiel, J. Kendrick, S. C. Rogers, J. Casci, M. Watson, F. King, E. Karlsen, M. Sjøvoll, A. Fahmi, A. Schäfer, Ch. Lennartz, *J. Mol. Struct. (Theochem.)*, 2003, 632, 1.

[3] DL-FIND: an Open-Source Geometry Optimizer for Atomistic Simulations, J. Kästner, J. M. Carr, T. W. Keal, W. Thiel, A. Wander, P. Sherwood, *J. Phys. Chem. A*, 2009, 113, 11856.
Sharma, A., & Mehrotra, R. (2014). 