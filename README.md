# 🏛️ RomanMNIST: 手寫羅馬數字辨識與數據增強

## 📖 專案簡介
本專案探討 **如何透過數據清理與增強技術，提高固定模型在手寫羅馬數字辨識上的準確度**。我們主要透過 **錯誤標籤修正、數據增強（旋轉、縮放、平移、對比度調整）** 來提升模型效能，並使用 **CleanVision** 檢測與清理異常數據。最終，我們成功將 **模型準確率提升至 80% 以上**。

## 🔥 研究動機
手寫數字辨識在 **歷史文獻數字化、自動化評分、身份驗證** 等應用中具有重要價值。羅馬數字辨識相較於阿拉伯數字更具挑戰性，因為其 **書寫風格多變**，且不同組合的數字容易混淆。本專案希望在 **固定模型架構** 下，透過更 **乾淨且多樣的數據**，來改善模型的辨識能力。

---

## 📊 數據集與方法

### **📂 資料來源**
- **原始數據集**: 來自 [Kaggle](https://www.kaggle.com/datasets/agneev/basedonenglishhandwrittencharactersmodified)
- 包含：
  - 訓練集：**3367 張影像**
  - 驗證集：**963 張影像**
  - 測試集：**52 張影像**
- **影像格式**: **灰階手寫羅馬數字**
- **挑戰點**:
  - 錯誤標籤
  - 影像品質不均（亮度、模糊、大小不一致）
  - 部分手寫數字難以辨識（雜訊影響）

---

### **🛠 研究方法**
#### **1️⃣ 錯誤標籤修正**
- **問題**: 原始數據包含錯誤標籤，影響模型學習
- **解決方案**:
  - 手動檢查 **錯誤標籤**，並將錯誤影像移動至正確類別
  - 刪除無法辨識或模糊的影像
  - **影響**: 修正後模型準確度提升至 **70% 以上**

#### **2️⃣ 外部數據擴增**
- **目標**: 增加多樣性，讓模型學習更廣泛的手寫風格
- **做法**:
  - 透過 **Chars74k dataset** 提取字母並組合成羅馬數字
  - **OpenCV** 生成新數據（雜訊、筆畫模擬、膨脹字母）
  - 每個類別新增約 **70-90 張新影像**
- **影響**: 準確率進一步提升至 **75%**

#### **3️⃣ 影像清理（CleanVision）**
- **問題**:
  - 低資訊量（Low Information）
  - 過亮 / 過暗影像（Light/Dark）
  - 重複影像（Near Duplicates）
- **解決方案**:
  - **刪除 144 張低品質影像**
  - **標準化影像大小**
  - **對比度調整**
- **影響**: 提高模型對不同書寫風格的適應性

#### **4️⃣ 數據增強（Data Augmentation）**
- **目標**: 增加數據量，提高模型泛化能力
- **增強方式**:
  - **訓練集增強**
    - 隨機旋轉：±10%（36 度）
    - 隨機縮放：±20%
    - 隨機平移：±15%
    - 隨機對比度：0.1~0.2
  - **驗證集增強**
    - 旋轉範圍較小（±5%）
    - 縮放範圍較小（±10%）
    - 避免過度變形
- **影響**: 訓練集擴增至 **10503 張**，驗證集擴增至 **3265 張**

#### **5️⃣ 最終數據清理**
- 使用 **CleanVision** 再次檢測並清理增強後數據
- **刪除低資訊影像**
- **最終影像數量**:
  - 訓練集 **9000 張**
  - 驗證集 **2940 張**
- **測試集準確度提升至 80% 以上**

---

## 🏆 研究結果
- **影響模型準確度的主要因素**：
  1. **錯誤標籤修正**
  2. **影像清理（CleanVision）**
  3. **數據增強（Data Augmentation）**
- **最終測試集準確度達到 80% 以上**

---

## 🚀 未來展望
- **提升自動標籤修正**: 開發基於 AI 的自動化標籤修正工具
- **擴展數據集**: 加入更多不同字體與手寫風格
- **優化增強策略**: 嘗試 **GAN（生成對抗網路）** 生成手寫數字

---

## 🔧 技術與工具
- **Python**（pandas、numpy、matplotlib）
- **機器學習**（TensorFlow、Keras）
- **影像處理**（OpenCV、CleanVision）
- **數據增強**（TensorFlow Image Augmentation）

---

## 📂 專案結構
📂 RomanMNIST   
│── 📄 README.md # 本文件  
│── 📄 RomanMNIST.pdf # 研究報告 PDF 版本   
│── 📄 RomanMNIST_code.ipynb # 資料清理與擴增處理 Notebook   
│── 📄 RomanMNIST_reprt.pdf  # 簡報


---

## 📜 參考資料
- [Kaggle Dataset - Handwritten Roman Digits](https://www.kaggle.com/datasets/agneev/basedonenglishhandwrittencharactersmodified)
- [CleanVision 影像清理工具](https://www.cnblogs.com/luohenyueji/p/18499084)
- [Chars74k Dataset](https://www.kaggle.com/datasets/agneev/basedonenglishhandwrittencharactersmodified)
- [Preparing a Roman MNIST Dataset](https://agneevmukherjee.github.io/agneev-blog/preparing-a-Roman-MNIST/)

---

