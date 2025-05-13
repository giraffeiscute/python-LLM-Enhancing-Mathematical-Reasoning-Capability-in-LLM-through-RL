# 使用 GRPO 增強小型語言模型的數學推理能力
本專案探討如何透過強化學習技術，提升小型語言模型在數學推理任務中的表現。研究重點為使用 Group Relative Policy Optimization（GRPO） 方法，並結合多種自定義獎勵函數，在 GSM8K 數據集上優化 Chain-of-Thought（CoT）生成效果。

## 專案背景
小型語言模型在處理複雜推理任務時常因參數量有限而表現不佳。然而，透過 GRPO 等強化學習方法及人類回饋（RLHF），可大幅提升其邏輯推理能力，甚至在部分任務上逼近大型封閉模型（如 GPT-4）的表現。

我們的實驗採用了 Qwen2.5-0.5B-Instruct 模型，一款開源且具商用授權的小型語言模型。

## 研究目標
1. 提升小型 LLM 處理算術與邏輯推理任務的能力

2. 探討不同獎勵設計對模型訓練的影響

3. 比較單例提示與格式強制下的效能差異

4. 分析推理長度與答題正確率之間的關係

## 自定義獎勵函數
格式獎勵：

strict_format_reward_func：完整包含 <reasoning> 與 <answer> 才得分

soft_format_reward_func：允許較鬆散的 XML 結構

count_xml：根據正確標籤數給予部分得分

正確率獎勵：

correctness_reward_func：僅正確答案獲得獎勵

int_reward_func：整數答案額外加分

推理長度獎勵：

依據 token 長度與理想範圍的 cosine 相似度給予獎勵

## 實驗設計
共進行四組主要實驗：

| 實驗編號 | 提示方式       | 獎勵策略           | 備註                 |
| ---- | ---------- | -------------- | ------------------ |
| Exp1 | 無提示        | 標準獎勵           | 格式不合，表現最差          |
| Exp2 | 有 One-shot | 標準獎勵           | 格式與正確率最佳           |
| Exp3 | 有 One-shot | 含懲罰 cosine 獎勵  | 過度懲罰導致準確率下降        |
| Exp4 | 有 One-shot | 不含懲罰 cosine 獎勵 | 表現優於 Exp3，但不及 Exp2 |

![image](https://github.com/giraffeiscute/python-LLM-Enhancing-Mathematical-Reasoning-Capability-in-LLM-through-RL/blob/main/chart/%E5%9C%96%E7%89%871.png)
![image](https://github.com/giraffeiscute/python-LLM-Enhancing-Mathematical-Reasoning-Capability-in-LLM-through-RL/blob/main/chart/%E5%9C%96%E7%89%872.png)

**實驗小結**
1. 缺少提示會導致模型無法生成正確格式

2. 過度依賴懲罰型獎勵可能導致推理結構混亂或答案錯誤


📈 重要發現
1. 提供例子 (one-shot) 能顯著提升格式與正確性

2. 過度懲罰會降低模型表現，特別是小模型

3. 推理長度與答對率呈正相關趨勢（尚需更多驗證）

4. 強化學習可有效改善結構化推理生成

👥 作者
楊致遠 Chih-Yuan Yang
研究領域：大型語言模型、機器學習
指導教授：陳偉堅 教授

李林晁 Li Linchao
研究領域：大型語言模型、擴散模型
指導教授：陳偉堅 教授
