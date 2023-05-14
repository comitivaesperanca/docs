# Documentação
<hr>

Esse repositório contém a documentação do projeto desenvolvido durante o [Pantanal.dev](pantanal.dev) em 2023.

## Ferramentas
- [Git](https://git-scm.com/)
- [Mkdocs](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [Python 3](https://www.python.org/)

## Como contribuir?
Para contribuir com a documentação, você deve seguir os seguintes passos:
```bash
# Clone o repositório
git clone git@github.com:comitivaesperanca/docs.git
cd docs
git checkout main # ou a branch que você deseja contribuir

# Instalar o mkdocs
pip install mkdocs

# Instalar as dependências
pip install -r requirements.txt

# Iniciar o servidor de desenvolvimento
mkdocs serve
```

## Como publicar?
Para publicar as modificações, basta realizar um Merge (após revisão) para a branch `main`. O deploy é feito automaticamente pelo Github Actions
O site pode ser acessado em: https://comitivaesperanca.github.io/docs/
