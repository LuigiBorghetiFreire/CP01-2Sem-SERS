# CP01-2Sem-SERS

Luigi Borgheti Freire - CCPH - RM569958

Projeto acadêmico desenvolvido para a disciplina **Soluções em Energias Renováveis e Sustentáveis**, do curso de **Ciência da Computação**. A atividade reúne duas análises exploratórias relacionadas ao consumo e à demanda de energia: uma baseada em dados públicos do Operador Nacional do Sistema Elétrico (ONS) e outra baseada no conjunto *Appliances Energy Prediction*, da UCI Machine Learning Repository.

## Objetivo

Aplicar conceitos de análise de dados com Python para coletar, organizar, filtrar, resumir e visualizar dados energéticos. O trabalho envolve a construção e inspeção de DataFrames, tratamento dos tipos de dados, cálculo de indicadores estatísticos, criação de recortes por critérios de consumo e interpretação dos resultados.

## Atividades desenvolvidas

### 1. Análise da carga elétrica de São Paulo — ONS

O primeiro notebook consulta diretamente a API pública de **Carga Verificada do ONS** para analisar a área de carga de São Paulo (`SP`) entre **1º e 7 de agosto de 2025**.

As principais etapas foram:

- requisição dos dados em formato JSON por meio da biblioteca `requests`;
- conversão dos registros para um DataFrame Pandas;
- inspeção da estrutura, atributos e tipos dos dados;
- renomeação e seleção das colunas relevantes;
- verificação de valores ausentes e conversão das datas para `datetime`;
- cálculo de carga mínima, máxima, média, mediana e amplitude;
- identificação dos períodos de alta demanda, definidos como valores superiores a 90% da carga máxima;
- comparação entre os registros de alta demanda e os registros acima da média;
- produção de gráfico de série temporal e histograma da carga global;
- interpretação dos padrões e elaboração de síntese técnica.

#### Principais resultados

| Indicador | Resultado |
|---|---:|
| Área analisada | São Paulo (SP) |
| Período | 01/08/2025 a 07/08/2025 |
| Medições | 336 |
| Carga mínima | 12.139,25 MW |
| Carga máxima | 23.185,31 MW |
| Carga média | 17.870,83 MW |
| Mediana | 18.199,13 MW |
| Amplitude | 11.046,06 MW |
| Limiar de alta demanda | 20.866,78 MW |
| Registros de alta demanda | 50 (14,88%) |
| Momento do pico | 01/08/2025 às 22:00 UTC |
| Registros acima da média | 184 (54,76%) |

A série temporal apresenta variações recorrentes ao longo dos dias, com redução da carga durante a noite e elevação nos períodos de maior atividade. Os registros acima de 90% do máximo representam uma parcela relativamente pequena da semana analisada, caracterizando períodos pontuais de maior demanda.

### 2. Análise de consumo residencial — UCI

O segundo notebook utiliza uma amostra tratada do conjunto **Appliances Energy Prediction** para explorar a relação entre consumo de eletrodomésticos, iluminação, temperatura e umidade em ambientes residenciais.

O arquivo analisado contém **1.974 registros e 8 atributos**:

- `Appliances`: consumo de energia dos eletrodomésticos, em Wh;
- `lights`: consumo de energia da iluminação, em Wh;
- `T1`, `T2` e `T3`: temperaturas de diferentes cômodos, em °C;
- `RH_1`, `RH_2` e `RH_3`: umidades relativas dos mesmos ambientes, em %.

As atividades incluíram inspeção do DataFrame, estatísticas descritivas, renomeação de colunas e criação de filtros. O maior consumo de eletrodomésticos encontrado foi de **1.080 Wh**. Adotando 70% desse máximo como limiar (**756 Wh**), foram selecionados **3 registros**, equivalentes a **0,15% da amostra**. Ao acrescentar o critério de temperatura `T1` acima da média de **21,61 °C**, o recorte foi reduzido para **2 registros**.

## Fontes dos dados

### Operador Nacional do Sistema Elétrico (ONS)

- [Portal de Dados Abertos do ONS](https://dados.ons.org.br/)
- [Conjunto de dados — Carga de Energia Verificada](https://dados.ons.org.br/dataset/carga-energia-verificada)
- [Endpoint da API de Carga Verificada](https://apicarga.ons.org.br/prd/cargaverificada)
- Consulta utilizada: área `SP`, de `2025-08-01` a `2025-08-07`.

### UCI Machine Learning Repository

- [Appliances Energy Prediction](https://archive.ics.uci.edu/dataset/374/appliances%2Benergy%2Bprediction)
- DOI: [10.24432/C5VC8G](https://doi.org/10.24432/C5VC8G)
- Autoria do conjunto: Luis Candanedo (2017).
- O notebook utiliza `DADOS_TRATADOS_01.csv`, uma amostra reduzida e com colunas selecionadas a partir do conjunto original.

## Tecnologias utilizadas

- Python 3
- Jupyter Notebook / Google Colab
- Pandas
- Requests
- Matplotlib
- Seaborn
- Google Gemini API (etapa opcional de apoio à redação do relatório)

## Como executar

1. Clone este repositório.
2. Instale as dependências:

   ```bash
   pip install pandas requests matplotlib seaborn jupyter
   ```

3. Mantenha o arquivo `DADOS_TRATADOS_01.csv` no mesmo diretório do notebook `CP01_2Sem.ipynb`.
4. Inicie o Jupyter Notebook:

   ```bash
   jupyter notebook
   ```

5. Abra os notebooks e execute as células na ordem em que aparecem.

> A análise do ONS depende de conexão com a internet para consultar a API. A etapa opcional com Gemini exige uma chave configurada de forma segura como `GEMINI_API_KEY`; nenhuma chave deve ser adicionada ao repositório.

## Estrutura sugerida do repositório

```text
.
├── README.md
├── Desafio_Final_Energia_ONS_API_Final.ipynb
├── CP01_2Sem.ipynb
└── DADOS_TRATADOS_01.csv
```

## Considerações finais

As análises demonstram como técnicas de exploração de dados podem apoiar a compreensão de diferentes escalas do uso de energia. Os dados do ONS permitem observar o comportamento agregado da carga elétrica e localizar períodos de pico, enquanto o conjunto residencial permite investigar situações de consumo elevado em conjunto com variáveis ambientais. As conclusões apresentadas são descritivas e não estabelecem relações de causa e efeito.
