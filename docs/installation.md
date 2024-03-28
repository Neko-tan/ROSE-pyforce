# Installation notes

The package has been tested on MacOS and Linux machines with **Python3.10**.

## Dependencies
The *pyforce* package requires the following dependencies:

```python
import numpy
import scipy
import matplotlib
import h5py

import pyvista
import gmsh
import dolfinx
import sklearn
import fluidfoam
```

Be sure to install *gmsh* and *gmsh-api* before *dolfinx* (the package has been tested with real mode of the PETSc library). The instructions to install *dolfinx* are available at [https://github.com/FEniCS/dolfinx#binary](https://github.com/FEniCS/dolfinx#binary).

### Set up a conda environment for *pyforce*

At first create a new conda environment
```bash
conda create --name <env_name>
```
If not already done, add conda-forge to the channels
```bash
conda config --add channels conda-forge
```
After having activate it, install 
```bash
conda install python=3.10
```
This provides also *pip* which is necessary to install *gmsh* as
```bash
python -m pip install gmsh gmsh-api
```
Then, *dolfinx* can be installed (real mode for *petsc* is supposed), currently only supports *v0.6.0*,
```bash
conda install fenics-dolfinx=0.6.0 mpich pyvista
```
Just for completeness, if you are to deal with complex numbers use the following command
```bash
conda install fenics-dolfinx=0.6.0 petsc=*=real* mpich pyvista
```
Add the following packages
```bash
conda install meshio scipy tqdm
```
Downgrade the following
```bash
python -m pip install setuptools==62.0.0
conda install numpy=1.23.5
```
Once this is completed, it may be necessary to re-install *gmsh*
```bash
python -m pip install gmsh gmsh-api
```
In the end, the *fluidfoam* ([https://github.com/fluiddyn/fluidfoam](https://github.com/fluiddyn/fluidfoam)) and *scikit-learn* are necessary to import data from OpenFOAM and to integrate Machine Learning (ML) with ROM
```bash
python -m pip install fluidfoam scikit-learn
```

## How to install *pyforce*?

Once all the dependencies have been installed, *pyforce* can be installed using *pip*.

Clone the repository 
```bash
git clone https://github.com/ROSE-Polimi/pyforce.git
```
Change directory to *pyforce* and install using pip
```bash 
python -m pip install pyforce/
```

## Generation of the documentation

*docs/* folder can be generate with
```bash
cd docs/
sphinx-apidoc -force -o ./api/. ../pyforce/pyforce
rm api/modules.rst
make clean
make html
```
These commands have been written in the *generate_docs.sh* script.

The following packages are needed:
```bash
python -m pip install sphinx==2.7.6 sphinxcontrib.bibtex==2.5.0 docutils==0.18.1 sphinx-rtd-theme==1.3.0 myst_parser IPython
```