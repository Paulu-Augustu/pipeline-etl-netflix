# 🎬 Pipeline ETL: Dados Netflix (2016-2025)

## 📌 Sobre o Projeto
Este projeto é fruto de uma iniciativa prática de estudos focada em simular os desafios diários de um ambiente corporativo de dados. 

Para estruturar o escopo, fiz o download de uma base de dados bruta sobre produções da Netflix diretamente do **Kaggle** e utilizei **Inteligência Artificial** para atuar como meu "Líder Técnico". Pedi para a IA analisar a estrutura da planilha e gerar demandas reais de negócio, limpeza e transformação de dados para que eu pudesse resolver escrevendo o código do zero.

O resultado é um pipeline completo de **ETL (Extração, Transformação e Carga)** construído utilizando Python e Pandas, onde os dados foram limpos, tipados e preparados para serem consumidos por ferramentas de Business Intelligence (BI).

## 🛠️ Tecnologias Utilizadas
* **Linguagem:** Python
* **Bibliotecas:** `pandas`, `re` (Regex)
* **Ambiente de Desenvolvimento:** Jupyter Notebook
* **Fonte dos Dados:** Kaggle

## 🗂️ Estrutura do Pipeline (Fases do ETL)

### 1. Extração (Extract)
* Leitura de arquivo `.csv` bruto.
* Resolução de problemas de codificação de caracteres (encoding) utilizando o parâmetro `encoding_errors='replace'` para lidar com caracteres especiais do padrão Windows/Latin-1 incompatíveis com UTF-8.
* Mapeamento inicial de tipos de dados e identificação de valores nulos.

### 2. Transformação e Limpeza (Transform)
Esta foi a fase de maior complexidade do projeto, exigindo o tratamento de colunas não estruturadas com base nas demandas geradas pela IA:
* **Visualizações (Viewership):** Uso de **Regex** (`str.extract(r'([\d\.]+)')`) para isolar os dados numéricos em meio a textos variados (como *"23.0M Streams"* e *"475M Hours"*), convertendo o resultado para formato decimal (`float`).
* **Engenharia de Features (Duração):** Quebra da coluna bruta de duração (ex: *"S4; 730 min"*) em duas novas variáveis independentes: `Season` (Temporada) e `Duration_Minutes` (Minutos inteiros), utilizando grupos de captura de Regex.
* **Tratamento de Datas:** Padronização da coluna de data de lançamento de formato texto (ex: *"17-Jun-16"*) para o tipo `datetime64` nativo do Pandas, mapeando os parâmetros corretos (`format='%d-%b-%y'`) para garantir a integridade dos dados e ganho de performance.
* **Padronização de Texto:** Remoção de espaços em branco residuais em colunas categóricas (como Gêneros) usando o comando `.str.strip()`.

### 3. Análise de Negócio (Insights)
Com a base padronizada e os cálculos matemáticos viabilizados, extraí as seguintes inteligências solicitadas no exercício:
* Top 5 produções com o maior volume de visualizações de toda a base.
* Média de avaliações (IMDb) agrupada por país de origem.
* Identificação dos títulos com o maior tempo de duração (minutagem) da base.

### 4. Carga (Load)
* Exportação do DataFrame final tratado para um novo arquivo CSV (`netflix_limpa_final.csv`), sem o índice nativo do Pandas (`index=False`), estruturado e pronto para a criação de dashboards pela equipe de BI.

## 🚀 Como Executar

1. Clone o repositório:
   ```bash
   git clone [https://github.com/SEU_USUARIO/NOME_DO_REPOSITORIO.git](https://github.com/SEU_USUARIO/NOME_DO_REPOSITORIO.git)
