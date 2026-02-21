# Detecção de Fraudes em Transações de Cartão de Crédito

Este repositório apresenta o desenvolvimento de um pipeline de Machine Learning para a detecção de transações fraudulentas, utilizando um dataset composto por variáveis transformadas via PCA ($V1$-$V28$) e atributos temporais/financeiros. O projeto foi desenvolvido com foco em **Robustez Experimental** e **Capacidade de Generalização**.

## 📊 Performance dos Modelos (Validação)

Após testes exaustivos com diferentes arquiteturas, os resultados obtidos no conjunto de validação (estratificado) foram:

| Modelo | ROC-AUC | Recall (Classe 1) | Justificativa de Escolha |
| :--- | :--- | :--- | :--- |
| **Regressão Logística** | 0.9729 | **0.87** | **Modelo Final**: Maior capacidade de captura de fraudes. |
| **Linear SVM** | **0.9730** | 0.48 | Alta precisão, mas Recall insuficiente para o negócio. |
| **Random Forest** | 0.9689 | 0.76 | Bom equilíbrio, mas superada pela Logística. |
| **XGBoost** | 0.9625 | 0.73 | Performance competitiva, porém mais complexa. |
| **MLP (Rede Neural)** | 0.5490 | 0.04 | Desempenho inadequado para dados desbalanceados. |

> **Nota Técnica:** A **Regressão Logística** foi selecionada como a solução campeã. Embora o SVM apresente uma ROC-AUC marginalmente superior, o Recall de **87%** da Logística é crítico para minimizar perdas financeiras por fraudes não detectadas.


## 🚀 Guia de Execução

Para reproduzir os resultados e gerar o arquivo de submissão final, siga rigorosamente as etapas abaixo:

### 1. Preparação dos Dados
* Baixe os arquivos `train.csv` e `test.csv` da plataforma da competição.
* Salve os arquivos localmente e adicione-os ao diretório do notebook de pré-processamento.

### 2. Geração dos Objetos de Dados (Pipeline)
* Acesse a pasta `EDA:pre-processamento/` e execute o notebook de pré-processamento.
* Este passo é essencial para realizar o escalonamento robusto, a engenharia de atributos e a limpeza dos dados.
* **Saída:** O notebook gerará os arquivos `dados_processados_dev.joblib` e `X_test_kaggle.joblib`, necessários para as próximas etapas.

### 3. Inferência e Submissão Final
* Acesse a pasta `modelo_final/` e execute o notebook de submissão.
* Este notebook foi criado especialmente para carregar o modelo treinado de **Regressão Logística** e os arquivos `.joblib` gerados anteriormente.
* **Resultado:** O notebook processará os dados de teste e gerará o arquivo CSV final para submissão direta no Kaggle.

---

## 📊 Metodologia e Escolha do Modelo

O projeto avaliou diversos algoritmos, incluindo SVM, Random Forest, XGBoost e Redes Neurais. O modelo final selecionado foi a **Regressão Logística** com os seguintes parâmetros:
* `C: 0.001`
* `penalty: 'l2'`
* `class_weight: 'balanced'`

## 🛠️ Requisitos
* Python 3.10+
* pandas
* scikit-learn
* joblib

---
