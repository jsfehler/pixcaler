# chainer-pix2pix
chainer implementation of pix2pix
https://phillipi.github.io/pix2pix/

The Japanese readme can be found [here](README-ja.md).

# Example result on CMP facade dataset
<img src="https://github.com/mattya/chainer-pix2pix/blob/master/image/example.png?raw=true">
From the left side: input, output, ground_truth


# usage
1. `pip install -r requirements.txt`
2. Download the facade dataset (base set) http://cmp.felk.cvut.cz/~tylecr1/facade/
3. `python train_facade.py -g [GPU ID, e.g. 0] -i [dataset root directory] --out [output directory] --snapshot_interval 10000`
4. Wait a few hours...
 - `--out` stores snapshots of the model and example images at an interval defined by `--snapshot_interval`
 - If the model size is large, you can reduce `--snapshot_interval` to save resources.

# Using other datasets
- データセットを用意する。位置の合った画像(あるいは画像的な構造を持つarray)のペアが必要。数百枚程度でもそれっぽい結果が出せると言われている。
- `facade_dataset.py`を書き換える。get_exampleが呼ばれた時に、i番目の(入力画像, 教師出力画像)が返るようになっていれば良い(両方numpy array)。
- `updater.py`でlossの計算を行っているが(現在はL1 loss + adversarial loss)、変える必要があれば変える。
- `facade_visualizer.py`の可視化コードをデータセットに合わせて書き換える。
- `train_facade.py`は50行目くらいのin_ch, out_chをデータセットに合わせて書き換える。
