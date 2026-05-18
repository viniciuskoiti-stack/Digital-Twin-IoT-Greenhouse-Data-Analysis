# 🔧 Projeto: Gêmeo Digital (Digital Twin) e Analytics para Agricultura de Precisão

> Projeto desenvolvido para a disciplina de Ciência de Dados, focado na aplicação da Indústria 4.0 na agricultura. O objetivo é utilizar telemetria IoT contínua para mapear processos biológicos em ambientes controlados e, por meio de Machine Learning, realizar a predição da biomassa vegetal para controle preditivo em malha fechada.

![Status do Projeto](https://img.shields.io/badge/Status-Conclu%C3%ADdo%20/%20M4-brightgreen)
![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Modelagem-orange?logo=scikit-learn)
![Google AI Studio](https://img.shields.io/badge/Google%20AI%20Studio-Dashboard-purple)

---

# 👥 1. Identificação do Grupo

- Instituição: Centro Educacional da Fundação Salvador Arena
- Curso: Engenharia de Controle e Automação
- Disciplina: Ciência de Dados
- Grupo: B

## Integrantes

- Jhuan Henrique Luz Dias — RA: 062210023
- Lucas Veiga Bezerra — RA: 062210006
- Yasmin Souza Correia — RA: 062210008
- Tifany Mariane Ferreira — RA: 062210019
- Vinicius Koiti Vila Nova Tsuchiya — RA: 062210022

---

# 🎯 2. Área-Problema Selecionada

O grupo selecionou a área de Gêmeos Digitais (Digital Twins) e Analytics em Tempo Real.

## ✅ Recorte do Projeto

Predição em tempo real da biomassa úmida (peso) de plantas em estufas inteligentes, utilizando variáveis morfológicas monitoradas por telemetria IoT para fundamentar sistemas de controle orientados a dados (data-driven control).

## 📌 Justificativa e Hipótese

Sensores físicos para medição direta de biomassa são invasivos, caros e de difícil calibração em larga escala. A hipótese central do projeto é que variáveis indiretas, como Área Foliar e Nível de Clorofila, possuem forte correlação com a biomassa vegetal, permitindo que algoritmos de Machine Learning atuem como sensores virtuais de alta precisão.

---

# 🧩 3. Diagnóstico e Definição do Problema

- Problema: A elevada quantidade de dados provenientes da instrumentação IoT agrícola carrega ruídos de leitura, perdas de pacote e outliers, dificultando a extração de variáveis fisiológicas confiáveis para controle preditivo.

- Impacto: A utilização de um pipeline robusto de tratamento de dados aliado a modelos preditivos permite maior eficiência no acionamento de atuadores, redução de desperdícios hídricos e energéticos e aumento da produtividade agrícola.

---

# 🗂️ 4. Arquitetura de Dados (Fonte e Dataset)

- Origem: Advanced IoT Dataset — Tikrit University
- Características: Dataset real de laboratório contendo aproximadamente 30.000 amostras telemétricas.
- Variáveis Principais:
  - Average leaf area of the plant (ALAP)
  - Average of chlorophyll in the plant (ACHP)
  - Plant height rate (PHR)

- Variável Alvo:
  - Average wet weight of the growth vegetative (AWWGV)

---

# 🔄 5. Plano de Tratamento de Dados (ETL)

O pipeline de dados segue as seguintes etapas:

## 1. Extração

Leitura da base de dados bruta localizada na pasta /data/raw.

## 2. Transformação

- Remoção de valores nulos
- Tratamento de falhas de leitura
- Aplicação do método estatístico IQR (Interquartile Range)
- Supressão de outliers elétricos e mecânicos

## 3. Carga

Armazenamento dos dados tratados em /data/processed para utilização pelo modelo preditivo.

---

# 📈 6. Desenvolvimento e Otimização (M2, M3 e M4)

## 🔍 M2 — Análise Exploratória (EDA)

A análise exploratória permitiu identificar:

- Correlação direta entre Área Foliar (ALAP) e Biomassa Vegetal (AWWGV)
- Relação entre Clorofila e Taxa de Crescimento
- Estabilidade superior em sistemas Smart IoT
- Viabilidade do modelo preditivo baseado em sensores indiretos

---

## 🤖 M3 — Modelagem de IA

Foi implementada uma arquitetura híbrida composta por:

### Camada de Predição Matemática

Modelo RandomForestRegressor treinado com os dados pós-ETL.

### Camada de Decisão Inteligente

Interface desenvolvida no Google AI Studio responsável por:

- Receber as variáveis telemétricas
- Interpretar o estado fisiológico da planta
- Gerar diagnósticos e comandos atuados em formato JSON

---

## ⚙️ M4 — Refinamento e Otimização Profissional

### Ajuste de Hiperparâmetros

Utilização do GridSearchCV para busca das melhores configurações matemáticas do modelo:

- max_depth = 10
- min_samples_split = 10
- n_estimators = 150

### Cross-Validation

Aplicação de validação cruzada (cv=5) para garantir robustez estatística e evitar overfitting.

### Engenharia de Atributos (Feature Importance)

As variáveis mais relevantes identificadas foram:

| Variável | Importância |
|---|---|
| ACHP | 56.2% |
| PHR | 35.4% |
| ALAP | 5.4% |
| ANPL | 2.8% |

---

## 📊 Métricas Finais do Modelo Otimizado

| Métrica | Resultado |
|---|---|
| MAE | 0.0080 |
| RMSE | 0.0099 |
| R² | 99.84% |

Os resultados demonstram elevada capacidade preditiva e aderência industrial do modelo.

---

# 🖥️ 7. Dashboard de Monitoramento

Interface visual implementada utilizando Google AI Studio.

## Funcionalidades

- Entrada manual de variáveis telemétricas
- Predição da biomassa vegetal
- Diagnóstico fisiológico
- Sugestão automática de atuação
- Exibição de métricas do modelo
- Respostas estruturadas em JSON

## Link do Protótipo

https://ai.studio/apps/d653c259-1129-46ca-b39a-37cc9c24b35f?fullscreenApplet=true

---

# 🧱 8. Estrutura do Repositório

Organização das pastas conforme o padrão profissional exigido:

```bash
/
├── data/               # Conjuntos de dados
│   ├── raw/            # Arquivo CSV original (imutável)
│   └── processed/      # Arquivo CSV tratado após filtro IQR (ETL)
│
├── docs/               # Documentação técnica e Apêndice de IA
│
├── images/             # Screenshots do dashboard (Agritwin) e diagramas (Matriz de Correlação)
│
├── notebooks/          # Notebooks Jupyter (Ambiente de Experimentação)
│   ├── M2_EDA.ipynb    # Etapa 2: Análise Exploratória e ETL
│   ├── M3_ML.ipynb     # Etapa 3: Modelagem Inicial de Machine Learning
│   ├── M4_Otimizacao.ipynb # Etapa 4: Refinamento, GridSearch e Cross-Validation
│   └── n1_individual/  # Diretório para os testes estatísticos de cada integrante
│
├── scripts/            # Código-fonte principal de produção (Scripts .py)
│   ├── etl.py          # Script isolado para processamento de dados
│   ├── train_model.py  # Script isolado para treino do modelo final otimizado
│   └── logica_decisao_ia.py  # Integração do Gêmeo Digital com IA (Google AI Studio)
│
├── requirements.txt    # Lista de bibliotecas essenciais para reprodução
└── README.md           # Documentação principal e guia de correção
```

---

# 🚀 9. Instruções para Execução

Para reproduzir o ambiente e executar o projeto, siga os passos abaixo:

## 1. Clonar o Repositório e Acessar o Diretório
Abra o seu terminal e execute:
```bash
git clone https://github.com/viniciuskoiti-stack/Digital-Twin-IoT-Greenhouse-Data-Analysis.git
```

## 2. Instalar Dependências
Certifique-se de ter o Python instalado (3.9+). Execute:
```bash
pip install -r requirements.txt
```

## 3. Execução via Notebooks (Experimentação)
Abra o Jupyter ou Colab e execute os arquivos na ordem lógica:
1. notebooks/M2_EDA.ipynb
2. notebooks/M3_ML.ipynb
3. notebooks/M4_Otimizacao.ipynb

## 4. Execução via Scripts (Produção)
Execute via terminal na ordem abaixo:

Passo A: Processamento de Dados (ETL)
```bash
python scripts/etl.py
```

Passo B: Treinamento e Otimização do Modelo
```bash
python scripts/train_model.py
```

Passo C: Gêmeo Digital (Integração IA)
```bash
python scripts/logica_decisao_ia.py
```

---

# 🧪 10. Entregas Individuais (Estatística, Robustez e XAI)

Esta seção centraliza as contribuições e investigações técnicas realizadas individualmente por cada membro do grupo, divididas entre a validação estatística inferencial e a auditoria de robustez dos modelos de IA.

## 10.1 — Aprofundamento Estatístico (Inferência)
Validação das hipóteses de correlação levantadas na etapa exploratória (EDA), aplicando testes de normalidade (Shapiro-Wilk) e testes de hipóteses paramétricos/não-paramétricos.

| Integrante | Variável Analisada | Teste Estatístico Realizado | Link do Notebook |
| :--- | :--- | :--- | :--- |
| Jhuan Henrique | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/Aprofundamento_Estatistico_Jhuan.ipynb) |
| Lucas Veiga | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/Aprofundamento_Estatistico_Lucas.ipynb) |
| Yasmin Souza | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/Aprofundamento_Estatistico_Yasmin.ipynb) |
| Tifany Mariane | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/Aprofundamento_Estatistico_Tifany.ipynb) |
| Vinicius Koiti | ACHP x Biomassa | Mann-Whitney e d de Cohen | [Notebook](notebooks/n1_individual/Aprofundamento_Estatistico_Vinicius_Koiti.ipynb) |

