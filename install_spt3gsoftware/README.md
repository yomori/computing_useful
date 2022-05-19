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

3. Install the required packages:

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
