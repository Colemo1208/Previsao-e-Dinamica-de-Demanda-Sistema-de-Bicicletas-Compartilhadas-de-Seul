# Exame B – Previsão da Demanda de Bicicletas Compartilhadas

Neste exame, a avaliação acontece em formato de **competição**: em vez de uma prova tradicional, as duplas vão trabalhar com um problema real de ciência de dados, do início ao fim. O desafio é investigar um conjunto de dados sobre o sistema de bicicletas compartilhadas de Seul, na Coreia do Sul, e, a partir dele, desenvolver um modelo capaz de estimar quantas bicicletas serão alugadas em uma determinada hora, com base nas condições do tempo e do calendário.

O trabalho será feito em **duplas**, e passa por três momentos: exploração dos dados, validação de hipóteses com estatística inferencial e construção de um modelo de regressão.

---

## Sobre os dados

Os dados estão no arquivo **`bike_sharing.csv`**, que reúne cerca de 7 mil registros horários coletados entre dezembro de 2017 e novembro de 2018. Para cada hora há informações como temperatura, umidade, velocidade do vento, visibilidade, radiação solar, chuva e neve, além da estação do ano, da indicação de feriado e do funcionamento do sistema naquele dia.

A descrição completa de cada coluna, com unidades e faixas de valores, está em [**`data_description.md`**](data_description.md). Recomenda-se ler esse arquivo antes de começar.

---

## Etapas do trabalho

O exame está organizado em **três etapas**, cada uma com sua própria entrega. Os prazos serão divulgados no SIGAA.

### Etapa 1: Exploração dos Dados (ATUALMENTE ESTAMOS FOCADOS NESSA)

O ponto de partida é conhecer bem o dataset. Nesta etapa, a dupla deve examinar cada variável individualmente e, em seguida, observar como elas se relacionam, com foco principal em entender **o que faz a demanda (`Rented_Bike_Count`) subir ou cair**. Problemas de qualidade dos dados, categorias raras ou valores extremos também devem ser identificados aqui, já que influenciam diretamente as decisões das etapas seguintes.

- **Sugestões do que investigar:**

  - Medidas resumo (média, mediana, desvio padrão, assimetria) para as variáveis numéricas.
  - Tabelas de frequência para as variáveis categóricas, apontando categorias dominantes e pouco representadas.
  - Histogramas e *boxplots* para visualizar o formato das distribuições e localizar possíveis *outliers*.
  - Verificação da qualidade dos dados (valores ausentes, duplicados, valores implausíveis), com proposta de tratamento.
  - Gráficos de dispersão entre `Rented_Bike_Count` e as variáveis contínuas.
  - *Boxplots* ou *violin plots* para comparar a distribuição de `Rented_Bike_Count` entre as categorias de uma variável.
  - Matriz de correlação entre as variáveis numéricas, com interpretação dos resultados.
  - Um fechamento destacando quais variáveis parecem mais promissoras para o modelo.
- **O que entregar:**

  - Notebook com as análises, gráficos e comentários explicando cada passo e o que foi observado.

### Etapa 2: Testes de Hipótese (POSTERIOR)

Com o conhecimento adquirido na exploração, a dupla deve propor **pelo menos três hipóteses** sobre os dados e verificá-las usando testes estatísticos adequados.

- **Alguns exemplos de perguntas:**

  - A demanda por bicicletas é diferente entre as estações do ano?
  - Em feriados, a quantidade de bicicletas alugadas muda?
  - Existe relação entre as condições do tempo e a demanda?
- **O que entregar:**

  - Notebook apresentando cada hipótese, o teste escolhido, a verificação das suposições do teste e a conclusão obtida.

### Etapa 3: Construção do Modelo (POSTERIOR)

Na última etapa, os alunos deverão construir um modelo de regressão linear múltipla para prever os preços de venda das casas, ou seja, a variável dependente é `Rented_Bike_Count` e as demais podem ser usadas (todas ou apenas parte delas) como variáveis independentes.

