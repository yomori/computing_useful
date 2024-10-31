conda create -n tf-gpu tensorflow-gpu<BR>
conda activate tf-gpu<BR>
pip install cosmopower --no-deps<BR>
pip install tqdm --no-deps<BR>
conda install  -c conda-forge scikit-learn<BR>
pip install tensorflow_probability --no-deps<BR>
pip install tf_keras --no-deps<BR>
pip install decorator --no-deps <BR>
pip install dm-tree --no-deps<BR>
pip install cloudpickle --no-deps<BR>
conda install nvidia::cuda-compiler<BR>
export XLA_FLAGS=--xla_gpu_cuda_data_dir=$CONDA_PREFIX<BR>
