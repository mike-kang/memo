```
dump layer0 info:
   channel(2)
   fmt(0x520c0420)
   width(300)
   height(300)
   channel(3)
   batch_num(1)
   fmt(0x23180888)

output layer number: 2
   layer (Softmax_scores_Y)
   pa (0x110b4ba0)
   va (0x73ec6ba0)
   size (126016)
   width (1)
   height (21)
   channel (3000)
   layout (whcn)
   bitdepth (16)
   sign_bits (1)
   int_bits (0)
   frac_bits (15)
   scale_ratio (1.000000)
   batch_num (1)
   layer (Concat_boxes_Y)
   pa (0x111971c0)
   va (0x73fa91c0)
   size (24000)
   width (1)
   height (4)
   channel (3000)
   layout (whcn)
   bitdepth (16)
   sign_bits (1)
   int_bits (1)
   frac_bits (14)
   scale_ratio (1.000000)
   batch_num (1)
load buf(pattern/output_300_300.yuv) ok

```
output layer 는 2개로, 3000개 box에 대해, score와 box 정보를 가진다.
score는 20(class) + 1 (배경)
box 는 중심점 변화량과 width, height 변화량

box의 좌표를 구하기 위해선, 3000개에 해당하는 default box의 각각의 중심점과 width, height 정보가 필요하다.



```
 ksflex@ksflex-desktop:~/work/novaic/root/model/fd2/pytorch-ssd$ python run_ssd_example.py mb1-ssd ../mobilenet-v1-ssd-mp-0_675.pth models/voc-model-labels.txt 0ac5fc8ae8b955d0.jpg
```

```
VENDOR_AI_BUF *layer_buffer = (VENDOR_AI_BUF *)malloc(outlayer_num * sizeof(VENDOR_AI_BUF));
network_get_ai_outlayer_by_path_id(proc_id, outlayer_path_list[i]/*path id*/, &(layer_buffer[i]));
hd_common_mem_flush_cache((VOID *)layer_buffer[i].va, layer_buffer[i].size); //cache data를 main memory로 보낸다.
UINT32 length = layer_buffer[i].width * layer_buffer[i].height * layer_buffer[i].channel * layer_buffer[i].batch_num;

ret = vendor_ai_cpu_util_fixed2float((VOID *)layer_buffer[i].va, layer_buffer[i].fmt, conf_loc_layer_float[i], layer_buffer[i].scale_ratio, length);
```