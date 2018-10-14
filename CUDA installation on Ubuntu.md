# Ubuntu 16.04 CUDA 9.2, TensorFlow GPU

## 環境

- OS: Ubuntu 16.04 LTS
- GPU: NVidia GeForce 1050Ti
- Anaconda3-5.2.0 (pyenv)
- CUDA 9.2
- cuDNN 7.2 for CUDA 9.2
- tensorflow-gpu=1.10.0

わざわざプロジェクトごとにTensorFlowや他のパッケージを導入するのもなぁと思い，pyenvでanaconda環境を用意しておいてそこに`conda install`などで追加するという形にした．pyenv-virtualenvやconda-venvもありかなと思われる．ちなみにUbuntu 18.04 LTSでもインストールを試みたがnvidia-396ドライバがうまく動作しないようで諦めた．(tensorflow-gpuは動く)

## インストール手順

### 準備

古いパッケージの削除．`dpkg -l | grep nvidia`などとして余計なものが残っていないか見ておくのもあり．

```shell
sudo apt remove --purge nvidia* cuda* libcudnn*
sudo apt autoremove
```

### インストールファイルの入手

[CUDA Toolkit 9.2 Downloads](https://developer.nvidia.com/cuda-downloads)から，Linux→x86_64→Ubuntu→16.04→.deb(network)と進み，.debファイルをダウンロードしておく．

そして再起動．

###  インストール

再起動したら，ログイン画面でCUIに移り，X serverを停止．

```shell
sudo service lightdm stop
pkill Xorg
```

以下のように，CUDAをインストール．

```shell
sudo dpkg -i cuda-repo-ubuntu1604_9.2.*_amd64.deb
sudo apt-key adv --fetch-keys http://developer.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo apt update
sudo apt install cuda
```

完了後，再起動．

### PATH

.bashrcなどに以下の行を追加．

```shell 
export PATH=/usr/local/cuda/bin:${PATH}
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:${LD_LIBRARY_PATH}
```

### 動作確認

```shell
nvidia-smi
nvcc -V
```

### cuDNNのインストール

```shell 
sudo dpkg -i libcudnn7_7.2*+cuda9.2_amd64.deb
sudo dpkg -i libcudnn7-dev_7.2*+cuda9.2_amd64.deb
sudo dpkg -i libcudnn7-doc_7.2*+cuda9.2_amd64.deb 
```

## TensorFlow GPUの導入

### 準備

ある作業フォルダでAnaconda環境に移り，Anacondaや他のパッケージを更新しておく．

```shell
pyenv local anaconda3-5.2.0
conda update conda
conda upgrade --all
```

### インストール

その後，TensorFlow GPU, kerasのインストールを行う.

```shell
conda install tensorflow-gpu keras
```

この時，tensorflow-gpuと共にインストールされるCUDAやcudnnのバージョンが違わないかきちんと確認しておく．

### 動作確認

インストールが完了したらpythonコンソールなどで，

```python
>>> import keras
Using TensorFlow backend．
>>>
```

となることを確認しておく．

[mnist_cnn.py](https://github.com/keras-team/keras/blob/master/examples/mnist_cnn.py)などのサンプルコードがきちんと動くか，また，別ウィンドウで`nvidia-smi -l 5`などとして計算にGPUがきちんと利用されているかをモニターしながらコードを実行して，問題なければ作業は完了．