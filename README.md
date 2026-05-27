# 🔍 Mineração de Dados — Criminalidade na Região de Piracicaba/SP

> Projeto da disciplina de **Mineração de Dados** — Análise de padrões criminais em 52 municípios da região de Piracicaba/SP utilizando K-Means e Regras de Associação (Apriori).

---

## 📌 Sobre o Projeto

Este projeto aplica técnicas de Mineração de Dados sobre dados reais de criminalidade fornecidos pela **Secretaria de Segurança Pública do Estado de São Paulo (SSP-SP)**, referentes ao ano de **2025**.

O objetivo é identificar agrupamentos de cidades com perfis criminais semelhantes e descobrir quais tipos de crime tendem a coocorrer na mesma cidade.

---

## 🗂️ Estrutura do Repositório

```
📁 mineracao-crimes-piracicaba/
│
├── 📄 codido_crimes.py                 # Código principal (K-Means + Apriori)
├── 📊 arquivo.xlsx                     # Base de dados — SSP-SP 2025
│
├── 📁 graficos/
│   ├── grafico_cotovelo.png            # Método do Cotovelo
│   ├── grafico_clusters.png            # Visualização dos clusters (PCA)
│   ├── heatmap_correlacao.png          # Correlação entre crimes
│   ├── outlier_rio_claro.png           # Rio Claro vs Cluster 1
│   └── zscore_rio_claro.png            # Z-Score de Rio Claro
│
├── 📁 resultados/
│   ├── clusters_resultado.csv          # Cluster de cada cidade
│   └── regras_associacao.csv          # Regras de associação geradas
│
├── 📄 relatorio_mineracao_crimes.pdf   # Relatório final completo
└── 📄 README.md
```

---

## 🗃️ Base de Dados

| Atributo | Valor |
|---|---|
| **Fonte** | SSP-SP — Secretaria de Segurança Pública |
| **Período** | Janeiro a Dezembro de 2025 |
| **Registros** | 1.196 linhas |
| **Municípios** | 52 cidades da região de Piracicaba/SP |
| **Tipos de crime** | 18 naturezas (após remoção de redundâncias) |
| **Formato** | Excel (.xlsx) |

---

## ⚙️ Metodologia

### 🔵 Agrupamento — K-Means

```
Dados → Pré-processamento → Normalização → Cotovelo → K-Means (k=3) → Avaliação
```

| Etapa | Detalhe |
|---|---|
| Pré-processamento | Pivot Table, remoção de redundâncias |
| Normalização | StandardScaler (média=0, desvio=1) |
| Definição do k | Método do Cotovelo + Silhouette Score |
| Avaliação | Silhouette Score = **0,52** ✅ |
| Visualização | PCA 2D |

### 🟠 Regras de Associação — Apriori

| Parâmetro | Valor | Justificativa |
|---|---|---|
| Suporte mínimo | 0,70 | Crime presente em ≥70% das cidades |
| Confiança mínima | 0,80 | ≥80% de confiabilidade preditiva |
| Lift | > 1,0 | Apenas associações reais |
| Max itemsets | 3 | Legibilidade das regras |
| **Regras geradas** | **287** | — |

---

## 📊 Resultados

### Clusters Identificados

| Cluster | Perfil | Cidades | Exemplos |
|---|---|---|---|
| **0** | 🟡 Média criminalidade | 8 | Araras, Leme, Nova Odessa |
| **1** | 🔴 Alta criminalidade | 6 | Piracicaba, Americana, Limeira, Sumaré, Rio Claro |
| **2** | 🟢 Baixa criminalidade | 38 | Demais municípios menores |

### Top Regras de Associação

```
SE homicídio culposo trânsito + roubo → ENTÃO tentativa de homicídio
   Suporte: 71% | Confiança: 94,9% | Lift: 1,20
```

### 🔎 Outlier — Rio Claro

Rio Claro se destaca como outlier dentro do Cluster 1 com **Z-score de 4,02** em homicídio doloso e **3,07** em lesão corporal culposa por acidente de trânsito — valores muito acima da média das demais cidades do mesmo grupo.

| Crime | Z-Score | Classificação |
|---|---|---|
| Homicídio doloso por acidente de trânsito | 7,14 | 🔴 Outlier severo |
| Homicídio doloso | 4,02 | 🔴 Outlier severo |
| Homicídio culposo outros | 3,40 | 🔴 Outlier severo |
| Lesão corp. culposa por acidente de trânsito | 3,07 | 🔴 Outlier severo |
| Tentativa de homicídio | 2,51 | 🔴 Outlier severo |
| Latrocínio | 2,36 | 🔴 Outlier severo |

---

## 🛠️ Tecnologias Utilizadas

![Python](https://img.shields.io/badge/Python-3.13-blue?logo=python)
![pandas](https://img.shields.io/badge/pandas-data--manipulation-150458?logo=pandas)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikit-learn)
![mlxtend](https://img.shields.io/badge/mlxtend-Apriori-green)
![matplotlib](https://img.shields.io/badge/matplotlib-charts-blue)
![seaborn](https://img.shields.io/badge/seaborn-visualization-teal)

| Biblioteca | Uso |
|---|---|
| `pandas` | Manipulação dos dados, pivot table |
| `numpy` | Operações matemáticas, binarização |
| `scikit-learn` | KMeans, StandardScaler, PCA, Silhouette |
| `mlxtend` | Apriori, association_rules |
| `matplotlib` + `seaborn` | Visualizações e gráficos |
| `openpyxl` | Leitura do arquivo Excel |

---

## 🚀 Como Executar

### 1. Clone o repositório
```bash
git clone https://github.com/seu-usuario/seu-repositorio.git
cd seu-repositorio
```

### 2. Crie e ative o ambiente virtual
```bash
python3 -m venv venv
source venv/bin/activate  # Mac/Linux
```

### 3. Instale as dependências
```bash
pip install pandas numpy scikit-learn mlxtend matplotlib seaborn openpyxl
```

### 4. Execute o código
```bash
python codido_crimes.py
```

### 5. Arquivos gerados automaticamente
```
grafico_cotovelo.png
grafico_clusters.png
heatmap_correlacao.png
outlier_rio_claro.png
zscore_rio_claro.png
clusters_resultado.csv
regras_associacao.csv
```

---

## 📚 Referências

- SSP-SP — Secretaria de Segurança Pública do Estado de São Paulo. Disponível em: [www.ssp.sp.gov.br](http://www.ssp.sp.gov.br)
- HAN, J.; KAMBER, M.; PEI, J. *Data Mining: Concepts and Techniques*. 3. ed. Morgan Kaufmann, 2011.
- ROUSSEEUW, P. J. Silhouettes: a graphical aid to the interpretation and validation of cluster analysis. *Journal of Computational and Applied Mathematics*, v. 20, p. 53-65, 1987.
- Scikit-learn Documentation: [scikit-learn.org](https://scikit-learn.org)
- Mlxtend Documentation: [rasbt.github.io/mlxtend](https://rasbt.github.io/mlxtend)

---

## 👥 Equipe

Projeto desenvolvido para a disciplina de **Mineração de Dados** — 2025.
Felippe Santuzzi e Paulo Algusto da Fonceseca
Professora: Angela Locatteli Godoy - Fatec Rio Claro SP

---

<p align="center">
  Feito com 🔍 dados reais e 🐍 Python
</p>
