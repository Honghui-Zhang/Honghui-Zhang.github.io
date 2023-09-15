---
title: "Installation of Orca"
excerpt: "ORCA is a general-purpose quantum chemistry program package that features virtually all modern electronic structure methods (density functional theory, many-body perturbation and coupled cluster theories, and multireference and semiempirical methods)."
collection: software
---
<img src='https://honghui-alice.github.io/Honghui_Zhang.github.io/images/orca.png' alt='Profile Image' height='500' width='500'><br/>

## Requirements
<pre>
Dependencies:
	gcc
	
Suggests: 
    gcc9.2.0
</pre>

## Installation

```r
tar xvf orca_5_0_4_linux_x86-64_shared_openmpi411.tar.xz

```

run orca with orca_run.lsf:

```r
#
#!/bin/bash
#
#BSUB -J JOB
#BSUB -n 40 ### ask for number of cores (default: 1)
#BSUB –R “span[hosts=2]” ### ask for 1 cores per node
#BSUB -W 8:00 ### set walltimelimit: hh:mm
#BSUB -o stdout_%J.out### Specify the output and error file. %J is the job-id
#BSUB -e stderr_%J.err### -o and -e mean append, -ooand -eomean overwrite

module load gcc/9.2.0
export LD_LIBRARY_PATH=~/soft/orca_5_0_4_linux_x86-64_shared_openmpi411:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/usr/mpi/gcc/openmpi-4.0.2a1/lib64/:$LD_LIBRARY_PATH



~/soft/orca_5_0_4_linux_x86-64_shared_openmpi411/orca test.inp > test.out

```


## Citations
[1] Neese, F. (2012) The ORCA program system, Wiley Interdiscip. Rev.: Comput. Mol. Sci., 2, 73-78.

[2] Neese, F. (2017) Software update: the ORCA program system, version 4.0, Wiley Interdiscip. Rev.: Comput. Mol. Sci., 8, e1327.