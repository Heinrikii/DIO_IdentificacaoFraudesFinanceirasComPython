# 🕵️‍♂️ Projeto de Detecção de Fraudes em Transações Financeiras

Este projeto tem como objetivo identificar **fraudes em transações financeiras** utilizando técnicas de **Machine Learning**.  
O fluxo foi construído em células estilo Jupyter Notebook, cada uma responsável por uma etapa específica.

---

## 📦 Importação e leitura dos dados
- Carregamos o dataset público de transações de cartão de crédito.
- Visualizamos os primeiros registros para entender a estrutura.

---

## 📊 Análise da variável alvo
- Verificamos a proporção de fraudes (`Class = 1`) e não fraudes (`Class = 0`).
- O dataset é **altamente desbalanceado** (menos de 1% de fraudes).

---

## ⚙️ Feature Engineering
- Criamos variáveis transformadas:
    - `Amount_log`: logaritmo do valor da transação.
    - `Amount_scaled`: normalização com `StandardScaler`.
- Isso ajuda os modelos a lidar melhor com escalas diferentes.

---

## 🔀 Split dos dados + Validação cruzada
- Dividimos os dados em treino e teste com `train_test_split`.
- Adicionamos **StratifiedKFold** para validação cruzada estratificada:
    - Garante que cada fold mantenha a proporção de fraudes e não fraudes.
    - Evita avaliações enviesadas.

---

## 🤖 Modelo base – Logistic Regression
- Treinamos um modelo simples de regressão logística.
- Avaliamos com métricas de classificação.

---

## 📈 Métricas adicionais
- Usamos métricas mais adequadas para dados desbalanceados:
    - **ROC Curve** e **AUC**.
    - **Precision-Recall Curve**.
- Isso mostra melhor o desempenho em detectar fraudes.

---

## ⚖️ Balanceamento dos dados
- Aplicamos duas técnicas:
    - **Undersampling**: reduz o número de não fraudes.
    - **SMOTE (Oversampling)**: gera exemplos sintéticos de fraudes.
- O objetivo é equilibrar a distribuição da variável alvo.

---

## 🧩 Ensemble de modelos
- Criamos um **VotingClassifier** combinando:
    - Logistic Regression
    - Random Forest
    - XGBoost
- O ensemble aumenta robustez e melhora recall.

---

## 🎯 Ajuste de threshold
- Alteramos o threshold de decisão para **0.25**.
- Isso torna o modelo mais sensível, reduzindo falsos negativos.
- Avaliamos com matriz de confusão normalizada.

---

## ⚡ Modelo XGBoost isolado
- Treinamos o XGBoost separadamente.
- O parâmetro `scale_pos_weight` ajuda a lidar com desbalanceamento.

---

## 🔍 Importância das variáveis
- Visualizamos quais features mais influenciam o modelo XGBoost.
- Isso ajuda na interpretação e explicabilidade.

---

## 🧩 Ajuste de hiperparâmetros
- Usamos **GridSearchCV** para testar diferentes combinações.
- Métrica de avaliação: **recall** (prioridade em detectar fraudes).

---

## 🧠 Explicabilidade com SHAP
- Aplicamos SHAP para entender o impacto das variáveis nas previsões.
- Permite explicar por que uma transação foi classificada como fraude.

---

# 🚀 Técnicas utilizadas
- **Pré-processamento**: normalização, transformação logarítmica.
- **Validação**: StratifiedKFold para manter proporções.
- **Modelos**: Logistic Regression, Random Forest, XGBoost.
- **Ensemble**: VotingClassifier para combinar modelos.
- **Balanceamento**: Undersampling e SMOTE.
- **Threshold tuning**: ajuste para aumentar recall.
- **Hiperparâmetros**: GridSearchCV.
- **Explicabilidade**: SHAP e análise de importância das variáveis.

---

## 📊 Fluxo do Projeto

![Fluxo de Detecção de Fraudes](https://copilot.microsoft.com/th/id/BCO.3492fb76-a4ac-47bf-a553-fb0cb0523d65.png)

---

## 🚀 Etapas do Pipeline

### 1️⃣ Coleta de Dados
- Dataset público de transações de cartão de crédito.
- Carregamento com `pandas`.

### 2️⃣ Pré-Processamento
- **Feature Engineering**:
  - `Amount_log`: transformação logarítmica.
  - `Amount_scaled`: normalização com `StandardScaler`.

### 3️⃣ Balanceamento de Dados
- **Undersampling**: reduz exemplos da classe majoritária.
- **SMOTE (Oversampling)**: gera exemplos sintéticos da classe minoritária.

### 4️⃣ Modelos Ensemble
- **VotingClassifier** combinando:
  - Logistic Regression
  - Random Forest
  - XGBoost  
    ➡️ Maior robustez e melhor recall.

### 5️⃣ Ajuste de Threshold
- Threshold ajustado para **0.25**.
- Torna o modelo mais sensível, reduzindo falsos negativos.

### 6️⃣ Avaliação
- Métricas utilizadas:
  - **Recall, Precision, F1-score**
  - **ROC Curve & AUC**
  - **Precision-Recall Curve**
  - **Matriz de Confusão Normalizada**

### 7️⃣ Importância das Variáveis
- Visualização das features mais relevantes no XGBoost.

### 8️⃣ Explicabilidade
- **SHAP**: explica o impacto das variáveis nas previsões.
- Transparência para analistas e stakeholders.

---

## 🧩 Técnicas Utilizadas
- **Pré-processamento**: normalização, transformação logarítmica.
- **Validação**: StratifiedKFold (garante proporções).
- **Modelos**: Logistic Regression, Random Forest, XGBoost.
- **Ensemble**: VotingClassifier.
- **Balanceamento**: Undersampling e SMOTE.
- **Threshold tuning**: ajuste para aumentar recall.
- **Hiperparâmetros**: GridSearchCV.
- **Explicabilidade**: SHAP e análise de importância das variáveis.

---

# 📊 Conclusão
Este projeto evoluiu de um protótipo inicial para um pipeline robusto, com técnicas modernas de balanceamento, ensemble e explicabilidade.  
O foco principal é **detectar o maior número possível de fraudes**, mesmo que isso aumente falsos positivos — pois o custo de não detectar uma fraude é muito maior.
