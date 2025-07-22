# Análise Preditiva da Escassez de Profissionais de Saúde Mental nos EUA

## Descrição

Este estudo investiga a escassez de profissionais de saúde mental nos Estados Unidos. Utilizando dados da Health Resources and Services Administration (HRSA), o trabalho objetiva prever a pontuação HPSA em áreas designadas de saúde mental, oferecendo subsídios para políticas de alocação de recursos.

Vídeo da apresentação do trabalho: https://youtu.be/fFZcjsALjZk

O artigo pode ser encontrado no arquivo `Análise Preditiva da Escassez de Profissionais de Saúde Mental nos EUA.pdf`, presente no repositório, ou pelo link a seguir: https://drive.google.com/file/d/1RT8rxcy86sOZsNZTcdRoqUUPtITHkNJx/view?usp=sharing

## Objetivos

* Construir modelos de classificação para prever a pontuação HPSA (0–25) em regiões com foco em saúde mental.
* Identificar variáveis demográficas e de atendimento que expliquem melhor a escassez de profissionais.
* Avaliar o desempenho de três algoritmos (Random Forest, Decision Tree e KNN) otimizados por GridSearchCV com validação cruzada.
* Analisar a importância relativa das features para fornecer recomendações de política pública.

## Conjuntos de Dados

Os dados foram obtidos no HRSA Data Warehouse ([https://data.hrsa.gov/data/download](https://data.hrsa.gov/data/download)) e envolvem:

* **All HPSAs – CSV.csv**

  * Registros: Aproximadamente 35 mil entradas específicas para saúde mental.
  * Colunas: 65 variáveis, incluindo:

    * `HPSA Score`: pontuação de 0 a 25 atribuída pelo National Health Service Corps.
    * `HPSA Discipline Class`: classifica serviços de saúde mental.
    * `HPSA Designation Population`: população afetada.
    * `HPSA FTE`: número de profissionais em equivalente tempo integral.
    * `HPSA Shortage`: profissionais adicionais necessários.
    * Indicadores geográficos e demográficos (pobreza, rural/urbano).

* **MUA/P – CSV.csv**

  * Registros de áreas/populações medicamente carentes.
  * Variáveis de interesse: percentual da população abaixo da linha de pobreza, idade, taxa de mortalidade infantil, população total, provedores por 1000 habitantes.
  * Observação: colunas críticas apresentaram alta taxa de valores ausentes (> 68%) e foram excluídas.

## Metodologia

1. **Pré-processamento e Limpeza**

Foi realizado um extenso processo de limpeza e tratamento de dados para garantir a robutez das informações fornecidas aos classificadores, incluindo:

   * Remoção de identificadores e colunas irrelevantes (IDs, descrições textuais).
   * Filtragem temporal: descartados registros anteriores a 2009 devido à pontuação HPSA invariável.
   * Tratamento de missing: avaliação da imputação (média, mediana ou moda) para variáveis com até 40% de ausência; exclusão de colunas acima desse limite.

3. **Transformação**

   * One-Hot Encoding para variáveis categóricas.
   * Padronização (StandardScaler) das variáveis numéricas.

4. **Modelagem Preditiva**

   * Divisão em treino (70%) e teste (30%).
   * Modelos avaliados:

     * **Random Forest**
     * **Decision Tree**
     * **K-Nearest Neighbors**
   * Otimização de hiperparâmetros via GridSearchCV com StratifiedKFold (k=5).

5. **Avaliação**

   * Métricas: acurácia, precisão, recall e F1-Score.

## Resultados

* **Random Forest** foi o melhor modelo, com F1-Score de **84,46%**.
* **Decision Tree**: F1-Score de 83,61%.
* **KNN**: F1-Score de 73,17%.

**Hiperparâmetros ótimos para Random Forest**:

* `n_estimators=100`
* `max_depth=None`
* `min_samples_split=2`

**Importância das features (top 5)**:

1. HPSA Designation Population
2. HPSA Shortage
3. HPSA Estimated Underserved Population
4. % Population Below 100% Poverty
5. HPSA FTE

## Como Reproduzir

1. **Clone o repositório**:

   ```bash
   git clone https://github.com/intel-comp-saude-ufes/2025-1-P1-Analise-de-Escassez-de-Profissionais-de-Saude-Mental-nos-EUA.git
   cd 2025-1-P1-Analise-de-Escassez-de-Profissionais-de-Saude-Mental-nos-EUA
   ```
2. **Instale dependências**:

   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn scipy
   ```
3. **Execute o Notebook**:

   ```bash
   jupyter notebook Analise_de_Escassez_de_Profissionais_de_Saude_Mental_nos_EUA.ipynb
   ```
4. **Ajustes**:

   * Atualize URLs dos CSVs, se necessário.

---

Elaborado por:

* Antonio Borssato - antonio.borssato@edu.ufes.br

* Lucas Alves - lucas.o.alves@edu.ufes.br

* Rodrigo Fardin - rodrigo.fardin@edu.ufes.br
