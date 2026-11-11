# Previsao e Dinamica de Demanda: Sistema de Bicicletas Compartilhadas de Seul

![Python](https://img.shields.io/badge/Python-3.12-3776AB?style=flat&logo=python&logoColor=white)
![Data Analysis](https://img.shields.io/badge/Data%20Analysis-Exploratory-21918c?style=flat)
![Visualizacao](https://img.shields.io/badge/Visualizacao-Seaborn%20%7C%20Matplotlib-31688e?style=flat)
![Status](https://img.shields.io/badge/Status-Etapa%201%20Concluida-brightgreen?style=flat)

Um estudo aprofundado de ciencia e analise exploratoria de dados sobre os fatores operacionais, meteorologicos e sazonais que determinam os volumes de locacao do sistema publico de bicicletas compartilhadas de Seul (Coreia do Sul).

---

## Visao Geral e Problema de Negocio

Sistemas de micromobilidade e compartilhamento de bicicletas urbanas enfrentam o desafio constante de rebalanceamento logistico de frotas e previsao de demanda horaria. Flutuacoes abruptas causadas pelo clima ou pelo calendario podem gerar estacoes saturadas ou vazias, impactando diretamente a receita e a satisfacao da populacao.

Este projeto investiga o comportamento dos usuarios a partir de uma base horaria contendo mais de 7 mil registros ao longo de um ano completo, respondendo a pergunta central de negocio: **o que faz a demanda (`Rented_Bike_Count`) subir ou cair drasticamente?**

---

## Caracteristicas do Dataset

Os dados originais compreendem registros horarios continuos coletados entre **1 de dezembro de 2017 e 30 de novembro de 2018** em Seul.

* **Volume de Observacoes:** 7.008 linhas horarias (365 dias de monitoramento).
* **Variavel Dependente (Alvo):** `Rented_Bike_Count` (quantidade de bicicletas alugadas em cada intervalo de 1 hora).
* **Variaveis Meteorologicas:**
  * Temperatura do ar (`Temperature` em °C)
  * Ponto de orvalho (`Dew_Point_Temperature` em °C)
  * Umidade relativa do ar (`Humidity` em %)
  * Velocidade do vento (`Wind_Speed` em m/s)
  * Visibilidade horizontal (`Visibility` em 10m)
  * Radiacao solar incidente (`Solar_Radiation` em MJ/m²)
  * Precipitacao acumulada de chuva (`Rainfall` em mm/h)
  * Precipitacao acumulada de neve (`Snowfall` em cm/h)
* **Variaveis Temporais e de Calendario:**
  * Data e hora do registro (`Date` e `Hour`, de 0 a 23h)
  * Estacao climatica do ano (`Seasons`: Inverno, Primavera, Verao, Outono)
  * Indicador de feriado oficial (`Holiday`: Holiday vs. No Holiday)
  * Indicador de disponibilidade operacional (`Functioning_Day`: Yes vs. No)

---

## Metodologia de Exploracao e Tecnicas Empregadas

1. **Qualidade e Sanitizacao:**
   - Inspecao de tipos primitivos, ausencia de valores nulos e estruturacao temporal no formato padrao ISO.
   - Criacao de features derivadas: tipo de dia (`Day_Type`: dia util vs. final de semana) e status binario de precipitacao (`Rain_Status` e `Snow_Status`).
2. **Analise Multiescalar (Horaria e Diaria):**
   - Agregacao diaria por volumes totais acumulados de demanda e precipitacao (`sum()`), eliminando o vies do ciclo de sono das madrugadas.
3. **Contraste de Subamostras (1º Quartil / P25 vs. Populacao Geral):**
   - Isolamento dos 25% dias de menor demanda do ano ($\le 5.089$ bicicletas/dia) e avaliacao de discrepancias distribucionais via **Graficos Quantil-Quantil (Q-Q Plots)** e curvas de densidade (KDE).
4. **Visualizacoes com Alta Relacao Sinal-Ruido:**
   - Graficos de dispersao em duas camadas de profundidade (segregacao visual e realce de eventos raros como temporais e nevascas sobre o fundo neutro).
   - Analise de correlacoes parametricas (Pearson) e nao-parametricas monotonas (Spearman).

---

## Principais Descobertas e Conclusoes da Analise

A dinamica de locacao de bicicletas em Seul e explicada por **tres eixos determinantes**:

### 1. Condicao Operacional Exogena (O "Filtro Zero")
* **Inoperancia do Servico (`Functioning_Day == 'No'`):** Em 234 horas do ano (distribuidas em 12 dias especificos), o sistema registrou rigorosamente **zero alugueis**, com todas as demais variaveis meteorologicas funcionando normalmente.
* **Insight:** Essas quebras decorrem de manutencao ou decisoes da administracao municipal, e nao de ausencia de demanda da populacao. Devem ser tratadas separadamente antes de calibrar modelos preditivos lineares.

### 2. Os Fatores Aceleradores da Demanda (Por que sobe?)
* **Temperatura do Ar (`Temperature`):** E a variavel continua de maior poder preditivo linear ($r = 0{,}54$; $\rho = 0{,}55$).
  * Em temperaturas congelantes ($< 0$ °C), a media e de apenas **198 bikes alugadas na hora**.
  * Na faixa de conforto termico ideal (20 a 28 °C), a demanda atinge **1.138 bikes alugadas na hora** — um salto de quase **6 vezes**.
* **Sazonalidade Termica:** O Verao e o Outono dominam o volume anual de alugueis (medianas diarias de **19.676** e **16.927** bikes/dia), enquanto o Inverno rigoroso derruba a mediana para apenas **4.246** bikes/dia.
* **Ritmo Urbano Circadiano:** A demanda horaria exibe um comportamento bimodal pronunciado com picos expressivos as **08h da manha** e as **18h da tarde**, refletindo a utilizacao intensiva do sistema para mobilidade de trabalho e estudo.

### 3. As Penalidades Severas (Por que despenca?)
* **Chuva (`Rainfall`):** E o maior inibidor imediato da demanda.
  * A mera presenca de qualquer precipitacao ($> 0$ mm) reduz os alugueis medios de **765 para 169 bikes/hora** (queda de **78%**).
  * Chuvas intensas ($> 2$ mm/h) colapsam a demanda para **74 bikes/hora** (queda de **90%**), achatando por completo a curva horaria, inclusive nos horarios de pico.
* **Neve (`Snowfall`):** Reduz a demanda horaria para **188 bikes/hora** e amplifica o efeito adverso das baixas temperaturas.
* **A Resolucao do Paradigma Termico:** Na analise do 1º Quartil (dias mais fracos do ano), comprovou-se que as quedas bruscas de demanda ocorridas durante o verao/outono decorreram de tempestades com **volumes diarios acumulados de ate 82 mm de chuva**.

---

## Proximos Passos do Projeto

* [x] **Etapa 1:** Analise Exploratoria de Dados (EDA), tratamento de features e sintese de variaveis promissoras.
* [ ] **Etapa 2:** Formulacao e validacao de testes estatisticos de hipotese (diferencas sazonais, impacto de feriados e testes de correlacao).
* [ ] **Etapa 3:** Desenvolvimento, calibracao e analise de residuos de modelos de Regressao Linear Multipla para predicao horaria.

---

## Tecnologias e Ambiente

O ambiente do projeto e gerenciado de forma reprodutivel via [**uv**](https://github.com/astral-sh/uv):

* **Linguagem:** Python 3.12+
* **Manipulacao e Analise de Dados:** `pandas`, `numpy`
* **Visualizacao:** `matplotlib`, `seaborn`
* **Modelagem e Estatistica:** `scipy`, `statsmodels`, `scikit-learn`
* **Kernel Jupyter:** `Python (EXAME B - uv)`

### Como Reproduzir Localmente

1. Clone o repositorio:
   ```bash
   git clone <URL_DO_REPOSITORIO>
   cd "EXAME B prob"
   ```

2. Instale as dependencias e o ambiente virtual com `uv`:
   ```bash
   uv sync
   ```

3. Registre o kernel do Jupyter:
   ```bash
   uv run python -m ipykernel install --user --name exame-b --display-name "Python (EXAME B - uv)"
   ```

4. Abra o notebook principal:
   ```bash
   uv run jupyter lab EXAME_B.ipynb
   ```

---

## Estrutura de Arquivos

```text
EXAME B prob/
├── EXAME_B.ipynb         # Notebook principal com a analise exploratoria completa (Etapa 1)
├── bike_sharing.csv      # Conjunto de dados original (7.008 registros horarios)
├── data_description.md   # Dicionario descritivo detalhado das variaveis
├── README.md             # Apresentacao do projeto e sintese dos resultados
├── README_EXAME.md       # Diretrizes, rubrica e instrucoes oficiais da disciplina
└── pyproject.toml        # Configuracao de dependencias do ambiente Python (uv)
```
