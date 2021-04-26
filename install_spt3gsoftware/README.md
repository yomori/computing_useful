These are the steps to install spt3g_software on a new computer

To be safe, undo all paths
1. Load gcc of your choice. If you are using the a module you can get the path using

```
conda env create -n 3g -f 3g_environment.yaml
```

```
export LIBRARY_PATH=""
export LD_LIBRARY_PATH=""
export PATH=/share/software/user/srcc/bin:/usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/users/$USER/bin
export CONDA_BUILD=1
conda activate 3g
```

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



