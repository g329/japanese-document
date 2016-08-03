インストールガイド
=========


.. _before_install:

事前準備
----

以下のプラットフォームでの利用を推奨しています.

* `Ubuntu <http://www.ubuntu.com/>`_ 14.04 LTS 64bit
* `CentOS <https://www.centos.org/>`_ 7 64bit

ChainerはPython 2.7.6+, 3.4.3+, 3.5.1+をサポートしています.
Chainerはg++などのC++コンパイラを使用します.
Chainerをインストールする前に, C++コンパイラをインストールしてください.
各推奨プラットフォームでは, 以下のコマンドでインストールすることができます.

.. code-block:: bash

  # Ubuntu 14.04
  $ apt-get install g++

  # CentOS 7
  $ yum install gcc-c++

``setuptools`` を, 以下のコマンドにより最新版にしてください

.. code-block:: bash

  $ pip install -U setuptools


Chainerのインストール
--------------

Chainerは以下のパッケージに依存しています.

* `NumPy <http://www.numpy.org/>`_ 1.9, 1.10, 1.11
* `Six <https://pythonhosted.org/six/>`_ 1.9

Chainerは, 以下のバージョンのCUDAをサポートしています.

* `CUDA <https://developer.nvidia.com/cuda-zone>`_ 6.5, 7.0, 7.5
* `filelock <https://filelock.readthedocs.org>`_

Chainerは, 以下のバージョンのcuDNNをサポートしています.

* `cuDNN <https://developer.nvidia.com/cudnn>`_ v2, v3, v4, v5

Chainerは, 以下のバージョンのCaffe Modelをサポートしています.

* `Protocol Buffers <https://developers.google.com/protocol-buffers/>`_
* Py3では, protobuf>=3.0.0を必要としています.

上記のライブラリはすべて ``pip`` や ``setup.py`` でChainerと同時にインストールされます.

HDF5は, 必要に応じてインストールしてください.

* `h5py <http://www.h5py.org/>`_ 2.5.0


pipを用いたインストール方法
~~~~~~~~~~~~~~~

以下のように, pipを用いてインストールすることを推奨します.

.. code-block:: bash

  $ pip install chainer


ソースコードからのインストール方法
~~~~~~~~~~~~~~~~~

ソースコードからインストールする際は, 下記のように ``setup.py`` を使ってください.

.. code-block:: bash

  $ tar zxf chainer-x.x.x.tar.gz
  $ cd chainer-x.x.x
  $ python setup.py install


.. _install_error:

インストールに失敗した際は...
~~~~~~~~~~~~~~~~

``-vvvv`` オプションを ``pip`` コマンドに付けて実行してください.
インストールログが表示されます.解決手段を見つけることができるかもしれません.

.. code-block:: bash

  $ pip install chainer -vvvv


Chainerのインストール方法（CUDA利用）
~~~~~~~~~~~~~~~~~~~~~~~~

CUDAツールキットは, Chainerの前にインストールする必要があります.
``CUDA_PATH`` が正しく設定されていれば, ChainerのインストーラはCUDAを自動的に検知します.

.. code-block:: bash

  $ pip install chainer


.. note::

   Chainerのインストーラは環境変数 ``CUDA_PATH`` を最初に探します.
   未設定ならば, Chainerのインストーラは環境変数 ``PATH`` から ``nvcc`` コマンドを探し，その親ディレクトリをCUDAインストール時のルートディレクトリとみなします.
   ``nvcc`` コマンドも見つからない場合, インストーラは ``/usr/local/cuda`` をデフォルト設定として利用します.


もしもあなたがCUDAをデフォルトでないディレクトリにインストールしていた場合, 環境変数 ``CUDA_PATH`` を正しく設定する必要があります.

.. code-block:: bash

  $ CUDA_PATH=/opt/nvidia/cuda pip install chainer


.. warning::

  ``sudo`` をChainerのインストール時に使いたい場合,  ``sudo`` コマンドはすべての環境変数を初期化することに注意してください.
  以下のようにして, 環境変数 ``CUDA_PATH`` を ``sudo`` に明示的に追加してください.

