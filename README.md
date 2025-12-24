# 🎓 Sistema de Predição de Risco de Reprovação em Matemática com Machine Learning

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-ML-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green)
![PowerBI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-Latest-orange.svg)](https://scikit-learn.org/)

---

## 📌 Visão Geral
Este projeto desenvolve uma solução completa de ciência de dados para identificar alunos com risco de reprovação na disciplina de matemática. A solução abrange desde a simulação de dados educacionais realistas até a criação de um modelo preditivo de alta performance e um dashboard para tomada de decisão pedagógica.

Utilizando dados de notas e frequência até o fim do terceiro bimestre, o sistema classifica os estudantes em três categorias finais:

- 🟢 **Aprovado**
- 🟡 **Recuperação**
- 🔴 **Reprovado**

A grande vantagem deste projeto está na antecipação do risco: a previsão é realizada ao final do 3º bimestre, permitindo que a escola atue preventivamente no último período do ano letivo por meio de intervenções pedagógicas orientadas por dados.

---

## 📚 Índice
1. [Pipeline do Projeto](#-pipeline-do-projeto)  
2. [Objetivo](#-objetivo)  
3. [Dados e Dicionário de Dados](#-dados)  
4. [Engenharia de Atributos e Desafios Técnicos](#-engenharia-de-atributos-e-desafios-técnicos)  
5. [Modelos e Avaliação](#-modelos-e-avaliação)  
6. [Interpretação dos Resultados](#-interpretação-dos-resultados)  
7. [Score de Risco e Dashboard](#-score-de-risco-e-dashboard)  
8. [Estrutura do Repositório](#-estrutura-do-repositório)  
9. [Como Executar](#-como-executar)  
10. [Resultados e Próximos Passos](#-resultados-e-próximos-passos)  

---

## 🔄 Pipeline do Projeto
1. Geração de dados sintéticos acadêmicos  
2. Análise exploratória e engenharia de atributos  
3. Treinamento e avaliação de modelos de classificação  
4. Geração de score de risco e visualização gerencial  

---

## 2️⃣ Objetivo
Desenvolver um sistema de previsão de risco acadêmico capaz de identificar, ao final do 3º bimestre, alunos com maior probabilidade de:

- 🟢 Aprovação  
- 🟡 Recuperação  
- 🔴 Reprovação  

Permitindo a implementação de ações pedagógicas direcionadas no último bimestre do ano letivo.

---

## 3️⃣ Dados
Os dados utilizados são sintéticos, gerados para fins educacionais e de demonstração do pipeline completo de Data Science aplicado ao contexto escolar.

### Estrutura de Avaliação (Matemática)
- 1 prova (máx: 8 pontos)  
- 2 trabalhos (máx: 1 ponto cada)  
- Frequência percentual no bimestre  

**Nota máxima por bimestre:** 10 pontos  
**Nota final:** média das quatro notas bimestrais  
**Frequência final:** percentual total de presença no ano  

### Regras de Aprovação
| Classe        | Condição                                      |
|---------------|-----------------------------------------------|
| Aprovado      | nota_final ≥ 7 **e** frequência ≥ 75%         |
| Recuperação   | 5 ≤ nota_final < 7 **e** frequência ≥ 75%     |
| Reprovado     | nota_final < 5 **ou** frequência < 75%        |

### Dicionário de Dados
| Variável | Descrição | Tipo |
| :--- | :--- | :--- |
| `id_aluno` | Identificador único do estudante | Inteiro |
| `frequencia` | Percentual de presença nas aulas (0-100) | Float |
| `nota_b1`, `nota_b2`, `nota_b3`, `nota_b4` | Notas dos bimestres | Float |
| `nivel_socioeconomico` | Classificação da renda familiar (1 a 5) | Categórico |
| `risco_reprovacao` | Target: 1 para alto risco, 0 para baixo risco | Binário |

---

## 4️⃣ Engenharia de Atributos e Desafios Técnicos
- Criação de variáveis agregadas como `media_nota_b1_b3` e `media_freq_b1_b3`, mais informativas que notas isoladas.  
- Desbalanceamento de classes tratado com `class_weight='balanced'`.  
- Ajuste de hiperparâmetros (ex.: `max_iter` na Regressão Logística) para garantir convergência.  

---

## 5️⃣ Modelos e Avaliação
Foram comparados os modelos de Regressão Logística e Random Forest, avaliados por meio de validação cruzada K-Fold.

| Modelo              | F1-Score (Macro) | Acurácia |
|---------------------|------------------|----------|
| Regressão Logística | 0.69             | 0.70     |
| Random Forest       | 0.66             | 0.72     |

---

## 6️⃣ Interpretação dos Resultados
- Principais preditores: `media_freq_b1_b3` (0.20) e `media_nota_b1_b3` (0.16).  
- Frequência por bimestre mais relevante que provas isoladas.  
- Trabalhos têm menor impacto.  
- Idade e série quase irrelevantes.  

### Conclusão Pedagógica
O modelo sugere que intervenções baseadas na assiduidade desde o segundo bimestre podem ser mais eficazes para prevenir o risco acadêmico do que focar apenas na recuperação de notas baixas no final do ano. A frequência se destaca como critério institucional excludente, funcionando como forte indicador de reprovação.

---

## 7️⃣ Score de Risco e Dashboard
O modelo final gera um score de risco acadêmico por aluno, permitindo a segmentação em **Baixo**, **Moderado** e **Alto Risco**.

📄 **Dashboard (PDF):**  
`dashboard/risco_academico_dashboard.pdf`

O dashboard apoia a coordenação pedagógica na:  
- Identificação de alunos prioritários  
- Análise de frequência e desempenho  
- Planejamento de intervenções acadêmicas  

---

## 📂 Estrutura do Repositório
```text
Previsao_Risco_Academico/
│
├── README.md
├── data/
│   ├── raw/
│   │   └── dados_academicos.csv
│   └── processed/
│       ├── dados_academicos_processados.csv
│       └── dados_dashboard_final.csv
│       └── dados_dashboard_final.xls
├── notebooks/
│   ├── 01_data_generation.ipynb
│   ├── 02_eda_and_feature_engineering.ipynb
│   ├── 03_modeling_and_evaluation.ipynb
│   └── 04_risk_scoring_and_outputs.ipynb
├── dashboard/
│   └── Dashboard_risco_reprovacao_matematica.pdf
│   └── screenshots/
│       ├── visao_geral.png
│       └── perfil_risco.png
└── requirements.txt
```
---

## 🚀 Como Executar

**Clone o repositório:**
git clone https://github.com/PauloVBernardo/Previsao_Risco_Academico.git
cd Previsao_Risco_Academico

**Instale as dependências:**
pip install -r requirements.txt

**Execute os notebooks na ordem numérica.**

## ✅ Status do Projeto e Próximos Passos
Status: Finalizado. 

### Possíveis melhorias:
Explorar modelos adicionais (XGBoost, LightGBM).
Investigar relação entre frequência e notas para maior valor pedagógico.
Implementar versão interativa do dashboard em Power BI Service.

## 📬 Contato
👤 Autor: Paulo Vitor dos Santos Bernardo
📧 Email: pauloviti@gmail.com
🔗 [LinkedIn] (www.linkedin.com/in/paulo-vitor-bernardo)
