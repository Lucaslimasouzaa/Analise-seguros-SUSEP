# Análise de Dados de Seguros de Automóveis (SUSEP-2021) (EM ANDAMENTO)

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458)
![Plotly](https://img.shields.io/badge/Plotly-Interactive%20Maps-3F4F75)
![Status](https://img.shields.io/badge/Status-Em_andamento-yellow)

> Este projeto realiza a ingestão, limpeza, enriquecimento e visualização de uma base de dados massiva de seguros de automóveis (referência SUSEP-2021), focando na distribuição demográfica e geográfica dos segurados no Brasil.

---

## 📋 Sobre o Projeto

O objetivo deste notebook é processar um dataset volumoso (~31 milhões de registros) de apólices de seguros, transformando dados brutos em insights visuais. O projeto aborda desafios comuns em Data Science, como otimização de memória, tratamento de datas, feature engineering e georreferenciamento a partir de CEPs.

### Principais Análises:
* **Perfil do Segurado:** Distribuição por Sexo e Tipo de Pessoa (Física/Jurídica).
* **Faixa Etária:** Cálculo de idade e histograma de distribuição.
* **Geolocalização:** Mapeamento de segurados por Estado (UF) e mapas de calor (Heatmaps) de densidade.
* **Estatística:** Verificação da Lei de Zipf na distribuição de seguros por estado.

---

## 🛠️ Tecnologias e Ferramentas

* **Linguagem:** Python
* **Manipulação de Dados:** `pandas`, `numpy`
* **Visualização:** `matplotlib`, `plotly.express` (Mapas interativos)
* **Geodados:** `requests` (para GeoJSON), base externa de CEPs.
* **Formatos:** CSV, Pickle (`.pkl` para otimização de I/O), HTML (para exportação dos mapas).

---

## ⚙️ Metodologia e Pipeline

### 1. Ingestão e Otimização
* Leitura do arquivo original `R_AUTO_2021A.csv`.
* Conversão imediata para formato **Pickle (.pkl)**, reduzindo drasticamente o tempo de carregamento em execuções subsequentes.
* Conversão de colunas de datas (`INICIO_VIG`, `FIM_VIG`, `DATA_NASC`) para `datetime`, tratando erros de formatação.

### 2. Engenharia de Atributos (Feature Engineering)
* **Cálculo de Idade:** Criação da coluna `IDADE` baseada na data de nascimento em relação ao ano de referência (2021).
* **Inferência de UF:** Criação de uma função lógica para mapear o Estado (UF) baseada nas faixas numéricas dos 5 primeiros dígitos do CEP.

### 3. Enriquecimento Geográfico (Geocoding)
Devido ao alto volume de dados, APIs de geolocalização (como `geopy` ou `brazilcep`) seriam inviáveis por tempo e limites de requisição.
* **Solução:** Merge (join) com uma base de dados externa (`cep_brasil_2018.csv`) contendo Lat/Lon por CEP.
* **Resultado:** Enriquecimento de ~75% da base (~23.8 milhões de registros validados com coordenadas).

### 4. Visualização de Dados
* Geração de gráficos de barras para variáveis categóricas.
* Histograma para distribuição de idades (com filtro para maiores de 18 anos).
* **Mapas Interativos (Plotly):**
    * **Choropleth:** Mapa do Brasil colorindo estados por volume de seguros.
    * **Heatmap:** Mapa de densidade utilizando coordenadas (Latitude/Longitude) de uma amostra dos dados.

<img width="590" height="390" alt="distribuicao_sexo" src="https://github.com/user-attachments/assets/5921364b-6037-41b6-8589-ccd23ad36462" />
<img width="590" height="390" alt="distribuicao_PF_PJ" src="https://github.com/user-attachments/assets/21c4b370-7fcb-403c-8153-5bc51ad07868" />
<img width="989" height="590" alt="Histograma_idade" src="https://github.com/user-attachments/assets/4a89b59a-2d24-4ed5-ac7f-cea1398e4938" />
<img width="2963" height="2368" alt="ranking_seguros_por_estado" src="https://github.com/user-attachments/assets/f535085e-f522-4213-a639-9d48ebe33ed0" />
<img width="2960" height="1754" alt="grafico_lei_de_zipf_estados" src="https://github.com/user-attachments/assets/ad4fac50-6785-4c9e-89e1-ffbc3ce4c637" />

---

## 📊 Exemplos de Resultados

### Distribuição Geográfica (Ranking)
O projeto identificou a concentração de seguros, validando a distribuição estatística (análise da Lei de Zipf nos dados estaduais).

*(Aqui você pode inserir uma imagem do gráfico de barras horizontais 'Ranking de Seguros por Estado' se tiver salvo)*

### Mapa Gerado
O notebook exporta o seguinte mapa interativo em HTML:
* `mapa_seguros_por_uf.html`: Visão de densidade por coordenadas.

---

## ⚠️ Notas sobre os Dados

* **Privacidade:** Nenhum dado pessoal sensível (nome, documento) é exposto nas visualizações.
* **Qualidade dos Dados:** Cerca de 25% dos CEPs não possuíam correspondência exata na base auxiliar de coordenadas ou estavam formatados incorretamente, sendo descartados apenas para a plotagem dos mapas de calor, mas mantidos para as análises estaduais (via lógica de faixas de CEP).

---

### Autor
**Lucas Augusto**
* www.linkedin.com/in/lucaslimasouz
