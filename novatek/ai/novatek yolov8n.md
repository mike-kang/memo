
학습/추론 모두에서 "color 정규화"를 하지 않는다. 

```
## [MEAN SUB]
# 0: disable meansub
# 1: enable meansub
[preproc/meansub/en] = 0
```

https://docs.ultralytics.com/ko/quickstart/

- 입력이 640×640이면 출력 해상도는 **80×80**, **40×40**, **20×20** → 총 **6,400 + 1,600 + 400 = 8,400** 지점에 대해 예측합니다.

아래는 convert한 방법인데, 기존 release에선 성공, release v2.5에선 실패했다.
```

docker run -it -v /home/ksflex/work/novaic:/mnt ubuntu16p04:v00.07.2108260

tools/release/release/ai_tool/novatek/novaic/toolchain/closeprefix/bin/compiler.nvtai --config-dir root --pattern-name fire-detect --chip 528  --use-heteroge 1
성공함
or

docker run -it -v /home/ksflex/work/novaic:/mnt ubuntu20p04:202407013

LD_LIBRARY_PATH=/mnt/tools/release_v2.5/release/ai_tool/novatek/novaic/toolchain/repo/proprietary/opencv/lib tools/release_v2.5/release/ai_tool/novatek/novaic/toolchain/closeprefix/bin/compiler.nvtai --config-dir root --pattern-name fire-detect --chip 528  --use-heteroge 1
실패함. - 
```
기존 release에서 성공한 것으로 돌려보면, 값이 맞질 않는다. 
추측으로는 기존 release 에서는 제대로 convert되지 않은 것 같다. release v2.5에서 제대로 convert해야 할 것 같다.

## onnx export
https://docs.ultralytics.com/ko/modes/export/#arguments

