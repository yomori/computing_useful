conda create --name cosmopower2
conda install python==3.9.18     <----- check python version supported by tensorflow
pip install --upgrade pip
conda install -c conda-forge tensorflow-gpu
pip install cosmopower
conda install matplotlib==3.5.3
pip install tensorflow-probability==0.12.2  <--- need to degrade
conda install -c conda-forge camb
conda install astropy==4.3.1
conda install -c conda-forge pyccl==2.5.0
conda install -c conda-forge mpi4py
python -m pip install --no-deps cobaya==3.0.3
pip install pandas==1.2.1
pip install fuzzywuzzy==0.17 
pip install GetDist==1.1.1 
pip install py-bobyqa==1.1 