* **Resumo dos Resultados (Vinicius Koiti):** Validou-se estatisticamente que o nível de Clorofila (ACHP) influencia significativamente a biomassa úmida. O teste de Shapiro-Wilk rejeitou a normalidade das amostras (p-valor < 0.05), justificando o uso do teste de Mann-Whitney, que rejeitou a hipótese nula (H0) com p-valor < 0.001. O Tamanho do Efeito (Cohen's d = 0.73) confirmou uma relevância prática de magnitude média-alta, validando a Clorofila como um dos principais preditores para o Gêmeo Digital.

---

## 10.2 — Auditoria de Robustez e Interpretabilidade (XAI)
Testes de estresse com injeção de ruído artificial (5%, 10% e 20%) nos sensores principais, análise de resíduos das maiores falhas e aplicação da biblioteca SHAP para interpretabilidade local (Casos de Sucesso vs. Falha).

| Integrante | Sensores Testados | Algoritmo de Explicabilidade | Link do Notebook |
| :--- | :--- | :--- | :--- |
| Jhuan Henrique | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/N1_Jhuan.ipynb) |
| Lucas Veiga | ACHP, PHR e ALAP | Stress Test e SHAP | [Notebook](notebooks/n1_individual/N1_Lucas_Veiga.ipynb) |
| Yasmin Souza | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/N1_Yasmin.ipynb) |
| Tifany Mariane | [PREENCHER] | [PREENCHER] | [Notebook](notebooks/n1_individual/N1_Tifany.ipynb) |
| Vinicius Koiti | ACHP, PHR, ALAP e ANPL | SHAP (Waterfall) e Stress | [Notebook](notebooks/n1_individual/N1_Vinicius_Koiti.ipynb) |

