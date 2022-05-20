# lprnet-on-tao-toolkit
lprnet-on-tao-toolkit は、NVIDIA TAO TOOLKIT を用いて LPRNet の AIモデル最適化を行うマイクロサービスです。  

## 動作環境
- NVIDIA 
    - TAO TOOLKIT
- LPRNet
- Docker
- TensorRT Runtime

## LPRNetについて
LPRNet は、画像内のナンバープレートの文字を認識し、カテゴリラベルを返すAIモデルです。  
LPRNet は、特徴抽出にResNet18を使用しており、混雑した場所でも正確に物体検出を行うことができます。

## 動作手順

### engineファイルの生成
LPRNet のAIモデルをデバイスに最適化するため、ResNet18 における LPRNet の .etlt ファイルを engine file に変換します。
engine fileへの変換は、Makefile に記載された以下のコマンドにより実行できます。

```
tao-convert:
	docker exec -it lprnet-tao-toolkit tao-converter -k nvidia_tlt -p image_input,1x3x48x96,4x3x48x96,16x3x48x96 \
		-t fp16 -e /app/src/lprnet_usa.engine /app/src/us_lprnet_baseline18_deployable.etlt
```

## 相互依存関係にあるマイクロサービス  
本マイクロサービスで最適化された LPRNet の AIモデルを Deep Stream 上で動作させる手順は、[lprnet-on-deepstream](https://github.com/latonaio/lprnet-on-deepstream)を参照してください。  

## engineファイルについて
engineファイルである lprnet_usa.engine は、[lprnet-on-deepstream](https://github.com/latonaio/lprnet-on-deepstream)と共通のファイルであり、本レポジトリで作成した engineファイルを、当該リポジトリで使用しています。  
