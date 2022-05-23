
* **[Link To The Blog Post](https://srush.github.io/annotated-s4)**


<a href="https://srush.github.io/annotated-s4"><img src="https://user-images.githubusercontent.com/35882/149201164-1723a44a-f34b-467c-94b0-ffda5ebcabbb.png"></a>



## Experiments

#### MNIST Sequence Modeling

```bash
python3 -m s4.train --dataset mnist --model s4 --epochs 100 --bsz 128 --d_model 128 --ssm_n 64
```

#### QuickDraw Sequence Modeling

```bash
# Default arguments
python3 -m s4.train --dataset quickdraw --model s4 --epochs 10 --bsz 128 --d_model 128 --ssm_n 64

# "Run in a day" variant
python3 -m s4.train --dataset quickdraw --model s4 --epochs 1 --bsz 512 --d_model 256 --ssm_n 64 --p_dropout 0.05
```

#### MNIST Classification

```bash
python3 -m s4.train --dataset mnist-classification --model s4 --epochs 10 --bsz 128 --d_model 128 --ssm_n 64
```

Gets "best" 97.76% accuracy in 10 epochs @ 40s/epoch on a TitanRTX.

#### CIFAR-10 Classification

```
# Following @frederick0329's/@albertgu's results: https://github.com/srush/annotated-s4/pull/43#issuecomment-1065444261
python3 -m s4.train --dataset cifar-classification --model s4 --epoch 100 --bsz 64 --n_layers 6 --p_dropout 0.25 --lr 5e-3 --d_model 512

# DSS Model
python3 -m s4.train --dataset cifar-classification --model dss --epoch 100 --bsz 64 --n_layers 6 --p_dropout 0.25 --lr 5e-3 --d_model 512
```

S4 gets "best" 87.05% accuracy after 100 epochs @ 3m8s/epoch on a TitanRTX
DSS gets "best" 88.90% accuracy after 100 epochs @ 3m11s/epoch on a TitanRTX

---

## Quickstart (Development)

We have two `requirements.txt` files that hold dependencies for the current project: one that is tailored to CPUs,
the other that installs for GPU.

### CPU-Only (MacOS, Linux)

```bash
# Set up virtual/conda environment of your choosing & activate...
pip install -r requirements-cpu.txt

# Set up pre-commit
pre-commit install
```

### GPU (CUDA > 11 & CUDNN > 8.2)

```bash
# Set up virtual/conda environment of your choosing & activate...
pip install -r requirements-gpu.txt

# Set up pre-commit
pre-commit install
```

## Dependencies from Scratch

In case the above `requirements.txt` don't work, here are the commands used to download dependencies.

### CPU-Only

```bash
# Set up virtual/conda environment of your choosing & activate... then install the following:
pip install --upgrade "jax[cpu]"
pip install flax
pip install torch torchvision torchaudio

# Defaults
pip install black celluloid flake8 google-cloud-storage isort ipython matplotlib pre-commit seaborn tensorflow tqdm

# Set up pre-commit
pre-commit install
```

### GPU (CUDA > 11, CUDNN > 8.2)

Note - CUDNN > 8.2 is critical for compilation without warnings, and GPU w/ at least Turing architecture for full
efficiency.

```bash
# Set up virtual/conda environment of your choosing & activate... then install the following:
pip install jax[cuda11_cudnn82] -f https://storage.googleapis.com/jax-releases/jax_releases.html
pip install flax
pip install torch==1.10.1+cpu torchvision==0.11.2+cpu torchaudio==0.10.1+cpu -f https://download.pytorch.org/whl/cpu/torch_stable.html

# Defaults
pip install black celluloid flake8 google-cloud-storage isort ipython matplotlib pre-commit seaborn tensorflow tqdm

# Set up pre-commit
pre-commit install
```
