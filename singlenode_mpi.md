```
export OMP_NUM_THREADS=8
HOSTS=$(scontrol show hostnames $SLURM_JOB_NODELIST | tr '\n' ,)
parallel --env OMP_NUM_THREADS,PATH,LD_LIBRARY_PATH,PYTHONPATH --joblog slurm-$SLURM_JOBID.log -j $SLURM_NTASKS_PER_NODE -S $HOSTS --wd $PWD "python yourcode.py {}" ::: {1..100}
```

The first line is optional, it just tells you how many core-per-job you want. <BR>
The second line returns all the host names that you have requested. <BR>
The third line will distribute the array of jobs onto the list of nodes using gnuparallel and wait until all the jobs are done.

To run this, you will have to request for more than one node for e.g.:
```
salloc -N24 --ntasks-per-node=4 --exclusive -C haswell -A mp107 --qos=interactive -t 04:00:00
```
NERSC interactive nodes have 32 cores on each node. the  ```--ntasks-per-node=4``` ensures that we are using all 32 cores (since 4x8=32, where 8 comes from ```OMP_NUM_THREADS=8```). This means that we are running 24x4=96 jobs with 8 cores each in parallel.
