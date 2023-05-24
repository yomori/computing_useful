These instructions are specifically for crossover, where there is some strange interactions between the intel compiler and conda.

### 1. Get Miniconda (https://docs.conda.io/en/latest/miniconda.html)
    wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
    sh Miniconda3-latest-Linux-x86_64.sh
 when asked for where to save just make a directory e.g.:
    
    /lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3/miniconda
 
 Do you wish the installer to initialize Miniconda3 by running conda init? [yes|no]
 
    -> no
    
 This will give you some command to activate the base conda environment:
    
    eval "$(/lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3/miniconda/bin/conda shell.bash hook)" 

### 2. Create new environment and activate
    conda create --prefix ./envs/testenv
    conda activate /lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3/envs/testenv

### 3. Install python packages
    conda install -c conda-forge python numpy
    conda install -c conda-forge openmpi openmpi-mpicc openmpi-mpicxx openmpi-mpifort
    conda install -c conda-forge mpi4py
    python -m pip install cobaya --upgrade

### 4. Download and install Pypolychord 
    git clone https://github.com/PolyChord/PolyChordLite.git

#### Modify Make file

    add the -fallow-argument-mismatch to FFLAGS
    i.e. FFLAGS += -DMPI -fallow-argument-mismatch

#### Set environment variables
    export FC=mpifort
    export CC=mpicc
    export CXX=mpicxx
### Install 
    5. run python setup.py install 

### Test
    
Go on an interactive node with more than two tasks

    srun --pty -p SPT3G -A SPT3G -t 24:00:00 -n2 -c8 /bin/bash

Test MPI using the following command

    cd /lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3
    eval "$(/lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3/miniconda/bin/conda shell.bash hook)"
    source activate /lcrc/project/SPT3G/users/ac.yomori/scratch/testcobaya3/envs/testenv
    mpirun -n 2 python -c "from mpi4py import MPI, __version__; print(__version__ if MPI.COMM_WORLD.Get_rank() else '')"
    
This should print out the version of your MPI4py (something like 3.1.4). To test the actual sampling use: 

    mpirun -n 2 cobaya-run test.yaml -f (Metropolis Hasting sampler)
    mpirun -n 2 cobaya-run test_polychord.yaml -f (Polychord sampler)
   
or do:
 
    sbatch test.submit
    
