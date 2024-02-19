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
## GPU_MPI Edition Installation of AMBER20 Requirements
<pre>
Dependencies:
	fftw, gcc, cuda, mpi
	
Suggests: 
    fftw/3.3.8, gcc/8.3.0, cuda/10.1, mpi/openmpi/4.0.5_8.3.0gcc
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
## Citations
[1] D.A. Case, K. Belfon, I.Y. Ben-Shalom, S.R. Brozell, D.S. Cerutti, T.E. Cheatham, III, V.W.D. Cruzeiro, T.A. Darden, R.E. Duke, G. Giambasu, M.K. Gilson, H. Gohlke, A.W. Goetz,R Harris, S. Izadi, K. Kasavajhala, A. Kovalenko, R. Krasny, T. Kurtzman, T.S. Lee, S. LeGrand, P. Li, C. Lin, J. Liu, T. Luchko, R. Luo, V. Man, K.M. Merz, Y. Miao, O. Mikhailovskii, G. Monard, H. Nguyen, A. Onufriev, F. Pan, S. Pantano, R. Qi, D.R. Roe, A. Roitberg, C. Sagui, S. Schott-Verdugo, J. Shen, C.L. Simmerling, N. Skrynnikov, J. Smith, J. Swails, R.C. Walker, J. Wang, L. Wilson, R.M. Wolf, X. Wu, D.M. York and P.A. Kollman (2020), AMBER 2020, University of California, San Francisco.