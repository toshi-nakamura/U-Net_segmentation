# U-Net_segmentation
PyTorch で U-Net をスクラッチ実装し、Oxford-IIIT Pet データセットで二値セグメンテーションを行いました。
あわせて、ImageNet 学習済みの ResNet34 をエンコーダに使った U-Netと精度を比較しています。

## 結果

| モデル | エポック数 | Best Val IoU |
|--------|-----------|--------------|
| U-Net（スクラッチ実装） | 10 | 0.8994 |
| U-Net（ResNet34エンコーダ・ImageNet事前学習） | 10 | **0.9414** |

- 同じエポック数で、事前学習済みエンコーダを使うと IoU が約 0.04 向上しました
- 事前学習済みモデルは 1 エポック目で Val IoU 0.9236 に達しており、収束も大幅に速くなりました

## 目的

- エンコーダ・デコーダ構造とスキップ接続の役割を、実装を通して理解する
- 損失関数（BCE + Dice）と評価指標（IoU）の意味を理解する
- 事前学習済みエンコーダを使った場合との違いを確認する

## データセット

- [Oxford-IIIT Pet Dataset](https://www.robots.ox.ac.uk/~vgg/data/pets/)（`torchvision.datasets.OxfordIIITPet` で自動ダウンロード）
- 学習：`trainval` 3,680 枚、検証：`test` 3,669 枚

## 考察・今後の課題

- スクラッチ実装では背景の一部をペットと誤判定するなど、細部の精度が低い。事前学習済みエンコーダでは輪郭がかなり正確になった
- IoU の低い画像を可視化し、背景がほぼない（犬・猫でほぼ画面が埋まっている）画像や、毛色が白一色の猫は背景と動物の判定が逆転してしまっていた
- スクラッチ実装に関してはエポック数を増やして再実験したい

## ライセンス
- コード：MIT License
- ノートブックに含まれる画像は [Oxford-IIIT Pet Dataset](https://www.robots.ox.ac.uk/~vgg/data/pets/)
  （O. M. Parkhi, A. Vedaldi, A. Zisserman, C. V. Jawahar）の画像を使用・加工したもので、
  [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/) に従います。
  画像の著作権は各撮影者に帰属します。