* **Resumo dos Resultados (Vinicius Koiti):** Através de uma auditoria de XAI, identificou-se que o modelo possui um viés de ancoragem na variável Clorofila (ACHP). Testes de estresse revelaram que ruídos acima de 15% nos sensores causam uma degradação crítica na predição. A análise via SHAP isolou casos extremos, resultando em um plano de ação que sugere filtros digitais no CLP e redundância de sensores para mitigar falhas de leitura em cenários de estresse térmico.

---

# 🎥 11. Demonstração do Projeto

## Pitch e Demonstração (2–3 min)

[COLE_AQUI_O_LINK_DO_VIDEO]

O vídeo apresenta:

- Estrutura do projeto
- Pipeline ETL
- Modelo Random Forest
- Métricas finais
- Otimização M4
- Interface no AI Studio
- Funcionamento do Gêmeo Digital

---

# 🤖 12. Apêndice de IA

## Ferramentas Utilizadas

- Google Gemini
- Google AI Studio

## Aplicações da IA

As ferramentas de IA auxiliaram:

- Estruturação do código Python
- Organização do pipeline ETL
- Revisão da sintaxe Scikit-Learn
- Criação de prompts JSON
- Organização do GitHub
- Estruturação do Dashboard

## Processo de Validação

Todas as decisões técnicas foram verificadas manualmente pelo grupo.

Foram auditados:

- Método IQR
- Cross-Validation
- GridSearchCV
- Métricas industriais
- Importância das variáveis
- Resultados do modelo

Nenhuma decisão técnica foi aplicada automaticamente sem validação humana.

---

© 2026 — Projeto de Ciência de Dados — Faculdade Engenheiro Salvador Arena