.. code-block:: bash

  $ sudo CUDA_PATH=/opt/nvidia/cuda pip install chainer



.. _install_cudnn:

Chainerのインストール方法（CUDA, cuDNN利用）
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

cuDNNはNVIDIA社が提供している, Deep Neural Networksのためのライブラリです.
Chainerは, cuDNNを利用することができます.
cuDNNを利用したい場合, Chainerをインストールする前にcuDNNとCUDAをインストールしてください.
CUDAと同じディレクトリにcuDNNをインストールすることをお勧めします.
Ubuntuを使っている場合, ``.h`` ファイルを ``include`` ディレクトリに, ``.so`` ファイルを ``lib64`` ディレクトリにコピーしてください.

.. code-block:: bash

  $ cp /path/to/cudnn.h $CUDA_PATH/include
  $ cp /path/to/libcudnn.so* $CUDA_PATH/lib64

対象ディレクトリは環境により異なります

Chainerのインストール方法(開発者向け)
~~~~~~~~~~~~~~~~~~~~~~~

ChainerはCythonを使用します(>= 0.23).
開発者の方々は, ``pyx`` ファイルからC++のソースコードを再生成するためにCythonを利用する必要があります.
``pip`` に ``-e`` オプションを付け,編集可能モードで利用することをお勧めします.

.. code-block:: bash

  $ pip install -U cython
  $ cd /path/to/chainer/source
  $ pip install -e .


Chainerに含まれるソースコードを利用するのみの場合, Cythonをインストールする必要はありません.

HDF5によるシリアライズのサポート
~~~~~~~~~~~~~~~~~~

HDF5によるシリアライズを有効にしたい場合, h5pyを手動でインストールしてください.
この機能は必須ではありません.

.. code-block:: bash

  $ pip install h5py


h5pyをインストールする前に, libhdf5をインストールする必要があります.
インストール方法は, 環境により異なります.

.. code-block:: bash

  # Ubuntu 14.04
  $ apt-get install libhdf5-dev

  # CentOS 7
  $ yum -y install epel-release
  $ yum install hdf5-devel


Chainerのアンインストール方法
------------------

pipを用いて, Chainerをアンインストールしてください.

.. code-block:: bash

  $ pip uninstall chainer


.. note::

   Chainerをアップグレードする際, ``pip`` は時々 ``site-packages`` に異なるバージョンのChainerをインストールすることがあります.
   ``pip`` がエラーを返すまで, アンインストールし続けてください.


Chainerのアップグレード
---------------

``-U`` オプションを付けて, ``pip`` を実行してください.

.. code-block:: bash

  $ pip install -U chainer


Chainerの再インストール
---------------

Chainerを再インストールしたい場合, まずChainerをアンインストールしてください.
再インストールする際, ``--no-cache-dir`` オプションを付けて ``pip`` を実行することをおすすめします.

.. code-block:: bash

  $ pip uninstall chainer
  $ pip install chainer --no-cache-dir

CUDAなしでChainerをインストールして, CUDAを使いたくなった場合, Chainerを再インストールしてください.
CUDAをアップグレードしたくなった場合も, Chainerを再インストールする必要があります.


"推奨"の意味
-------

私達はJenkinsを用いてChainerの動作確認を行っています.
その他の環境でのChainerの動作については, 保証できません.


よくある質問
------

インストール時に "hdf5.h is not found"というメッセージが表示される
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

libhdf5を持っていない可能性があります.
hdf5をインストールしてください.
参考 :ref:`before_install`.


MemoryErrorが発生する
~~~~~~~~~~~~~~~~

Cythonのインストールに失敗している可能性があります.
手動でインストールしてみてください.
参考 :ref:`install_error`.


Examples を実行すると "cuDNN is not enabled" と表示される
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

cuDNNを利用したChainerのビルドに失敗しています.
cuDNNを利用しない場合, このメッセージを無視してください.
cuDNNを利用する場合, Chainerのインストール(cuDNN利用)の手順をもう一度行ってください.
``-vvvv`` オプションが, 役に立つかもしれません.
参考 :ref:`install_cudnn`.
