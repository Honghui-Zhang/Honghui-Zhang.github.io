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
export PATH=$PATH:/soft/vmd-1.9.4a55/bin
```


