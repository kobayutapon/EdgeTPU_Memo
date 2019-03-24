# Edge TPU Deviceの使い方（準備編）
参照URL:https://coral.withgoogle.com/tutorials/accelerator/

## 必要な環境
Edge TPUを動作させるにはUSBポートを備えたLinuxを搭載したコンピュータが必要です。
* Debian 6.0 or higher, or any derivative thereof (such as Ubuntu 10.0+)
* System architecture of either x86_64 or ARM64 with ARMv8 instruction set

ARM v8アーキテクチャを備えたARM64でも動作するので、Raspberry Pi2/3B/3B+でも動作します。
(3A+でも動作するよね)

## Linux/Raspberry Piでのセットアップ
1. 以下のコマンドを実行し、RuntimeとPython Libraryをインストールする。

```
 wget http://storage.googleapis.com/cloud-iot-edge-pretrained-models/edgetpu_api.tar.gz  
 tar xzf edgetpu_api.tar.gz  
 cd python-tflite-source  
 bash ./install.sh
```
インストール中に"Would you like to enable the maximum operating frequency?"と聞かれるが、ここでYを押すとTPUをぶん回す設定になる。その場合、TPU自体の発熱が大変になるそうなので注意すること。  
あと、install.shのシェルスクリプトがpython3.5決め打ちになっていて、3.5以上が入っていると実行時にエラーになる。その場合、install.shを修正すれば良い。

2. PCとAccelaratorをUSBケーブルで接続する。

3. デモを実行し、動作確認をしてみる。
以下のコマンドを実行し、動作を見てみる。
```
# From the python-tflite-source directory
cd edgetpu/

python3 demo/classify_image.py \
--model test_data/mobilenet_v2_1.0_224_inat_bird_quant_edgetpu.tflite \
--label test_data/inat_bird_labels.txt \
--image test_data/parrot.jpg
```

以下のような出力がなされれば動作している。
```
---------------------------
Ara macao (Scarlet Macaw)
Score :  0.613281
---------------------------
Platycercus elegans (Crimson Rosella)
Score :  0.152344
```
自分の環境では以下のような警告がでるが、動作に支障はない模様。ただちょっと気持ち悪い。

```
W third_party/darwinn/driver/package_registry.cc:65] Minimum runtime version required by package (5) is lower than expected (10).
```

