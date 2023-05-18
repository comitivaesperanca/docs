Para executar a plataforma, é necessário ter o [Docker](<https://www.docker.com/>) instalado na máquina. <br>. 
Também é necessário ter uma chave SSH configurada no Github. Para isso, siga os passos abaixo:

- [Gerando uma chave SSH](https://docs.github.com/pt/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)


### Frontend
Inicialmente, clone o repositório para sua máquina, seguindo os passos abaixos:
```bash
git clone git@github.com:comitivaesperanca/frontend.git
```
Em seguida, execute o comando:
```bash
docker-compose up -d --build
```

### Backend
Inicialmente, clone o repositório para sua máquina, seguindo os passos abaixos:
```bash
git clone git@github.com:comitivaesperanca/backend.git
```
Em seguida, execute o comando:
```bash
docker-compose up -d --build
```

### Dados
Inicialmente, clone o repositório para sua máquina, seguindo os passos abaixos:
```bash
git clone git@github.com:comitivaesperanca/data.git
```
Em seguida, execute o comando:
```bash
docker-compose up -d --build
```
Acessos aos sistemas da plataforma:

- Airflow: http://localhost:8080
- LabelStudio: http://localhost:8005
- Jupyter: http://localhost:8888
- API Predict: http://localhost:7000