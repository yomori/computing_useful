conda create --name class_sz
conda activate class_sz
conda install python==3.9.18
conda install numpy==1.19.5
conda install -c conda-forge cython
conda install -c conda-forge scipy
conda install -c conda-forge six
pip install mcfit
pip install --no-deps tensorflow==2.6.5

make clean
make
cd python
pip install -e .
cd classy_szfast


pip install --no-deps cosmopower
conda install tqdm
conda install -c conda-forge scikit-learn
conda install -c conda-forge absl-py
conda install protobuf
conda install wrapt
conda install astunparse
conda install termcolor
conda install -c conda-forge keras-preprocessing
conda install -c conda-forge flatbuffers
conda install -c conda-forge tensorflow-probability
conda install -c conda-forge keras==2.7.0

edit class_sz/python/classy_szfast/classy_szfast/config.py
in particular path_to_cosmopower_organization

mkdir  cosmopower-organtization
git clone https://github.com/cosmopower-organization/lcdm.git
git clone https://github.com/cosmopower-organization/mnu.git
git clone https://github.com/cosmopower-organization/neff.git
git clone https://github.com/cosmopower-organization/wcdm.git


