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
