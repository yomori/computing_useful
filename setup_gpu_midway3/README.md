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
conda install -c "nvidia/label/cuda-11.8.0" cuda-nvcc
######python3 -m pip install nvidia-cudnn-cu11==8.6.0.163 tensorflow==2.12.*
```

Here don't do ```conda install cuda-nvcc``` because it will install the latest version of the package. You need the version that matches with the cudatoolkit that you have installed (in step 3.) as described in [https://github.com/google/jax/discussions/6843#discussioncomment-2721688](https://github.com/google/jax/discussions/6843#discussioncomment-3103782). You can check the version of cudatoolkit you have with ```conda list```

5. Install GPU-enabled Jax
```
pip install --upgrade "jax[cuda11_pip]" -f https://storage.googleapis.com/jax-releases/jax_cuda_releases.html
```

6. Install cudakit and tensorflow
```
python3 -m pip install nvidia-cudnn-cu11==8.6.0.163 tensorflow==2.12.*
```

7.
```
pip install --quiet git+https://github.com/DifferentiableUniverseInitiative/JaxPM.git
pip install --quiet optax tqdm hdf5plugin
pip --quiet install flax optax
pip install -U scikit-learn
```
