These are the steps to install spt3g_software on a new computer

1. To be safe of any path conflicts, undo all paths
```
export PATH=/share/software/user/srcc/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/users/$USER/bin
export LIBRARY_PATH=""
export LD_LIBRARY_PATH=""
```

2. Create a new conda environment
```
conda env create -n 3g -f 3g_environment.yaml
```
where 3g_environment.yaml has a list of all the packages needed.

3. Activate the compiler inside conda environment instead of the system one.
```
export CONDA_BUILD=1
conda activate 3g
```

4. To safely complete the following step you may need to reserve a compute node because of memory requirements.
```
export DIR_SPT3GSOFTWARE=<whereever-you-intalled-software>
cd $DIR_SPT3GSOFTWARE
rm -rf build
mkdir build
cd build
cmake ..
make
export PYTHON_PATH=$PYTHON_PATH:$DIR_SPT3GSOFTWARE
```
The last step of make will take about 15 minutes




If you awant to start from scratch
-----------------------------------------------------
```
conda create -n spt3g_v2
```
Here don't do 
```
conda create -n spt3g_v2 python=3.7
```
because this will use the system gcc compiler to install python which will probbaly be an OLDER version of GLIBC. 
Instead, install the conda compilers FIRST, and then use those compilers to install python.
```
conda activate spt3g_v3
conda install -c anaconda gcc_linux-64
conda install -c anaconda gxx_linux-64
conda install -c anaconda gfortran_linux-64
conda deactivate
```
(typically its considered bad practice to mix -c anaconda and -c conda-forge but I've found that the anaconda version compilers are more up-to-date.)
then install everything else
```
export CONDA_BUILD=1
conda activate spt3g_v2
conda install -c conda-forge scipy
conda install -c conda-forge boost
conda install -c conda-forge cmake
conda install -c conda-forge fftw
conda install -c conda-forge gsl
conda install -c conda-forge hdf5
conda install -c conda-forge netcdf4
```

Finally add a link so that python finds 3gsoftware
```
export PYTHON_PATH=$PYTHON_PATH:$DIR_SPT3GSOFTWARE
```

It might be also useful to install ipython and notebook and nbextensions
```
conda install -c conda-forge ipython
conda install -c conda-forge notebook
conda install -c conda-forge jupyter_contrib_nbextensions
```
