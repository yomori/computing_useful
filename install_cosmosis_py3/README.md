If you're on a Linux system CosmoSIS comes with a nice automatic installer.
The problem is that it is based on python2.7, which is phased out already.
Doing a manual installation can be extremely painful especially when the HPC uses the default compiler to install openmpi/mpich (since cosmosSIS requires std=c++14).

The easiest way to use CosmoSIS+ python3 is to install using conda.<BR>


1. First create a conda environment <BR>
```
conda env create -n <nameofyourenv> -f environment.yaml
```
where ```environment.yaml``` (included in this repo) is a list of packages needed, that I have compiled. ```<nameofyourenv>``` can be anything.
  
2. Activate your environment (and switching to the conda compilers instead of sys compiler)

```
export CONDA_BUILD=1
conda activate <nameofyourenv>
```

3. Move setup-my-cosmosis to the base cosmoSIS directory and edit the line
```
COSMOSIS_SRC_DIR=
```
and then source the setup file
```
source setup-my-cosmosis
```

4. 
```
make
```
