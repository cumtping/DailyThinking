### CPU only版本安装较简单，先安装该版本。

### 有下面几种安装方式：
- VirtualEnv
- native pip
- Docker
- Anacona

### 本文记录使用VirtualEnv安装Cpu only版本TensorFlow的过程。

以Python2.7版本为例

- 安装python-virtualenv
  sudo apt-get install python-pip python-dev python-virtualenv
- 创建virtualenv环境
  virtualenv --system-site-packages targetDirectory
- 进入virtualenv环境
  source ~/tensorflow/bin/activate
- 更新pip
  easy_install -U pip
- 安装tensorflow
  pip install --upgrade tensorflow
  
安装信息：
wenpingwang-> pip install --upgrade tensorflow
Collecting tensorflow
/home/wenpingwang/work/tools/tensorflow/local/lib/python2.7/site-packages/pip-9.0.1-py2.7.egg/pip/_vendor/requests/packages/urllib3/util/ssl_.py:318: SNIMissingWarning: An HTTPS request has been made, but the SNI (Subject Name Indication) extension to TLS is not available on this platform. This may cause the server to present an incorrect TLS certificate, which can cause validation failures. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#snimissingwarning.
  SNIMissingWarning
/home/wenpingwang/work/tools/tensorflow/local/lib/python2.7/site-packages/pip-9.0.1-py2.7.egg/pip/_vendor/requests/packages/urllib3/util/ssl_.py:122: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
  Downloading tensorflow-1.6.0-cp27-cp27mu-manylinux1_x86_64.whl (45.9MB)
    100% |████████████████████████████████| 45.9MB 39kB/s 
Collecting six>=1.10.0 (from tensorflow)
  Downloading six-1.11.0-py2.py3-none-any.whl
Collecting enum34>=1.1.6 (from tensorflow)
  Downloading enum34-1.1.6-py2-none-any.whl
Collecting tensorboard<1.7.0,>=1.6.0 (from tensorflow)
  Downloading tensorboard-1.6.0-py2-none-any.whl (3.0MB)
    100% |████████████████████████████████| 3.1MB 440kB/s 
Collecting gast>=0.2.0 (from tensorflow)
  Downloading gast-0.2.0.tar.gz
Collecting protobuf>=3.4.0 (from tensorflow)
  Downloading protobuf-3.5.2-cp27-cp27mu-manylinux1_x86_64.whl (6.4MB)
    100% |████████████████████████████████| 6.4MB 223kB/s 
Collecting astor>=0.6.0 (from tensorflow)
  Downloading astor-0.6.2-py2.py3-none-any.whl
Collecting mock>=2.0.0 (from tensorflow)
  Downloading mock-2.0.0-py2.py3-none-any.whl (56kB)
    100% |████████████████████████████████| 61kB 1.2MB/s 
Collecting grpcio>=1.8.6 (from tensorflow)
  Downloading grpcio-1.10.0-cp27-cp27mu-manylinux1_x86_64.whl (7.4MB)
    100% |████████████████████████████████| 7.4MB 206kB/s 
Collecting numpy>=1.13.3 (from tensorflow)
  Downloading numpy-1.14.2-cp27-cp27mu-manylinux1_x86_64.whl (12.1MB)
    100% |████████████████████████████████| 12.1MB 112kB/s 
Collecting termcolor>=1.1.0 (from tensorflow)
  Downloading termcolor-1.1.0.tar.gz
Collecting backports.weakref>=1.0rc1 (from tensorflow)
  Downloading backports.weakref-1.0.post1-py2.py3-none-any.whl
Collecting absl-py>=0.1.6 (from tensorflow)
  Downloading absl-py-0.1.11.tar.gz (80kB)
    100% |████████████████████████████████| 81kB 480kB/s 
Collecting wheel (from tensorflow)
  Downloading wheel-0.30.0-py2.py3-none-any.whl (49kB)
    100% |████████████████████████████████| 51kB 494kB/s 
Collecting futures>=3.1.1; python_version < "3" (from tensorboard<1.7.0,>=1.6.0->tensorflow)
  Downloading futures-3.2.0-py2-none-any.whl
Collecting markdown>=2.6.8 (from tensorboard<1.7.0,>=1.6.0->tensorflow)
  Downloading Markdown-2.6.11-py2.py3-none-any.whl (78kB)
    100% |████████████████████████████████| 81kB 508kB/s 
