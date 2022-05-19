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




If you want to do a manual install
-----------------------------------------------------
1. Create a fresh conda environment
```
conda create --prefix {path_to_env}/{env_name}
```
You can check the list of environments you have installed using 
```
conda env list
```
which should list you names or paths to conda environements.

2. To activate the environment you just created, do:
```
conda activate {path_to_env}/{env_name}
```

3. Install the required packages
```
conda install -c conda-forge cxx-compiler c-compiler fortran-compiler scipy fftw gsl hdf5 libflac=1.3.1 cmake boost netcdf4 python=3.9
```

4. Move to the directory where you cloned spt3g_software and then do the standard installation:
```
cd spt3g_software
mkdir build
cd build
cmake ..
make
```
If it complains that it cannot make a safe link then cmake is probably searching for additional locations when it shouldnt be.
In that case just reset the path:
```
PATH=$(getconf PATH)
```
and then repeat.

5. Finally add a link so that python finds 3gsoftware
```
export PYTHON_PATH=$PYTHON_PATH:$DIR_SPT3GSOFTWARE
```
