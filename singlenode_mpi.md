export OMP_NUM_THREADS=8
HOSTS=$(scontrol show hostnames $SLURM_JOB_NODELIST | tr '\n' ,)
parallel --env OMP_NUM_THREADS,PATH,LD_LIBRARY_PATH,PYTHONPATH --joblog slurm-$SLURM_JOBID.log -j $SLURM_NTASKS_PER_NODE -S $HOSTS --wd $PWD "python yourcode.py {}" ::: {1..100}


