```bash
../../toolchain/closeprefix/bin/compiler.nvtai  <config dir path> <pattern-name> --chip 528

<config dir path>: config directory를 가진 부모 path
<pattern-name>: model의 이름
<config dir path>/config/<pattern-name>/cnn25 에 gen_config.txt 파일이 존재해야 한다.

```
추가 옵션
--use-heteroge 1  (ssd_mobilev1 convert시 필요했다.)


convert에 필요한 옵션들 중 가장 중요한 것은 gen_config.txt이다.

# gen_config.txt 
   - 'config dir path'의 상대 경로로 지정한다.
   - path 가 필요한 항목들
     - ref_img_list.txt 와 참조 이미지 파일들 
     - mean_data.txt
     - model (onnx)

Novatek은 여러 모델을 한 곳에서 관리하는 구조를 염두해 둔 것 같다. 그래서 convert시에도 config-dir을 받고 그 안에서 model directory 내에 config






