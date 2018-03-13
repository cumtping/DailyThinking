 Installing TensorFlow on Windows

This guide explains how to install TensorFlow on Windows. Although these instructions might also work on other Windows variants, we have only tested (and we only support) these instructions on machines meeting the following requirements:

    64-bit, x86 desktops or laptops
    Windows 7 or later

Determine which TensorFlow to install

You must choose one of the following types of TensorFlow to install:

    TensorFlow with CPU support only. If your system does not have a NVIDIA® GPU, you must install this version. Note that this version of TensorFlow is typically much easier to install (typically, in 5 or 10 minutes), so even if you have an NVIDIA GPU, we recommend installing this version first. Prebuilt binaries will use AVX instructions.
    TensorFlow with GPU support. TensorFlow programs typically run significantly faster on a GPU than on a CPU. Therefore, if your system has a NVIDIA® GPU meeting the prerequisites shown below and you need to run performance-critical applications, you should ultimately install this version.

Requirements to run TensorFlow with GPU support

If you are installing TensorFlow with GPU support using one of the mechanisms described in this guide, then the following NVIDIA software must be installed on your system:

    CUDA® Toolkit 9.0. For details, see NVIDIA's documentation Ensure that you append the relevant Cuda pathnames to the %PATH% environment variable as described in the NVIDIA documentation.
    The NVIDIA drivers associated with CUDA Toolkit 9.0.
    cuDNN v7.0. For details, see NVIDIA's documentation. Note that cuDNN is typically installed in a different location from the other CUDA DLLs. Ensure that you add the directory where you installed the cuDNN DLL to your %PATH% environment variable.
    GPU card with CUDA Compute Capability 3.0 or higher for building from source and 3.5 or higher for our binaries. See NVIDIA documentation for a list of supported GPU cards.

If you have a different version of one of the preceding packages, please change to the specified versions. In particular, the cuDNN version must match exactly: TensorFlow will not load if it cannot find cuDNN64_7.dll. To use a different version of cuDNN, you must build from source.
Determine how to install TensorFlow

You must pick the mechanism by which you install TensorFlow. The supported choices are as follows:

    "native" pip
    Anaconda

Native pip installs TensorFlow directly on your system without going through a virtual environment. Since a native pip installation is not walled-off in a separate container, the pip installation might interfere with other Python-based installations on your system. However, if you understand pip and your Python environment, a native pip installation often entails only a single command! Furthermore, if you install with native pip, users can run TensorFlow programs from any directory on the system.

In Anaconda, you may use conda to create a virtual environment. However, within Anaconda, we recommend installing TensorFlow with the pip install command, not with the conda install command.

NOTE: The conda package is community supported, not officially supported. That is, the TensorFlow team neither tests nor maintains this conda package. Use that package at your own risk.
Installing with native pip

If one of the following versions of Python is not installed on your machine, install it now:

    Python 3.5.x 64-bit from python.org
    Python 3.6.x 64-bit from python.org

TensorFlow supports Python 3.5.x and 3.6.x on Windows. Note that Python 3 comes with the pip3 package manager, which is the program you'll use to install TensorFlow.

To install TensorFlow, start a terminal. Then issue the appropriate pip3 install command in that terminal. To install the CPU-only version of TensorFlow, enter the following command:

C:\> pip3 install --upgrade tensorflow

To install the GPU version of TensorFlow, enter the following command:

C:\> pip3 install --upgrade tensorflow-gpu

Installing with Anaconda

The Anaconda installation is community supported, not officially supported.

Take the following steps to install TensorFlow in an Anaconda environment:

    Follow the instructions on the Anaconda download site to download and install Anaconda.

    Create a conda environment named tensorflow by invoking the following command:

    C:> conda create -n tensorflow pip python=3.5 

    Activate the conda environment by issuing the following command:

    C:> activate tensorflow
     (tensorflow)C:>  # Your prompt should change 

    Issue the appropriate command to install TensorFlow inside your conda environment. To install the CPU-only version of TensorFlow, enter the following command:

    (tensorflow)C:> pip install --ignore-installed --upgrade tensorflow 

    To install the GPU version of TensorFlow, enter the following command (on a single line):

    (tensorflow)C:> pip install --ignore-installed --upgrade tensorflow-gpu 

Validate your installation

Start a terminal.

If you installed through Anaconda, activate your Anaconda environment.

Invoke python from your shell as follows:

$ python

Enter the following short program inside the python interactive shell:

>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))

If the system outputs the following, then you are ready to begin writing TensorFlow programs:

Hello, TensorFlow!

If you are new to TensorFlow, see @{$get_started/get_started$Getting Started with TensorFlow}.

If the system outputs an error message instead of a greeting, see Common installation problems.

There is also a helpful script for Windows TensorFlow installation issues.
Common installation problems

We are relying on Stack Overflow to document TensorFlow installation problems and their remedies. The following table contains links to Stack Overflow answers for some common installation problems. If you encounter an error message or other installation problem not listed in the following table, search for it on Stack Overflow. If Stack Overflow doesn't show the error message, ask a new question about it on Stack Overflow and specify the tensorflow tag.
Stack Overflow Link 	Error Message
41007279 	

[...\stream_executor\dso_loader.cc] Couldn't open CUDA library nvcuda.dll

41007279 	

[...\stream_executor\cuda\cuda_dnn.cc] Unable to load cuDNN DSO

42006320 	

ImportError: Traceback (most recent call last):
File "...\tensorflow\core\framework\graph_pb2.py", line 6, in 
from google.protobuf import descriptor as _descriptor
ImportError: cannot import name 'descriptor'

42011070 	

No module named "pywrap_tensorflow"

42217532 	

OpKernel ('op: "BestSplits" device_type: "CPU"') for unknown op: BestSplits

43134753 	

The TensorFlow library wasn't compiled to use SSE instructions

38896424 	

Could not find a version that satisfies the requirement tensorflow
