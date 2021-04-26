These are the steps to install spt3g_software on a new computer

1. To be safe of any path conflicts, undo all paths
```
export PATH=/share/software/user/srcc/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/users/$USER/bin
```

2. Create a new conda environment
```
conda env create -n 3g -f 3g_environment.yaml
```

3.
```
export LIBRARY_PATH=""
export LD_LIBRARY_PATH=""
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



