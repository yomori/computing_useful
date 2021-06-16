Main steps
============================

If you're on a Linux system CosmoSIS comes with a nice automatic installer.
The problem is that it is based on python2.7, which is phased out already.
Doing a manual installation can be extremely painful especially when the HPC uses the default compiler to install openmpi/mpich (since cosmosSIS requires std=c++14).

The easiest way to use CosmoSIS+ python3 is to install using conda.<BR>

0. If you don't have conda on your computer you can get it from: <BR>
https://www.anaconda.com/products/individual <BR>
I'm personally a fan of intelpython since I find it to perform better for numerical computations (packaged as conda): <BR>  https://software.intel.com/content/www/us/en/develop/tools/distribution-for-python.html <BR>
  
See the "futher tips" section for a few extra points to improve usability.
  
1. First create a conda environment <BR>
```
conda env create -n <nameofyourenv> -f environment.yaml
```
where ```environment.yaml``` (included in this repo) is a list of packages needed, that I have compiled. ```<nameofyourenv>``` can be anything.
  
2. Activate your environment (and switching to the conda compilers instead of sys compiler). Without the first line, it will default to the default system compiler which is probably gcc 4.8.X and doesn't have std=c++14. 

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

  

Further tips
========================

Installing Anaconda
-----------------------
  
When installing Anaconda, after installation is complete, you will see a prompt saying:
```
Do you wish the installer to initialize Anaconda3
by running conda init? [yes|no]
```
it is recommended to say "no" here. This is because if you have another version of anaconda installed somewhere it will interfere.
Instead, you should make an alias that will activate the conda environment:
 
 ```
 alias ac='eval "$(/project/chihway/yomori/repo/anaconda3/bin/conda shell.YOUR_SHELL_NAME hook)"' 
 ```
  
 where YOUR_SHELL_NAME should be your shell name (bash/zsh etc.)
  
Writing a submit script
-----------------------

When you submit a job script, the first thing that need to happen isyou need to activate the conda environment.This can be achieved by:
```
eval "$(WHERE_YOU_INSTALLED_ANACAONDA/anaconda3/bin/conda shell.YOUR_SHELL_NAME hook)"
```
next you need you activate the specific conda environment. You can see the list of the conda environments listed by doing 
```
conda-env list
```
  
example1 (on midway3)
```
#!/bin/bash
#SBATCH -t 36:00:00
#SBATCH --ntasks=200
#SBATCH --cpus-per-task=1
#SBATCH --partition=caslake
#SBATCH --account=pi-chihway
#SBATCH --job-name=5x2_maglim

# load conda
eval "$(/project/chihway/yomori/repo/anaconda3/bin/conda shell.bash hook)"

# load specific envinment
conda activate cosmosis3
   
cd /project/chihway/yomori/repo/y3-6x2pt/cosmosis/simulated_analysis/5x2_linbias_maglim
  
source ../../start_current_cosmosis.sh
source ../setup_vars_6x2_maglim_nohighz.sh
export RUN_NAME=5x2_linbias_maglim_lcdm_nohighz
export DEMODEL=lcdm
  
srun -n 200 cosmosis --mpi params_5x2_linbias_maglim.ini -p runtime.sampler='multinest'
```
