## Introdução
A infraestrutura do Radar da Soja é composta por 3 serviços principais: o banco de dados, backend, frontend e microserviço de predict. Todos esses serviços são executados em Kubernetes, que é uma plataforma de orquestração de contêineres de código aberto que automatiza a implantação, o dimensionamento e o gerenciamento de aplicativos em contêineres. O Kubernetes foi escolhido por ser uma ferramenta que permite a execução de aplicações em contêineres de forma escalável e confiável, além de ser uma ferramenta amplamente utilizada no mercado, permitindo realizar a implantação do Radar da Soja em diversos provedores de nuvem como [AWS](https://aws.amazon.com/pt/), [Azure](https://azure.microsoft.com/pt-br/) e [Google Cloud](https://cloud.google.com/).

## Docker
Todos os serviços do Radar da Soja são executados em contêineres Docker. O Docker é uma plataforma de código aberto que permite que você crie, teste e implante aplicativos rapidamente. O Docker permite empacotar um aplicativo com todas as partes de que ele precisa, como bibliotecas e outras dependências, e enviá-lo como um único pacote. Ao fazer isso, graças ao contêiner, o aplicativo será executado em qualquer ambiente: de uma máquina física a uma máquina virtual, em um data center ou na nuvem.
Para executar o Radar da Soja em um ambiente local, é necessário instalar o Docker e o Docker Compose. 

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Kubernetes
O Kubernetes é uma plataforma de orquestração de contêineres de código aberto que automatiza a implantação, o dimensionamento e o gerenciamento de aplicativos em contêineres. O Kubernetes foi escolhido por ser uma ferramenta que permite a execução de aplicações em contêineres de forma escalável e confiável, além de ser uma ferramenta amplamente utilizada no mercado, permitindo realizar a implantação do Radar da Soja em diversos provedores de nuvem como [AWS](https://aws.amazon.com/pt/), [Azure](https://azure.microsoft.com/pt-br/) e [Google Cloud](https://cloud.google.com/).

Para executar em Kubernetes, foi necessário criar quatro deployments (Frontend, Backend, Predict e Label Studio) criando pods e respectivos services contendo Load Balancers para cada um dos serviços. 


### Deployments
O Deployments é um objeto do Kubernetes que permite a criação de pods e replicações dos mesmos. Para cada serviço do Radar da Soja, foi criado um deployment, que é responsável por criar e gerenciar os pods e replicações dos mesmos.

<figure>
    <img src="../images/deployments_azure.png">
    <figcaption>Objetos criado no serviço de Kubernetes da Azure (Fonte: Autores, 2023)</figcaption>
</figure>

### Pods
O Pod é a menor unidade que pode ser criada e gerenciada no Kubernetes. Um pod é um grupo de um ou mais contêineres, com armazenamento compartilhado (volumes), endereço IP e opções de como executar os contêineres. Ele seria o equivalente a uma máquina virtual, porém com um tamanho muito menor. Para cada serviço do Radar da Soja, foi criado um pod, que é responsável por executar o serviço.

<figure>
    <img src="../images/pods_azure.png">
    <figcaption>Objetos criado no serviço de Kubernetes da Azure (Fonte: Autores, 2023)</figcaption>
</figure>

### Services
O Service é um objeto do Kubernetes que permite a comunicação entre os pods. Para cada serviço do Radar da Soja, foi criado um service, que é responsável por permitir a comunicação externa com o pod.
No serviço de Kubernetes da Azure, foi criado um Load Balancer para cada service, que é responsável por distribuir as requisições entre os pods.

<figure>
    <img src="../images/services_azure.png">
    <figcaption>Objetos criado no serviço de Kubernetes da Azure (Fonte: Autores, 2023)</figcaption>
</figure>

## PostgreSQL
O PostgreSQL é um sistema de gerenciamento de banco de dados objeto-relacional (ORDBMS). O PostgreSQL foi escolhido por ser um banco de dados relacional de código aberto, que possui uma grande comunidade e é amplamente utilizado no mercado. Além disso, o PostgreSQL é compatível com o ORM utilizado no Radar da Soja, o Entity Framework Core.
No Radar da Soja, o PostgreSQL é utilizado para armazenar os dados das notícias e dos usuários.

### Custos com nuvem
Durante a execução do projeto, apenas o Apache Airflow não teve seu deploy no cluster de Kubernetes. O custo médio por dia ficou em torno de R$ 5.20 reais, sendo que o maior custo foi com o uso de máquinas virtuais, que ficou em torno de R$59.08 reais. O custo total do projeto foi de R$ 115.11. Estimasse que o custo total do projeto seja de R$ 464.82 ao final do mês. O custo total do projeto pode ser visto na imagem abaixo:
<figure>
    <img src="../images/forecast.jpg">
    <figcaption>Projeção de custos (Fonte: Autores, 2023)</figcaption>
</figure>

<figure>
    <img src="../images/custos_com_nuvem.jpg">
    <figcaption>Custo com nuvem durante o desenvolvimento. (Fonte: Autores, 2023)</figcaption>
</figure>