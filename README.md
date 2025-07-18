# ETL COVID-19 Data Pipeline

Este repositório contém um notebook Python (`etl_covid19.ipynb`) que implementa um pipeline ETL para dados de COVID-19. O objetivo é extrair dados brutos, transformá-los, gerar análises e carregar (salvar) dados limpos e agregados para uso posterior.

---

## 📁 Estrutura do Projeto

```bash
├── dados_brutos/
│   └── covid_19_complete.csv   # Arquivo CSV original com dados completos de COVID-19
├── notebooks/
│   └── etl_covid19.ipynb       # Notebook com todo o pipeline ETL
├── dados_limpos/
│   ├── covid_19_clean.csv     # Dados agregados e limpos em CSV
│   └── covid_19_clean.xlsx    # Dados agregados e limpos em Excel
├── requirements.txt           # Dependências do projeto
└── README.md                  # Este arquivo de documentação
```

---

## 📝 Descrição

O pipeline ETL executa as seguintes etapas:

1. **Extração**: leitura do arquivo CSV bruto usando `pandas`.
2. **Transformação**:

   * Remoção da coluna `Province/State`.
   * Renomeação de `Country/Region` para `Country`.
   * Preenchimento de valores faltantes em `Confirmed`, `Deaths`, `Recovered` e `Active` com zero.
   * Filtragem de linhas onde todas as métricas sejam zero.
   * Conversão da coluna `Date` para o tipo `datetime`.
3. **Carga**:

   * Agrupamento por país, somando casos confirmados, mortes, recuperados e ativos.
   * Cálculo da taxa de mortalidade (`Deaths / Confirmed * 100`).
4. **Análise**:

   * Seleção dos top 15 países por casos confirmados.
   * Seleção dos top 15 países por taxa de mortalidade.
   * Geração de gráficos de barras horizontais lado a lado para visualizar as métricas.
5. **Exportação**:

   * Salvamento do DataFrame agregado em CSV e Excel na pasta `dados_limpos/`.

---

## ⚙️ Pré-requisitos

* Python 3.11+
* pip

### Instalar dependências

```bash
pip install -r requirements.txt
```

Conteúdo do `requirements.txt`:

```txt
pandas
numpy
matplotlib
```

---

## 🔍 Detalhes do Pipeline ETL

- **Leitura de Dados**: usa `pd.read_csv` para carregar o CSV bruto.
- **Limpeza**:
  - `drop` e `rename` de colunas para padronização.
  - `fillna(0)` para métricas numéricas.
  - Filtragem de linhas onde todas as métricas são zero para remover entradas irrelevantes.
- **Conversão de Data**: `pd.to_datetime` para facilitar operações de data.
- **Agregação**: `groupby('Country').agg(...)` para combinar registros por país.
- **Cálculo de Métricas**: adiciona coluna `Mortality Rate` arredondada em duas casas.
- **Visualização**: gera gráficos com `matplotlib` para análise rápida.
- **Exportação**: salva o resultado final em CSV e Excel.

---

## 📝 Licença

Este projeto está licenciado sob a MIT License. Veja o arquivo `LICENSE` para mais detalhes.

```
