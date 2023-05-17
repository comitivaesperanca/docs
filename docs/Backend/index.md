
# Backend

## **Domain Driven Design**

No projeto da API do “Radar da Soja” foi utilizado padrões e conceitos do DDD (Domain Driven Design), possibilitando compreender a fundo o modelo de negócios abordado nesse projeto e o domínio do mercado da Soja, permitindo identificar características essenciais das notícias e entender as regras de negócio relacionadas a elas.

Com base nesse conhecimento, foi implementado um modelo de domínio que representa as Notícias, incluindo seus atributos (objetos de valores). Utilizamos também o conceito de bounded context, para delimitar em um espaço específico as notícias sobre a soja, isolando suas regras e lógica em um contexto bem definido.

Com a aplicação do DDD, foi possível desenvolver um sistema mais estruturado e alinhado com o domínio de negócio, facilitando a manutenção e a evolução do projeto ao longo do tempo.

<center> ![capa_ddd](images\capa_ddd.png) </center>

## **Web Service**

### **.NET Core C#**

Como tecnologia escolhida para o projeto API do Radar da Soja, o .NET Core C# foi escolhido por se tratar de uma linguagem poderosa e versátil, pois combina eficiência e desempenho de linguagens de baixo nível com a facilidade de uso e a sintaxe amigável de linguagens de alto nível.

A plataforma .NET e a linguagem C# são conhecidas por oferecer bom desempenho e escalabilidade. O .NET usa a compilação just-in-time (JIT) para converter o código C# em código de máquina altamente otimizado, resultando em execução eficiente. Além disso, a plataforma .NET possui recursos avançados para dimensionamento, como o suporte a aplicativos em várias camadas e a capacidade de lidar com grandes volumes de tráfego.

A Microsoft oferece um ecossistema de produtos e serviços amplo e integrado. Ao desenvolver em C#, você pode aproveitar essa integração com outros produtos e serviços da Microsoft, como o Azure (plataforma de nuvem), o SQL Server (banco de dados), o Office 365 (produtividade), entre outros. Isso permite que você desenvolva aplicativos que se integrem perfeitamente com esses serviços e aproveite a sinergia entre eles.

Portanto, podemos afirmar que esta tecnologia supre todas nossas necessidades e expectativas para o desenvolvimento desta API, de forma que foi desenvolvida de maneira simples a fim de garantir agilidade no processo de desenvolvimento do projeto.

### **Swagger**

O Swagger consiste em uma ferramenta de auxílio muito eficaz para projeção, construção, documentação e teste de serviços de sua API REST.

Uma grande vantagem oferecida pelo Swagger é a criação de documentação automática para nossos serviços Web RESTful, que, com base nas anotações em código-fonte, a ferramenta Swagger cria a documentação detalhada dos endpoints da aplicação bem como parâmetros, tipos de dados e códigos de respotas para suas funcionalidades. Com isso, desenvolvedores e usuários são capazes de entender como utilizar corretamente os serviços oferecidos.

Atualmente essa ferramenta é utilizada em diversos projetos em diversas linguagens, pois oferece um amplo suporte a essa e muitas outras tecnologias e linguagens de programação. Além disso, trabalhar com o swagger é garantir a padronização e consistência de sua API, pois, ao adotar o Swagger, estamos seguindo a abordagem padronizada e consistente para documentar e descrever nossos serviços, o que é uma excelente vantagem em grandes equipes, mas que também se aplica a nosso cenário de desenvolvimento atual.

De forma sucinta, o Swagger garanteu uma solução comum de documentar serviços, garantindo que todos estejam na mesma página e sigam as mesmas práticas recomendadas, além de fornecer uma experiência interativa na exploração e teste de APIs.

### **ORM Entity Framework e Code First**

Sem dúvida, um dos grandes desafios do Pantanal.Dev foi desenvolver um produto de software seguindo conceitos da Engenharia de Software casado com aplicação de Machine Learning em um tempo extremamente reduzido. Boa parte do tempo de desenvolvimento do projeto foi utilizado para idealizar o produto e construir o modelo de negócio, com isso o desenvolvimento que possuia cronograma curto se mostrou ainda mais apertado em seus prazos.

Com isso, tornou-se mais que necessário adotar práticas e ferramentas que auxiliassem o desenvolvimento ágil, sendo uma delas o framework ORM Entity Framework, uma poderosa ferramenta capaz de impactar positivamente na produtividade do desenvolvimento da API, fornecendo mapeamentos automáticos de objetos, facilidade na criação de tabelas em bancos de dados relacionais através de suas Migrations, amplo suporte à consultas ao contexto da aplicação(LINQ) entre outras ferramentas que garantiram que o serviço básico da API fosse entregue em tempo para seus usuários.

Graças ao Entity Framework ORM, após o processo de criação das Entidades no projeto API, a ferramenta de mapeamento, alinhada aos conceitos de Code Firts, possibilitou a criação de tabelas no banco de dados PostgreSQL, poupando horas de trabalho na criação manual de tabelas, relacionamentos e definições de propriedades dentro da base de dados, tornando-se inegável o avanço em produtividade ao implementarmos primeiramente as classes(entidades) do projeto, para posteriormente serem persistidas ao banco de dados.