- **O que fazer:**

  - Ajustar o modelo de **regressão linear**, testando diferentes combinações de variáveis e possíveis transformações.
  - Analisar os resíduos do modelo escolhido.
  - Avaliar a significância das variáveis por meio de ANOVA.
- **O que entregar:**

  - Notebook com:
    - O modelo final e a justificativa das escolhas feitas ao longo do processo
    - A análise dos resíduos

---

## Critérios de Avaliação

As três entregas serão corrigidas segundo os mesmos critérios:

1. **Qualidade Técnica** [4 pts]: o código funciona corretamente e aplica as técnicas vistas em aula?
2. **Clareza** [4 pts]: o notebook é bem organizado, com textos explicativos e gráficos fáceis de interpretar?
3. **Criatividade** [2 pts]: a dupla trouxe ideias próprias, abordagens diferentes ou análises que vão além do básico?

### Apresentações

Além dos notebooks, haverá apresentações em sala:

- Após a **Etapa 1 (ET01)**, metade das duplas, escolhida por sorteio, apresentará seus resultados.
- Após a **Etapa 2 (ET02)**, as duplas restantes apresentarão os resultados dessa etapa.
- A nota dessas apresentações entra como uma das atividades da disciplina (APR).

> Cada apresentação terá 10 minutos no total: 7 minutos de exposição e 3 minutos de perguntas. Um integrante, sorteado na hora, faz a apresentação, e o outro fica responsável por responder às perguntas do professor e dos colegas.

## Arguição Final (Nota do Exame B)

Depois da entrega da **Etapa 3 (ET03)**, cada aluno passará por uma arguição **individual** com o professor, em data e horário a serem definidos. A nota obtida nessa arguição será a nota do Exame B.

Como vai funcionar:

* **Quantidade de perguntas:** cada aluno responderá a **2 perguntas**.
* **Valor:** cada pergunta vale **5 pontos**.
* **Tempo:** 5 minutos por aluno.
* **Conteúdo:** fundamentos teóricos de regressão linear e o notebook entregue pela dupla na Etapa 3.

## Bônus da Competição

As duplas que quiserem disputar pontos extras devem incluir, ao final do notebook da Etapa 3, uma função que use o modelo já treinado para:

1. Ler um arquivo de teste cego chamado `TesteRegressao.csv`;
2. Gerar as previsões de `Rented_Bike_Count` para cada linha;
3. Salvar um novo CSV contendo **somente** os valores previstos, na mesma ordem das linhas do arquivo de teste, com o nome no formato `NOME_ALUNO1-NOME_ALUNO2.csv`.

> **Como testar antes de entregar:** o repositório traz o arquivo `exemplo.csv`, com as 5 primeiras linhas do teste oficial. Ele tem as mesmas colunas do dataset original, exceto `Rented_Bike_Count`. Basta renomeá-lo para `TesteRegressao.csv` no Colab e rodar a função para confirmar que o arquivo de saída é gerado sem erros.

> **Cuidado:** todo tratamento aplicado aos dados de treino (criação de variáveis, codificação, transformações) precisa ser aplicado da mesma forma ao arquivo de teste. Se a variável resposta tiver sido transformada, as previsões devem voltar para a escala original (número de bicicletas) antes de serem salvas.

O desempenho será medido pelo $R^2$ calculado sobre os dados de teste ocultos:

- **1º lugar:** +2 pontos no Exame B.
- **2º e 3º lugares:** +1 ponto no Exame B.

---

## Regras de Entrega

- Todos os notebooks devem ser desenvolvidos em Python no Google Colab e enviados pelo SIGAA.
- Não serão aceitas entregas fora do prazo.

---

## Considerações Finais

