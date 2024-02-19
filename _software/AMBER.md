---
title: "Installation of AMBER"
excerpt: "Amber is the collective name for a suite of programs that allow users to carry out molecular dynamics simulations, particularly on biomolecules."
collection: software
---
<img src='https://honghui-zhang.github.io/images/amber.png' alt='Profile Image' height='400' width='400'><br/>

## MPI Edition Installation of AMBER20 Requirements
<pre>
Dependencies:
	fftw, gcc, mpi
	
Suggests: 
    fftw/3.3.8, gcc/9.2.0, mpi/openmpi/4.0.2_8.3.0gcc
</pre>

## Installation
You can install load the essential dependencies with:
```r
module load fftw/3.3.8 gcc/9.2.0 mpi/openmpi/4.0.2_8.3.0gcc

```

You can unzip the installation files:

```r
tar xvf AmberTools20.tar.bz2
tar xvf Amber20.tar.bz2
cd amber20_src
```
now we can set the AMBERHOME environment variable with:

```r
export AMBERHOME=/soft/amber20_src
```

then inshall Amber with: 

``` r
./configure gnu
source amber.sh
make install
make test
./configure -mpi gnu
source amber.sh
make install
make test
```
## Add environment variables to the bashrc file
``` r
export AMBERHOME=/soft/amber20_src
source /soft/amber20_src/amber.sh
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$AMBERHOME/lib
```

run Amber with AMBER_mpi.lsf:
``` r
#!/bin/bash 
# 
#BSUB -J MPIJob ### set the job Name 
#BSUB -n 20 ### ask for number of cores (default: 1) 
#BSUB –R “span[ptile=20]” ### ask for 4 cores per node 
#BSUB -W 10:00 ### set walltime limit: hh:mm
#BSUB -o stdout_%J.out ### Specify the output and error file. %J is the job-id 
#BSUB -e stderr_%J.err ### -o and -e mean append, -oo and -eo mean overwrite 

module load fftw/3.3.8 gcc/9.2.0 mpi/openmpi/4.0.2_8.3.0gcc

mpirun -np $LSB_DJOB_NUMPROC ~/soft/amber20_src/bin/sander.MPI -O -i min1.in -p complex.top -c complex.crd -ref complex.crd -o min1.out -r min1.rst
```

## GPU_MPI Edition Installation of AMBER20 Requirements
<pre>
Dependencies:
	fftw, gcc, intel, cuda, mpi
	
Suggests: 
    fftw/3.3.8, gcc/8.3.0, intel/2019.5, cuda/10.1, mpi/openmpi/4.0.5_8.3.0gcc
</pre>

## Installation
You can install load the essential dependencies with:
```r
module load fftw/3.3.8 gcc/8.3.0 intel/2019.5 cuda/10.1 mpi/openmpi/4.0.5_8.3.0gcc
```


then inshall Amber with: 

``` r
./configure -cuda -mpi gnu
source amber.sh
make install
make test
```

then run Amber with Amber_GPU.lsf:
``` r
#!/bin/bash 
# 
#BSUB -J Job ### set the job Name 
#BSUB -n 4
#BSUB -q q2080
#BSUB -R "span[ptile=4]"
#BSUB -gpu num=4
#BSUB -W 240:00 ### set walltime limit: hh:mm
#BSUB -o stdout_%J.out ### Specify the output and error file. %J is the job-id 
#BSUB -e stderr_%J.err ### -o and -e mean append, -oo and -eo mean overwrite 

export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$AMBERHOME/lib

export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH

module load fftw/3.3.8 gcc/8.3.0 intel/2019.5 cuda/10.1 mpi/openmpi/4.0.5_8.3.0gcc

~/soft/amber20_src/bin/pmemd.cuda.MPI -O -i md.in -p complex.top -c equil.rst -o md.out -r md.rst -x md.nc
``` 
## Citations
[1] D.A. Case, K. Belfon, I.Y. Ben-Shalom, S.R. Brozell, D.S. Cerutti, T.E. Cheatham, III, V.W.D. Cruzeiro, T.A. Darden, R.E. Duke, G. Giambasu, M.K. Gilson, H. Gohlke, A.W. Goetz,R Harris, S. Izadi, K. Kasavajhala, A. Kovalenko, R. Krasny, T. Kurtzman, T.S. Lee, S. LeGrand, P. Li, C. Lin, J. Liu, T. Luchko, R. Luo, V. Man, K.M. Merz, Y. Miao, O. Mikhailovskii, G. Monard, H. Nguyen, A. Onufriev, F. Pan, S. Pantano, R. Qi, D.R. Roe, A. Roitberg, C. Sagui, S. Schott-Verdugo, J. Shen, C.L. Simmerling, N. Skrynnikov, J. Smith, J. Swails, R.C. Walker, J. Wang, L. Wilson, R.M. Wolf, X. Wu, D.M. York and P.A. Kollman (2020), AMBER 2020, University of California, San Francisco.