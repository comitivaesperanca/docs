
# 🐱‍👤 Dados

Com a proposta da solução definida, foi necessário definir a arquitetura da plataforma de dados que irá suportar a solução, bem como quais dados, modelos e ferramentas serão utilizados para a construção da solução.

## Fonte de dados

Foi realizado uma busca de dados abertos que pudessem ser utilizados para a construção da solução em sites como [Kaggle](https://kaggle.com), [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/index.php) e [Google Dataset Search](https://datasetsearch.research.google.com/). Entretanto, não foi encontrado nenhum dataset que atendesse aos requisitos necessários para a construção da solução, como por exemplo: dados em português, dados de notícias referente a Soja, bem como uma classificação de sentimento para essas notícias que tivesse o ponto de vista do produtor rural/trading.

### CEPEA - Centro de Estudos Avançados em Economia Aplicada

Com a necessidade de treinarmos o modelo utilizando o máximo de fontes que não houvesse viés político, foi encontrado o site do CEPEA, que é um centro de estudos avançados em economia aplicada, que é uma instituição de pesquisa da USP. O CEPEA possui uma [página de boletins diários](https://www.cepea.esalq.usp.br/br/categoria/diarias-de-mercado.aspx), chamada Diárias do Mercado, que são publicações diárias sobre o mercado de commodities agrícolas, como soja, milho, café, etc. Esses boletins são publicados diariamente desde 1997.

### Notícias Agricolas

Além do CEPEA, foi encontrado o site [Notícias Agricolas](https://www.noticiasagricolas.com.br/), que é um portal de notícias sobre o agronegócio brasileiro. Esse portal possui uma seção de notícias sobre soja, que são publicadas diariamente desde 2006. Essa fonte de notícias é interessante pois possui uma visão mais voltada para o produtor rural, diferente do CEPEA que possui uma visão econômica.
O Notícias Agricolas possui um grande volume de notícias que são de outras fontes como [Reuters](https://www.reuters.com/), o que pode ser interessante para o treinamento do modelo, uma vez que podemos regras para o mercado internacional da commodity.

## Coleta de dados

### Introdução

Para realizar a coleta de dados das plataformas acima, foi necessário a utilização da ferramenta [Apache Airflow](https://airflow.apache.org/), que é uma plataforma de orquestração de fluxos de trabalho (workflow) de código aberto que permite aos usuários programar, agendar e monitorar tarefas em fluxos de trabalho complexos. Essa ferramenta foi escolhida pois suas vantagens permite com que o processo de coleta seja escalável, flexível e com monitoramento em tempo real.
As tarefas de coleta de dados foram divididas em 3 etapas:

- [Coleta de dados do CEPEA](https://github.com/comitivaesperanca/data/blob/main/airflow/dags/data_engineering/scrapping_cepea.py)
- [Coleta de dados do Notícias Agricolas](https://github.com/comitivaesperanca/data/blob/main/airflow/dags/data_engineering/scrapping_noticias_agricolas.py)

Para cada fonte de dados, foi necessário criar uma DAG (Directed Acyclic Graph) que é um fluxo de trabalho que define como as tarefas serão executadas, para cada fonte de dados. Essas DAGs foram criadas utilizando a sintaxe de Python, e utilizam bibliotecas como BeautifulSoup, Pandas e Requests para realizar a coleta de dados.

O processo de fluxo de dados ficou da seguinte forma:

![Fluxo de dados](images/fluxo_de_coleta.png)

### Processo de coleta

Para executar a primeira carga de dados completa, foi necessário parametrizar as DAGs para buscar os dados desde 1997, para o CEPEA, e desde 2006, para o Notícias Agricolas. Após a execução da primeira carga de dados, as DAGs foram parametrizadas para buscar os dados apenas do dia anterior, para que o processo de coleta seja incremental.

![DAG desenvolvida para coleta de dados do CEPEA](images/dag_cepea.png "DAG desenvolvida para coleta de dados do CEPEA")
![DAG desenvolvida para coleta de dados do Notícias Agricolas](images/dag_noticias_agricolas.png "DAG desenvolvida para coleta de dados do Notícias Agricolas")

Na imagem acima, é possível visualizar a DAG desenvolvida para a coleta de dados do CEPEA e do Notícias Agricolas. Essas DAGs são executadas diariamente, e a cada execução, os dados do dia anterior são coletados e armazenados localmente, podendo vir a ser carregado a um banco de dados ou a um data lake.

### Análise exploratória
Ao concluir a carga incremental do CEPEA, foi possível obter 7639 notícias, desde Julho de 2006 até a presente data, conforme o gráfico abaixo:
<iframe width=700, height=500 frameBorder=0 src="images/quantidade_noticias_cepea.html"></iframe> 

Já o Notícias Agricolas, foi possível obter 23.601 notícias, conforme a imagem abaixo:
<iframe width=700, height=500 frameBorder=0 src="images/quantidade_noticias_agricolas.html"></iframe> 

Para iniciar o tratamento das notícias, de maneira que fosse possível filtrar apenas as notícias referentes a soja, foi necessário realizar uma análise exploratória dos dados, para entender quantas notícias houvesse Soja mencionada, ao menos duas vezes. No Dataset do CEPEA, foi possível encontrar 954 notícias que tivesse a palavra Soja mencionada ao menos duas vezes, conforme a imagem abaixo:
<iframe width=700, height=500 frameBorder=0 src="images/soja.html"></iframe>

No Dataset do Notícias Agricolas, foi possível encontrar 3.358 notícias que tivesse a palavra Soja mencionada ao menos duas vezes, conforme a imagem abaixo:
<iframe width=700, height=500 frameBorder=0 src="images/soja_na.html"></iframe>

### Rotulação dos dados
Para realizar a rotulação dos dados, foi utilizado a ferramenta [Label Studio](https://labelstud.io/), que é uma plataforma de marcação de dados (data labeling) de código aberto que permite criar tarefas de marcação de forma simples e escalável. 
Conforme o curto prazo para a entrega do projeto, foi necessário realizar a rotulação dos dados manualmente, porém, para uma entrega futura, é possível utilizar técnicas de NLP para realizar a rotulação dos dados de maneira automática, como por exemplo, utilizando o [Spacy](https://spacy.io/).

Devido ao grande volume, a equipe optou por classificar apenas as notícias do CEPEA, que possuía um volume menor de dados, e que possuía uma visão mais econômica, diferente do Notícias Agricolas, que pode possuir notícias com viés político.

Foi realizado o deployment da ferramenta Label Studio utilizando o serviço de Kubernetes da [Azure](https://azure.microsoft.com/pt-br/), e a rotulação dos dados foi realizada por 4 pessoas do time, conforme a imagem abaixo:
![Rotulação dos dados](images/labelstudio_rotulacao.jfif "Momento onde o time atingiu 599 notícias rotuladas")

### Criação do modelo
Após a rotulação dos dados, foi necessário realizar o treinamento do modelo de Machine Learning, para que fosse possível criar o *Motor de Classificação* do Radar da Soja, que é o responsável por classificar as notícias em Positivo, Neutro ou Negativo. Com a necessidade de desenvolvermos um modelo utilizando BERT (através de redes neurais), o time optou por desenvolver um modelo baseline, para servir de efeito de comparação, utilizando o modelo [Naive Bayes Multinomial](https://scikit-learn.org/stable/modules/naive_bayes.html), que é um modelo de classificação probabilístico baseado no teorema de Bayes, que assume que a presença de uma característica em uma classe não está relacionada com a presença de qualquer outra característica.

#### Modelo Naive Bayes Multinomial (Baseline)
O modelo Naive Bayes Multinomial foi escolhido por ser um modelo de classificação probabilístico, que é um modelo simples e rápido, que pode ser utilizado como baseline para comparação com outros modelos mais complexos. <br>
No Naive Bayes Multinomial, determinamos a probabilidade de uma notícia pertencer a uma classe, baseado na frequência de palavras que aparecem na notícia.  <br>
Para o treinamento do modelo, foi utilizado o dataset rotulado (421 notícias), sendo separado em 80% para treino (336 notícias) e 20% (101 notícias) para validação.  <br>
Após o treinamento, foi possível obter o seguinte reporte de classificação:

<figure>
    <img src="images/modelo_naive_treino.png">
    <figcaption>Resultado de classificação do modelo no conjunto de teste. (Fonte: Autores, 2023)</figcaption>
</figure>
    
Enquanto que para o conjunto de validação, foi possível obter o seguinte reporte de classificação:
<figure>
    <img src="images/modelo_naive_validacao.png">
    <figcaption>Resultado de classificação do modelo no conjunto de validação. (Fonte: Autores, 2023)</figcaption>
</figure>

Após o treinamento do modelo, foi possível obter uma acurácia de 0.62 no conjunto de teste, e 0.60 no conjunto de validação, o que mostra que o modelo possui uma boa capacidade de generalização, e que pode ser utilizado como baseline para comparação com outros modelos mais complexos.

#### Modelo BERT
Com a crescente utilização de modelos de Deep Learning para a resolução de problemas de NLP, o time optou por utilizar o modelo BERT, que é um modelo de Deep Learning desenvolvido pelo Google, que possui uma arquitetura baseada em redes neurais, e que possui um desempenho superior a outros modelos de NLP, como o Naive Bayes Multinomial. <br>
O modelo BERT é utilizado como um modelo pré-treinado, que é treinado em um grande volume de dados, e que pode ser utilizado para resolver problemas de NLP, como classificação de texto, sumarização de texto, entre outros. <br>
Para a aplicação do modelo no projeto, foi necessário realizar o fine-tuning do modelo, que é o processo de treinar o modelo pré-treinado em um conjunto de dados específico para o problema que se deseja resolver. <br>
Para o treinamento do modelo, foi utilizado o dataset rotulado (421 notícias), sendo separado em 80% para treino (336 notícias) e 20% (101 notícias) para validação.  <br>
Após o treinamento, foi possível obter o seguinte reporte de classificação para o conjunto de teste:


<figure>
    <img src="images/treinamento_bert.jpg">
    <figcaption>Resultado de classificação do modelo no conjunto de teste.(Fonte: Autores, 2023)</figcaption>
</figure>

<figure>
    <img src="images/validacao_bert.jpg">
    <figcaption>Resultado de classificação do modelo no conjunto de teste.(Fonte: Autores, 2023)</figcaption>
</figure>

#### Considerações sobre o modelo
Após o treinamento dos modelos, foi possível obter os seguintes resultados:

| Modelo | Acurácia no conjunto de teste | Acurácia no conjunto de validação | Precisão - Validação| Recall - Validação | F1-Score - Validação |
| --- | --- | --- | --- | --- | --- |
| Naive Bayes Multinomial | 0.62 | 0.60 | 0.70 | 0.57 | 0.54 |
| BERT | 0.76 | 0.70 | 0.72 | 0.70 | 0.68 |

Por se tratar de um modelo de Deep Learning, o BERT possui uma acurácia superior ao Naive Bayes Multinomial, que é um modelo de Machine Learning tradicional. <br>
Entretanto, o modelo BERT possui uma precisão inferior ao Naive Bayes Multinomial, o que pode ser explicado pela quantidade de dados de treinamento.
Para uma entrega futura, é necessário que o modelo BERT seja treinado com um volume maior de dados, para que seja possível obter uma precisão maior, e que possa ser utilizado no Radar da Soja.

Contundo, é nitido que o modelo BERT possui uma acurácia superior ao Naive Bayes Multinomial, o que mostra que o modelo BERT possui uma capacidade de generalização superior ao Naive Bayes Multinomial, e que pode ser utilizado como modelo de classificação no Radar da Soja.

### Deploy do modelo
Para que o modelo possa ser utilizado no Radar da Soja possa ser integrado na plataforma, foi necessário realizar dois deploys do modelo: Integração no Pipeline de ingestão de notícias na plataforma e criação de uma API para que seja feito a interação do modelo. O usuário digitaria o texto da notícia e o modelo retornaria a classificação da notícia, com suas respectivas probabilidades.

#### Pipeline de classificação
Para o Pipeline de classificação, foi incrementar a tarefa já criada para o Airflow, para que ao concluir a ingestão de notícias ao armazenamento, o modelo fosse executado, e que a classificação encaminhada a plataforma através da aplicação Backend. Para atingir esse objetivo, foi necessário incluir os arquivos dos modelos (Para o Naive Bayes Multinomial, foi necessário incluir o arquivo `naive_bayes.pkl`, e para o BERT, foi necessário incluir os arquivos `modelo_soja_rede_neural.pt`).

#### API de classificação
Para que outras aplicações do Radar da Soja pudesse interagir com o modelo, foi necessário criar uma API para que fosse possível realizar a classificação de notícias. Para isso, foi necessário criar uma API utilizando a ferramenta [FastAPI](https://fastapi.tiangolo.com/), que é uma ferramenta de desenvolvimento de APIs de alto desempenho, que utiliza a sintaxe de Python, e que possui uma documentação automática através do Swagger. <br>
Para a criação da API, foi necessário criar um endpoint que recebesse o texto da notícia, e que retornasse a classificação da notícia, com suas respectivas probabilidades, foi necessário carregar o modelo treinado, e que fosse possível realizar a classificação da notícia. <br>