Collecting html5lib==0.9999999 (from tensorboard<1.7.0,>=1.6.0->tensorflow)
  Downloading html5lib-0.9999999.tar.gz (889kB)
    100% |████████████████████████████████| 890kB 362kB/s 
Collecting werkzeug>=0.11.10 (from tensorboard<1.7.0,>=1.6.0->tensorflow)
  Downloading Werkzeug-0.14.1-py2.py3-none-any.whl (322kB)
    100% |████████████████████████████████| 327kB 1.0MB/s 
Collecting bleach==1.5.0 (from tensorboard<1.7.0,>=1.6.0->tensorflow)
  Downloading bleach-1.5.0-py2.py3-none-any.whl
Collecting setuptools (from protobuf>=3.4.0->tensorflow)
  Downloading setuptools-38.5.2-py2.py3-none-any.whl (490kB)
    100% |████████████████████████████████| 491kB 350kB/s 
Collecting funcsigs>=1; python_version < "3.3" (from mock>=2.0.0->tensorflow)
  Downloading funcsigs-1.0.2-py2.py3-none-any.whl
Collecting pbr>=0.11 (from mock>=2.0.0->tensorflow)
  Downloading pbr-3.1.1-py2.py3-none-any.whl (99kB)
    100% |████████████████████████████████| 102kB 419kB/s 
Building wheels for collected packages: gast, termcolor, absl-py, html5lib
  Running setup.py bdist_wheel for gast ... done
  Stored in directory: /home/wenpingwang/.cache/pip/wheels/8e/fa/d6/77dd17d18ea23fd7b860e02623d27c1be451521af40dd4a13e
  Running setup.py bdist_wheel for termcolor ... done
  Stored in directory: /home/wenpingwang/.cache/pip/wheels/de/f7/bf/1bcac7bf30549e6a4957382e2ecab04c88e513117207067b03
  Running setup.py bdist_wheel for absl-py ... done
  Stored in directory: /home/wenpingwang/.cache/pip/wheels/3c/0f/0a/6c94612a8c26070755559045612ca3645fea91c11f2148363e
  Running setup.py bdist_wheel for html5lib ... done
  Stored in directory: /home/wenpingwang/.cache/pip/wheels/6f/85/6c/56b8e1292c6214c4eb73b9dda50f53e8e977bf65989373c962
Successfully built gast termcolor absl-py html5lib
Installing collected packages: six, enum34, futures, wheel, markdown, setuptools, protobuf, html5lib, werkzeug, bleach, numpy, tensorboard, gast, astor, funcsigs, pbr, mock, grpcio, termcolor, backports.weakref, absl-py, tensorflow
  Found existing installation: six 1.5.2
    Not uninstalling six at /usr/lib/python2.7/dist-packages, outside environment /home/wenpingwang/work/tools/tensorflow
  Found existing installation: wheel 0.24.0
    Not uninstalling wheel at /usr/lib/python2.7/dist-packages, outside environment /home/wenpingwang/work/tools/tensorflow
  Found existing installation: setuptools 2.2
    Uninstalling setuptools-2.2:
      Successfully uninstalled setuptools-2.2
  Found existing installation: html5lib 0.999
    Not uninstalling html5lib at /usr/lib/python2.7/dist-packages, outside environment /home/wenpingwang/work/tools/tensorflow
  Found existing installation: numpy 1.8.2
    Not uninstalling numpy at /usr/lib/python2.7/dist-packages, outside environment /home/wenpingwang/work/tools/tensorflow
Successfully installed absl-py-0.1.11 astor-0.6.2 backports.weakref-1.0.post1 bleach-1.5.0 enum34-1.1.6 funcsigs-1.0.2 futures-3.2.0 gast-0.2.0 grpcio-1.10.0 html5lib-0.9999999 markdown-2.6.11 mock-2.0.0 numpy-1.14.2 pbr-3.1.1 protobuf-3.5.2 setuptools-38.5.2 six-1.11.0 tensorboard-1.6.0 tensorflow-1.6.0 termcolor-1.1.0 werkzeug-0.14.1 wheel-0.30.0
/home/wenpingwang/work/tools/tensorflow/local/lib/python2.7/site-packages/pip-9.0.1-py2.7.egg/pip/_vendor/requests/packages/urllib3/util/ssl_.py:122: InsecurePlatformWarning: A true SSLContext object is not available. This prevents urllib3 from configuring SSL appropriately and may cause certain SSL connections to fail. You can upgrade to a newer version of Python to solve this. For more information, see https://urllib3.readthedocs.io/en/latest/security.html#insecureplatformwarning.
