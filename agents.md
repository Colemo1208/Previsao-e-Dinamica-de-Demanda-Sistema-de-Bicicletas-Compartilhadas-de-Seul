# AGENTS.md – Diretrizes para Agentes de IA

Este documento orienta agentes de IA no auxílio ao desenvolvimento do projeto acadêmico **Exame B – Previsão da Demanda de Bicicletas Compartilhadas**.

---

## 1. Visão Geral do Projeto

- **Contexto:** Trabalho acadêmico universitário (UFPA) em formato de competição de Ciência de Dados.
- **Objetivo:** Investigar o dataset do sistema de bicicletas públicas de Seul (Coreia do Sul) e desenvolver um modelo de regressão linear para prever a quantidade horária de bicicletas alugadas (`Rented_Bike_Count`).
- **Arquivo principal de análise:** `EXAME_B.ipynb`.
- **Arquivos de referência:**
  - `README.md`: Instruções completas, regras de entrega e critérios de avaliação.
  - `data_description.md`: Descrição das variáveis, unidades e tipos.

---

## 2. Estrutura das Etapas da Disciplina

1. **Etapa 1 – Exploração dos Dados (EDA):**
   - Medidas descritivas (média, mediana, desvio padrão, assimetria).
   - Frequência de categóricas e identificação de classes raras.
   - Histogramas, *boxplots*, *violin plots* e *scatter plots*.
   - Tratamento de qualidade de dados (nulos, duplicados, inconsistências).
   - Matriz de correlação e interpretação.
   - Síntese de variáveis mais promissoras.

2. **Etapa 2 – Testes de Hipótese:**
   - No mínimo 3 hipóteses estatísticas bem delineadas (H₀ e H₁).
   - Nível de significância definido (ex: $\alpha = 0,05$).
   - Verificação prévia de suposições dos testes (normalidade, homocedasticidade, etc.).
   - Apresentação de estatística do teste, p-valor e interpretação prática em tabela.

3. **Etapa 3 – Modelagem Preditiva:**
   - Modelo de **Regressão Linear Múltipla**.
   - Análise de significância das variáveis via ANOVA e valores-p.
   - Diagnóstico dos resíduos (normalidade, homocedasticidade, independência).
   - Função final de inferência para teste cego (`TesteRegressao.csv`) sem vazamento de dados (*data leakage*).

---

## 3. Padrões de Código e Requisitos Obrigatórios

Qualquer contribuição ou sugestão de código nos notebooks deve seguir rigorosamente:

- **Comentário de abertura em células de código:**
  ```python
  # Objetivo: Descrição sucinta da finalidade desta célula
  ```
- **Modularização e Funções:**
  - Criar funções para operações reutilizáveis (carregamento, pré-processamento, plotagem, métricas).
  - Toda função deve possuir *docstring* concisa (descrição, parâmetros e retorno).
- **Acompanhamento do Dataset:**
  - Exibir o estado antes e depois de alterações estruturais (`df.shape`, `df.isna().sum()`, etc.).
- **Justificativas:**
  - Sempre acompanhar tratamentos de dados e transformações com explicações teóricas ou empíricas.
- **Reprodutibilidade:**
  - Semente aleatória padrão: `random_state=2025`.
  - Exibir versões das bibliotecas no início do notebook:
    ```python
    import pandas as pd, numpy as np, sklearn
    print(pd.__version__, np.__version__, sklearn.__version__)
    ```
- **Estilo:** PEP 8, limite visual de 100 caracteres por linha, nomes de variáveis autoexplicativos.

---

## 4. Ambiente e Ferramentas

O ambiente do projeto é gerenciado via **`uv`**:

- **Ambiente Virtual:** `.venv/`
- **Comando de execução:** `uv run python ...`
- **Kernel Jupyter:** `Python (EXAME B - uv)` (instalado como `exame-b`)
- **Bibliotecas Principais:**
  - Manipulação & Análise: `pandas`, `numpy`
  - Visualização: `matplotlib`, `seaborn`
  - Estatística & Modelagem: `scipy`, `statsmodels`, `scikit-learn`
  - Notebook: `ipykernel`

---

## 5. Instruções de Comportamento para o Agente

1. **Foco Pedagógico e Crítico:** Não entregue respostas prontas sem fundamentação estatística. Explique *por que* uma técnica foi escolhida (ex.: quando usar Pearson vs. Spearman, ou log-transform na variável alvo).
2. **Prevenção de Erros Comuns:**
   - Garantir que transformações no conjunto de treino sejam aplicáveis aos dados de teste sem gerar vazamento (*data leakage*).
   - Cuidar da multicolinearidade (ex.: `Temperature` vs. `Dew_Point_Temperature`).
   - Evitar a armadilha das variáveis dummy (*dummy variable trap*).
3. **Respeito aos Critérios de Avaliação:** Priorizar clareza visual nos gráficos (títulos, rótulos de eixos legíveis, paleta coerente) e coerência com a rubrica da disciplina.
