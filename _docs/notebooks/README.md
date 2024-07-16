# How-To
1. Install miniconda:
   1. Download and install the appropriate Miniconda installer from https://docs.conda.io/en/latest/miniconda.html. With Anaconda you can create environments that use any Python version (e.g. Python 2.7 or Python 3.6), so install the latest Python 3.x and if find out later you need a Python 2.7 environment, you can create one. Windows users also need to choose between 32-bit (old Windows XP) or 64-bit (modern Windows) versions.
1. Create the atn environment: 
   `$ conda env create -f .\environment.yml`
1. Activate the `atn` environment:
   `$ conda activate atn`
3. Start Jupyter Notebook: `$ jupyter notebook`