```
export OMP_NUM_THREADS=8
HOSTS=$(scontrol show hostnames $SLURM_JOB_NODELIST | tr '\n' ,)
parallel --env OMP_NUM_THREADS,PATH,LD_LIBRARY_PATH,PYTHONPATH --joblog slurm-$SLURM_JOBID.log -j $SLURM_NTASKS_PER_NODE -S $HOSTS --wd $PWD "python yourcode.py {}" ::: {1..100}
```

The first line is optional, it just tells you how many core-per-job you want. <BR>
The second line returns all the host names that you have requested. <BR>
The third line will distribute the array of jobs onto the list of nodes using gnuparallel and wait until all the jobs are done.
