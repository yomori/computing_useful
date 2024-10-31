conda create -n tf-gpu tensorflow-gpu
conda activate tf-gpu
pip install cosmopower --no-deps
pip install tqdm --no-deps
conda install  -c conda-forge scikit-learn
pip install tensorflow_probability --no-deps
pip install tf_keras --no-deps
pip install decorator --no-deps 
pip install dm-tree --no-deps
pip install cloudpickle --no-deps
conda install nvidia::cuda-compiler
export XLA_FLAGS=--xla_gpu_cuda_data_dir=$CONDA_PREFIX
