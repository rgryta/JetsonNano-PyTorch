# JetsonNano-PyTorch
Repository containing built PyTorch wheels for Jetson Nano

## How to
Make sure you have `git lfs` installed on your system and then clone this repository, execute `git lfs pull` (or corresponding command) and install needed `.whl` file.

## Compiling from source
1. Install CUDA (at the moment of writing, CUDA 11.8 is supported) - https://developer.nvidia.com/cuda-11-8-0-download-archive - select arch: aarch64-jetson, compilation: native, installer: local (preference)
2. Use following instructions as base: https://forums.developer.nvidia.com/t/pytorch-for-jetson/72048
3. Install Jinja2 (needed before installing pytorch requirements - otherwise MarkupSafe fails to satisfy requirements)
4. Install numpy (if already installed, upgrade/reinstall) - if broken, you may need to resort to something like `sudo python3.11 -m pip uninstall numpy`
5. Make sure you have python3.X-dev installed
6. Clone pytorch repository and install requirements
7. Install ccache
8. Ensure that `nvcc --version` works, if not add it to path: export PATH=/usr/local/cuda/bin:$PATH
9. Additionally to flags from nvidia developers forum, set up CMAKE flag: export CMAKE_CUDA_ARCHITECTURES="53;62;72"
10. Pip install/upgrade PyYaml (Otherwise you might get `AttributeError: module 'collections' has no attribute 'Hashable'`)
11. Pip install/upgrade cmake
12. Build wheel: `python3.X setup.py bdist_wheel`

## .bashrc
Example .bashrc setup:
```sh
export PATH=/usr/local/cuda/bin:$PATH
export CMAKE_CUDA_ARCHITECTURES="53;62;72"
export USE_CUDA=1
export USE_NCCL=0
export USE_DISTRIBUTED=0
export USE_QNNPACK=0
export USE_PYTORCH_QNNPACK=0
export TORCH_CUDA_ARCH_LIST="5.3;6.2;7.2"
export PYTORCH_BUILD_VERSION=2.1.0
export PYTORCH_BUILD_NUMBER=1
```
