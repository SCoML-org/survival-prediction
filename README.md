# ICU 病患存活預測競賽

## 競賽簡介

這個競賽旨在透過機器學習技術預測重症加護病房（ICU）病患的存活情況。參賽者需要利用提供的病患資料，建立一個能夠準確預測病患是否存活的模型。這項研究對於提升醫療照護品質、優化醫療資源分配以及改善病患預後具有重要意義。

## 環境設置

### 必要套件安裝
我們建議使用 Conda 進行環境管理。如果你還沒有安裝 Conda，可以從 [Miniconda](https://docs.conda.io/en/latest/miniconda.html) 或 [Anaconda](https://www.anaconda.com/download) 下載安裝。

```bash
# 建立 conda 虛擬環境
conda create -n icu-survival python=3.9
conda activate icu-survival

# 安裝必要套件
conda install pandas=2.1.0 numpy=1.24.3 scikit-learn=1.3.0 jupyter=1.0.0 matplotlib=3.7.2 seaborn=0.12.2

# 或者使用 pip 安裝（如果某些套件在 conda 中找不到）
# pip install -r requirements.txt
```

requirements.txt 內容：
```
pandas==2.1.0
numpy==1.24.3
scikit-learn==1.3.0
jupyter==1.0.0
matplotlib==3.7.2
seaborn==0.12.2
```

## 提交方式

### 提交檔案格式
- 檔案名稱：submission.csv
- 檔案格式：CSV，需包含兩個欄位：
  - encounter_id：病患的唯一識別碼
  - hospital_death：預測結果（0表示存活，1表示死亡）
- 範例格式：
```csv
encounter_id,hospital_death
13622,0
3289,0
72644,0
1643,0
...
```

## Baseline 模型說明

我們提供了一個基礎的預測模型作為起點，這個模型採用了隨機森林演算法，並實作了基本的資料預處理流程。

### 資料預處理流程
在資料預處理階段，我們進行了以下處理：
1. 資料清理：
   - 移除對預測無關的識別欄位（如 encounter_id, patient_id 等）
   - 處理遺漏值：數值型特徵使用平均值填補，類別型特徵使用最常見值填補
2. 特徵轉換：
   - 將類別型特徵（如性別、種族、ICU類型等）轉換為數值編碼
   - 保留原始的數值型特徵

### 模型訓練與驗證
- 使用 scikit-learn 的 RandomForestClassifier
- 採用 5 折交叉驗證評估模型表現
- 模型效能：
  - 整體準確率達到約 93%
  - 對於存活病例的預測表現較好（召回率 99%）
  - 對於死亡病例的預測仍有改進空間（召回率 25%）

## 改進建議
1. 特徵工程：
   - 創建新的特徵組合
   - 處理特徵之間的相關性
   - 使用更進階的特徵選擇方法

2. 模型選擇：
   - 嘗試其他演算法（XGBoost, LightGBM 等）
   - 使用深度學習模型
   - 集成多個模型

3. 資料處理：
   - 處理資料不平衡問題
   - 使用更複雜的缺失值填補方法
   - 特徵標準化/正規化

## 參考資源
- [競賽網頁](https://scoml.org/competition/survival-prediction)
- [Discord 社群](https://discord.gg/3tupXYqXa8)
