## Installation

### Code

The code has been tested with Python 3.8, CUDA 10.2 and PyTorch 1.7.1 on Ubuntu 18.04.

- Clone this repo, create virtual environment & install requirements
    ```
    git clone git@github.com:muelea/shapy.git
    cd shapy
    export PYTHONPATH=$PYTHONPATH:$(pwd)/attributes/

    conda create -n SHAPY python=3.8
    conda activate SHAPY
    pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
    pip install -r requirements.txt
    pip install pytorch-lightning==1.4.0rc0
    pip install opencv-python

    cd attributes
    python setup.py install

    cd ../mesh-mesh-intersection
    export CUDA_SAMPLES_INC=$(pwd)/include
    pip install -r requirements.txt
    python setup.py install
    cd ..
    ```

* Set OPENGL Platform to OS Mesa
```shell
export PYOPENGL_PLATFORM='osmesa'
```

* Get Pyrender Working with OSMesa <br>
Follow the instruction here: [link](https://pyrender.readthedocs.io/en/latest/install/index.html#osmesa) 

  
* If you get an error saying `ImportError: cannot import name 'OSMesaCreateContextAttribs' from 'OpenGL.osmesa'`, install a compatible version of `pyopengl`
```shell
cd ..
git clone https://github.com/mmatl/pyopengl.git
pip install ./pyopengl
cd shapy
```

* If you get an error w.r.t. jpeg4py package saying `AttributeError: 'JPEG' object has no attribute 'decompressor'`, install `libturbojpeg`
```shell
sudo apt-get install libturbojpeg
```

* If you get an error saying `numpy` has no attribute `bool`, install a previous version of `numpy`
```shell
pip3 install mxnet-mkl==1.6.0 numpy==1.23.1
```

* If you get an error saying `cannot import name 'get_num_classes' from 'torchmetrics.utilities.data'`, downgrade `torchmetrics` to `v0.6.0`
```shell
pip install torchmetrics==0.6.0
```

### Body model and model data

#### Folder structure

In `shapy/data`, you will need subfolders for the neutral SMPL-X body model (body_models) and ExPose and SHAPY models and utilities (expose_release, trained_models, utility_files). The final data structure should look like this:
```bash
data
├── body_models
├── expose_release
├── trained_models
└── utility_files
```


```bash
cd data
bash download_data.sh
```

#### Complete folder structure

After that, you should have the following structure:

```bash
data
├── body_models
│   ├── smpl
│   └── smplx
├── expose_release
│   ├── data
│   │   ├── all_means.pkl
│   │   └── SMPLX_to_J14.pkl
│   └── utility_files
│       └── flame
│           └── SMPL-X__FLAME_vertex_ids.npy
├── trained_models
│   ├── a2b
│   │   ├── caesar-female_smplx-female-10betas
│   │   ├── caesar-female_smplx-neutral-10betas
│   │   ├── caesar-male_smplx-male-10betas
│   │   └── caesar-male_smplx-neutral-10betas
│   ├── b2a
│   │   └── polynomial
│   │       ├── caesar-female_smplx-female-10betas
│   │       ├── caesar-female_smplx-neutral-10betas
│   │       ├── caesar-male_smplx-male-10betas
│   │       └── caesar-male_smplx-neutral-10betas
│   └── shapy
│       └── SHAPY_A
└── utility_files
    ├── evaluation
    │   └── eval_point_set
    │       ├── HD_SMPL_sparse.pkl
    │       └── HD_SMPLX_from_SMPL.pkl
    ├── measurements
    │   ├── measurement_defitions.yaml
    │   ├── smpl_measurement_vertices.yaml
    │   └── smplx_measurements.yaml
    ├── shape_priors
    │   ├── female_normal.npz
    │   └── male_normal.npz
    └── smplx
        ├── smplx_correspondences.npz
        └── smplx_extra_joints.yaml
```
