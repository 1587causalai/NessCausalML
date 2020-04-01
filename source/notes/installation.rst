项目简介
============

本文是关于 Robert Ness Causal Machine Learning 的项目简介

.. note::
    我们不建议以root用户身份在系统python上进行安装。

安装步骤
---------------
    
请按照以下步骤来安装： 

#. 确保已安装PyTorch 1.4.0：

    .. code-block:: none

        $ python -c "import torch; print(torch.__version__)"
        >>> 1.4.0


#. 安装所有需要的软件包 with ``${CUDA}`` replaced by either ``cpu``, ``cu92``, ``cu100`` or ``cu101`` depending on your PyTorch installation:

    .. code-block:: none

      $ pip install torch-scatter==latest+${CUDA} -f https://pytorch-geometric.com/whl/torch-1.4.0.html



常见问题集
--------------------------

#. ``ImportError: ***: cannot open shared object file: No such file or directory``: Add CUDA to your ``$LD_LIBRARY_PATH`` (see `Issue#43 <https://github.com/rusty1s/pytorch_geometric/issues/43>`_).

#. ``undefined symbol:``, *e.g.* ``_ZN2at6detail20DynamicCUDAInterface10set_deviceE``: Clear the pip cache and reinstall the respective package (see `Issue#7 <https://github.com/rusty1s/pytorch_scatter/issues/7>`_). On macOS, it may help to install clang compilers via conda (see `Issue#18 <https://github.com/rusty1s/pytorch_geometric/issues/18>`_):

   .. code-block:: none

      $ conda install -y clang_osx-64 clangxx_osx-64 gfortran_osx-64

#. Unable to import ``*_cuda``: You need to ``import torch`` first before importing any of the extension packages (see `Issue#6 <https://github.com/rusty1s/pytorch_scatter/issues/6>`_).

#. ``error: command '/usr/bin/nvcc' failed with exit status 2``: Ensure that at least CUDA >= 8 is installed (see `Issue#25a <https://github.com/rusty1s/pytorch_geometric/issues/25>`_ and `Issue#106 <https://github.com/rusty1s/pytorch_geometric/issues/106>`_).

#. ``return __and_<is_constructible<_Elements, _UElements&&>...>::value``: Ensure that your ``gcc`` version is at least 4.9 (and below 6) (see `Issue#25b <https://github.com/rusty1s/pytorch_scatter/issues/25>`_).
   You will also need to reinstall PyTorch because ``gcc`` versions must be consistent across all PyTorch packages.

#. ``file not recognized: file format not recognized``: Clean the repository and temporarily rename Anaconda's ``ld`` linker (see `Issue#16683 <https://github.com/pytorch/pytorch/issues/16683>`_).

#. ``undefined symbol: __cudaPopCallConfiguration``: Ensure that your PyTorch CUDA version and system CUDA version match (see `Issue#19 <https://github.com/rusty1s/pytorch_scatter/issues/19>`_):

   .. code-block:: none

      $ python -c "import torch; print(torch.version.cuda)"
      $ nvcc --version

#. ``undefined symbol: _ZN3c105ErrorC1ENS_14SourceLocationERKSs``: The ``std::string`` abi does not match between building PyTorch and its extensions.
   This is fixable by building extensions with ``-D_GLIBCXX_USE_CXX11_ABI=1`` or building PyTorch from source (see `this PyTorch thread <https://discuss.pytorch.org/t/undefined-symbol-when-import-lltm-cpp-extension/32627>`_).

#. On macOS: ``'gcc' failed with exit status 1``: Install the respective packages by using the following environment variables (see `Issue#21 <https://github.com/rusty1s/pytorch_scatter/issues/21>`_):

   .. code-block:: none

       $ MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py install

#. On macOS: ``ld: warning: directory not found for option '-L/usr/local/cuda/lib64'`` and ``ld: library not found for -lcudart``: Symlink ``cuda/lib`` to ``cuda/lib64`` (see `Issue#116 <https://github.com/rusty1s/pytorch_geometric/issues/116>`_):

   .. code-block:: none

       $ sudo ln -s /usr/local/cuda/lib /usr/local/cuda/lib64

#. On macOS: ``The version of the host compiler ('Apple clang') is not supported``: Downgrade your command line tools (see `this StackOverflow thread <https://stackoverflow.com/questions/36250949/revert-apple-clang-version-for-nvcc/46574116>`_) with the respective version annotated in the `CUDA Installation Guide for Mac <https://developer.download.nvidia.com/compute/cuda/10.1/Prod/docs/sidebar/CUDA_Installation_Guide_Mac.pdf>`_ (Section 1.1) for your specific CUDA version.
   You can download previous command line tool versions `here <https://idmsa.apple.com/IDMSWebAuth/signin?appIdKey=891bd3417a7776362562d2197f89480a8547b108fd934911bcbea0110d07f757&path=%2Fdownload%2Fmore%2F&rv=1>`_.
