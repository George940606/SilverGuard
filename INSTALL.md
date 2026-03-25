# 🛡️ SilverGuard 專題環境安裝指南 (YOLO26 + M5 正式版)
本文件引導如何在 Apple Silicon (M5) 晶片上架設最新的 YOLO26 跌倒偵測開發環境。

## 一、 建立虛擬環境 (Conda)
為了確保專題環境純淨，我們建立一個獨立的開發空間。
### 1. 建立名為 silverguard 的環境 (Python 3.10)
```bash
conda create -n silverguard python=3.10 -y
```

### 2. 進入環境 (每次開始寫程式前都要執行這行)
```bash
conda activate silverguard
```

## 二、 安裝核心套件 (正式穩定版)
這裡安裝最穩定的正式版 PyTorch，並搭配最新的 Ultralytics 框架。
### 1. 安裝正式版 PyTorch (支援 Mac M5 的 GPU 加速)
```bash
pip install torch torchvision torchaudio
```

### 2. 安裝最新的 Ultralytics (支援 YOLO26) 與影像工具
```bash
pip install ultralytics opencv-python requests
```

#### 💡 Windows 組員注意：
若組員電腦有 NVIDIA 顯卡，請他們改跑此指令：
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```

## 三、 驗證安裝與 YOLO26 測試
請在終端機輸入 python，並貼上這段程式碼來確認硬體與模型是否就緒。
```python
import torch
from ultralytics import YOLO

# 1. 檢查硬體加速 (MPS)
print(f"PyTorch 版本: {torch.__version__}")
print(f"M5 GPU 加速 (MPS) 是否可用: {torch.backends.mps.is_available()}")

# 2. 測試載入最新的 YOLO26 Pose 模型
try:
    # 只要框架夠新，直接填 yolo26 就會自動下載最新的權重
    model = YOLO("yolo26n-pose.pt") 
    print("✅ YOLO26 模型載入成功！")
except Exception as e:
    print(f"❌ 載入失敗，請檢查網路連線: {e}")

exit()
```

## 四、 環境維護常用指令
* 退出房間：
```bash
conda deactivate
```
* 進入 SilverGuard 實驗室：
```bash
conda activate silverguard
```
* 回到 Anaconda 大廳 (Base)：
```bash
conda activate base
```
* 徹底移除環境 (砍掉重練)：
```bash
conda deactivate
conda env remove -n silverguard
```