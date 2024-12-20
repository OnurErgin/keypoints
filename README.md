# Key Point detection with MMPose and ONNX

(MMPose works on Linux, Windows and macOS. It requires Python 3.7+, CUDA 9.2+ and PyTorch 1.8+. https://mmpose.readthedocs.io/en/latest/installation.html)

## Setting up the environment.

0. Ensure Python is installed.

    On Windows, install python from python.org\
    On Linux python3 is probably installed with the system\
    Deactivate conda if present:
    `conda deactivate`


1. Install PipX to install Poetry\
On Windows:
`py -m pip install --user pipx`\
On Ubuntu: 
`sudo apt install pipx`

    It is possible (even most likely) the above finishes with a WARNING looking similar to this:\
        ```
        WARNING: The script pipx.exe is installed in `<USER folder>\AppData\Roaming\Python\Python3x\Scripts` which is not on PATH
        ```
        If so, go to the mentioned folder, allowing you to run the pipx executable directly. Enter the following line (even if you did not get the warning):\
        `.\pipx.exe ensurepath`

1. Install Poetry
    (use pip to install libraries to use in python scripts, use pipx to install commands, like poetry)
    
    `pipx install poetry`

     For VSCode to recognize the venv with poetry by placing it into the project folder:\
    ``` bash
    poetry config virtualenvs.in-project true
    ```
1. Initiate the project with `poetry init` and disable the package mode (we use poetry for package management only)

    ``` toml
    [tool.poetry]
    package-mode = false
    ```

1. Add the necessary packages

    1. Add the source for Pytorch v12.4
        ``` bash
        poetry source add --priority=explicit pytorch124 https://download.pytorch.org/whl/cu124
        ```
    1. Add pytorch and torchvision
        ``` bash
        poetry add torch --source pytorch124
        poetry add torchvision --source pytorch124
        ```

    1. Install CUDA at the system level (this is not a package, can't be installed with poetry)
        ``` bash
        # https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu
        # Install the new cuda-keyring package for ubuntu2404/x86_64

        wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2404/x86_64/cuda-keyring_1.1-1_all.deb
        sudo dpkg -i cuda-keyring_1.1-1_all.deb

        sudo apt-get update
        sudo apt-get install cuda-toolkit
        sudo apt-get install nvidia-gds
        sudo reboot
        ```

    1. Install MMPose

        ``` bash
        # poetry add openmim
        # poetry shell 
        # mim install mmengine
        # mim install "mmcv>=2.0.1"
        
        # Above or below. should be same. 
        poetry add mmengine
        poetry add "mmcv>=2.0.1"

        python -c "import mmpose; print(mmpose.__version__)"
        ```