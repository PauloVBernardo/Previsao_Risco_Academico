# 🎓 Previsão de Risco Acadêmico em Matemática com Machine Learning

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green)
![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)

## 📌 Visão Geral

Este projeto desenvolve um sistema de **previsão de risco acadêmico** aplicado à
disciplina de **Matemática**, tradicionalmente associada a altos índices de retenção
em instituições de ensino.

Utilizando dados de **notas e frequência ao longo dos quatro bimestres**, o sistema
classifica os estudantes em três categorias finais:

- 🟢 **Aprovado**
- 🟡 **Recuperação**
- 🔴 **Reprovado**

O diferencial do projeto está na **antecipação do risco**: a previsão é realizada
ao final do **3º bimestre**, permitindo que a escola atue preventivamente no último
período do ano letivo por meio de **intervenções pedagógicas orientadas por dados**.

---

## 🔄 Pipeline do Projeto

1. Geração de dados sintéticos acadêmicos
2. Análise exploratória e engenharia de atributos
3. Treinamento e avaliação de modelos de classificação
4. Geração de score de risco e visualização gerencial

---

## 1️⃣ Contexto

As taxas de aprovação escolar podem ser significativamente melhoradas quando a
instituição identifica dificuldades **ainda durante o ano letivo**, em vez de agir
apenas após o fechamento das notas finais.

Este projeto propõe um modelo de Machine Learning que:
- Utiliza dados acadêmicos dos **três primeiros bimestres**;
- Prevê a situação final do aluno em Matemática;
- Apoia a tomada de decisão pedagógica baseada em dados.

O sistema pode ser utilizado por coordenações pedagógicas para:
- Direcionar reforço escolar;
- Avaliar políticas de avaliação (provas x trabalhos);
- Reduzir taxas de reprovação em disciplinas críticas.

---

## 2️⃣ Objetivo

Desenvolver um sistema de previsão de risco acadêmico capaz de identificar,
ao final do **3º bimestre**, alunos com maior probabilidade de:

- 🟢 Aprovação
- 🟡 Recuperação
- 🔴 Reprovação

Permitindo a implementação de **ações pedagógicas direcionadas** no último
bimestre do ano letivo.

---

## 3️⃣ Dados

Os dados utilizados são **sintéticos**, gerados para fins educacionais e de
demonstração do pipeline completo de Data Science aplicado ao contexto escolar.

### 3.1 Estrutura de Avaliação (Matemática)

O ano letivo é dividido em **quatro bimestres**.  
Em cada bimestre, o aluno possui:

- 1 prova (valor máximo: 8 pontos)
- 2 trabalhos (valor máximo: 1 ponto cada)
- Frequência percentual no bimestre

**Nota máxima por bimestre:** 10 pontos  
**Nota final:** média das quatro notas bimestrais  
**Frequência final:** percentual total de presença no ano

### 3.2 Regras de Aprovação

| Classe        | Condição                                      |
|---------------|-----------------------------------------------|
| Aprovado      | nota_final ≥ 7 **e** frequência ≥ 75%         |
| Recuperação   | 5 ≤ nota_final < 7 **e** frequência ≥ 75%     |
| Reprovado     | nota_final < 5 **ou** frequência < 75%        |

---

## 🛠️ Desafios Técnicos & Soluções

- **Engenharia de Atributos:** criação de variáveis agregadas como
  `media_nota_b1_b3`, `media_freq_b1_b3` e `slope_nota`, que se mostraram mais
  informativas do que notas isoladas.
- **Desbalanceamento de Classes:** utilização de `class_weight='balanced'`
  para garantir que alunos em risco fossem adequadamente considerados.
- **Convergência de Modelos:** aplicação de `StandardScaler` e ajuste do
  `max_iter` na Regressão Logística para garantir estabilidade.

---

## 📊 Resultados e Performance

Foram comparados os modelos de **Regressão Logística** e **Random Forest**,
avaliados por meio de **Validação Cruzada (K-Fold)**.

| Modelo              | F1-Score (Macro) | Acurácia |
|---------------------|------------------|----------|
| Regressão Logística | 0.71             | 0.70     |
| Random Forest       | 0.64             | 0.70     |

### Principais Insights

- Variáveis agregadas de **frequência e média de notas** foram os principais
  preditores de risco.
- A frequência apresentou alta importância no modelo por ser um **critério
  institucional excludente**, apesar de possuir **baixa correlação direta (0.05)**
  com as notas no dataset sintético.
- O modelo aprende regras de aprovação, não relações pedagógicas causais —
  limitação reconhecida e documentada.

---

## 📈 Score de Risco e Dashboard

O modelo final gera um **score de risco acadêmico por aluno**, permitindo a
segmentação em **Baixo**, **Moderado** e **Alto Risco**.

Devido a limitações de compartilhamento do Power BI Service na versão gratuita,
o dashboard é disponibilizado em **formato PDF** neste repositório.

📄 **Dashboard (PDF):**  
`dashboard/risco_academico_dashboard.pdf`

O dashboard foi desenvolvido para apoiar a coordenação pedagógica na:
- Identificação de alunos prioritários;
- Análise de frequência e desempenho;
- Planejamento de intervenções acadêmicas.

---

## 📂 Estrutura do Repositório

```text
student-risk-prediction/
│
├── README.md
│
├── data/
│   ├── raw/
│   │   └── dados_academicos_bimestrais.csv
│   └── processed/
│       ├── dados_modelo_b1_b3.csv
│       └── dados_dashboard_risco.csv
│
├── notebooks/
│   ├── 01_data_generation.ipynb
│   ├── 02_eda_and_feature_engineering.ipynb
│   ├── 03_modeling_and_evaluation.ipynb
│   └── 04_risk_scoring_and_outputs.ipynb
│
├── dashboard/
│   └── risco_academico_dashboard.pdf
│
└── requirements.txt
```

## 🚀 Como Executar

### Clone o repositório:

git clone https://github.com/seu_usuario/student-risk-prediction


### Instale as dependências:

pip install -r requirements.txt


### Execute os notebooks na ordem numérica.

# ✒️ Autor

Paulo Vitor dos Santos Bernardo
🔗 LinkedIn