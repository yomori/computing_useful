1. Create new conda environment:
```
conda create --prefix /project/chihway/yomori/envs/analysis-gpu
conda activate /project/chihway/yomori/envs/analysis-gpu
```
2. Install pip
```
conda install pip
```

3. Install cudakit and tensorflow
```
conda install -c conda-forge cudatoolkit=11.8.0
python3 -m pip install nvidia-cudnn-cu11==8.6.0.163 tensorflow==2.12.*
```
4. Following the instructions from tensorflow installation manual https://www.tensorflow.org/install/pip:
```
mkdir -p $CONDA_PREFIX/etc/conda/activate.d
echo 'CUDNN_PATH=$(dirname $(python -c "import nvidia.cudnn;print(nvidia.cudnn.__file__)"))' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
echo 'export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/:$CUDNN_PATH/lib' >> $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
source $CONDA_PREFIX/etc/conda/activate.d/env_vars.sh
```

5. Install GPU-enabled Jax
```
pip install --upgrade "jax[cuda11_pip]" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
```

6. Once you edit the LD_LIBRARY_PATH in step 4., your git will stop working for some reason (find solution later) so you will have to exit the environment to install other packages. Namely do:
```
conda deactivate
git clone https://github.com/DifferentiableUniverseInitiative/JaxPM
cd JaxPM
python setup.py install
```
