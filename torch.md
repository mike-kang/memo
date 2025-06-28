# version 확인
```bash
pip show torch | grep Version
```
- **정상 (GPU 지원)**: `Version: 2.1.0+cu118` ← `+cuXXX` 포함
    
- **문제 (CPU-only)**: `Version: 2.1.0` 또는 `+cpu`

# 설치
https://pytorch.org/get-started/locally/  
```bash
# CUDA 12.1
conda install pytorch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 pytorch-cuda=12.1 -c pytorch -c nvidia

or

pip install torch==2.2.2 torchvision==0.17.2 torchaudio==2.2.2 --index-url https://download.pytorch.org/whl/cu121

```