A ideia deste exame é aproximar a avaliação do que acontece no dia a dia de quem trabalha com dados: entender o problema, explorar, testar ideias e construir um modelo defensável. Aproveitem para trocar ideias com o colega de dupla, experimentar abordagens diferentes e, principalmente, aprender com o processo.

---

## Orientações de Formatação e Organização

### Organização do Notebook

* **Resumo inicial e seções:** comece o notebook com um pequeno resumo dos objetivos e do que foi feito. Cada seção deve ter um cabeçalho no padrão `## Seção X – Nome da Seção`. Vamos trabalhar começando uma seção querendo analisar algo para responder uma pergunta X, e no fim da seção ou de descobertas vamos apresentar o que observamos naquela analise
* **Hierarquia de títulos:** use os níveis de título do Markdown para deixar o notebook fácil de navegar, com `##` para as partes principais e `###` para os subtópicos. Por exemplo:

  * `## Etapa 1 – Análise Exploratória`
  * `### 1.1 Distribuição da Demanda`
* **Comentário no início de cada célula:** toda célula de código deve abrir com um comentário curto dizendo o que ela faz. Siga o padrão PEP8 (nomes descritivos, indentação correta e linhas de até 100 caracteres).

```python
  # Objetivo: Descrição sucinta
```

### Uso de Funções

* **Modularização:** organize o código em funções que representem as etapas do fluxo de trabalho (carregar dados, tratar, visualizar, modelar etc.). Não existe uma quantidade mínima, mas as funções devem evitar repetição de código e deixar claro o papel de cada parte da análise. Exemplo:

```python
def carregar_dados(caminho):
    """Lê o arquivo CSV e devolve um DataFrame."""
    # ...
    return df
```

* **Docstrings:** toda função deve ter uma docstring curta explicando o que faz, quais parâmetros recebe e o que retorna.

### Acompanhamento do Dataset

Depois de cada transformação importante nos dados, mostre como o dataset ficou antes e depois. Por exemplo:

```python
  print("Shape:", df.shape)
  print("Missing por coluna:\n", df.isna().sum())
  print("Estatísticas básicas:\n", df.describe().T)
```

### Justificativas

* Sempre que fizer algum tratamento nos dados (remoção de outliers, codificação, transformações, criação de variáveis), adicione uma célula Markdown com o título **Justificativa**, explicando o motivo da escolha com base teórica ou nos próprios dados.
* Quando apresentar textos de justificativas ou coisas assim use bullet points e textos em prosas. Pode destacar code
  usando `exemplo` de formatação, evite abusar de textos em negrito sem necessidade. Evite colocar o texto assim:

```markdown
### Conclusão Parcial e Transição para as Variáveis Numéricas

> **Constatação fundamental do aluno:**
> - Conforme suspeitado, em todos os dias em que o sistema esteve inativo (`Functioning_Day == 'No'`), a contagem de aluguéis é **estritamente zero** (`Rented_Bike_Count == 0`). Isso explica completamente diversos pontos nulos identificados na série temporal.
>
> **Próxima etapa investigativa:**
> - Com o funcionamento do sistema esclarecido e os fatores de calendário delimitados, a questão central agora é: **o que faz a demanda despencar em dias normais de funcionamento (`Functioning_Day == 'Yes'`), inclusive durante as estações quentes?**
> - A resposta provável reside nas **variáveis numéricas e meteorológicas** (temperaturas extremas, chuva torrencial, neve intensa, vento e umidade elevada).
> - Seguiremos a exploração com a análise detalhada das variáveis contínuas e sua correlação com `Rented_Bike_Count`.
```

### Reprodutibilidade

* Use **semente aleatória fixa** em todas as operações que envolvem aleatoriedade (`random_state=2025`).
* Mostre as **versões das bibliotecas** logo no início do notebook:

```python
  import pandas as pd, numpy as np, sklearn
  print(pd.__version__, np.__version__, sklearn.__version__)
```

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

Bom trabalho a todos, e que vença o melhor modelo!
