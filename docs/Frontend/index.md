## Radar da soja Web



## 🆘 **Como executar?**
A plataforma é feita em Next e usando Typescript:
- *[Nextjs](<https://nextjs.org/>)*
- *[Typescript](<https://www.typescriptlang.org/>)*

Para executar a plataforma, é necessário ter o [Docker](<https://www.docker.com/>) instalado na máquina. <br>

Inicialmente, clone o repositório para sua máquina, seguindo os passos abaixos:
```bash
git clone
```
Em seguida, execute o comando:
```bash
npm install
```
Em seguida, execute o comando:
```bash
docker-compose up -d --build
```

Após a execução do comando, a plataforma estará disponível para uso. <br>
- Para acessar, acesse o endereço: http://localhost:3000

## **Mais informações**

Para saber mais sobre o NextJS e suas tecnologias, acesse os seguintes recursos:

- [Next.js Documentation](https://nextjs.org/docs) 
- [Learn Next.js](https://nextjs.org/learn) 

## **Next.JS Rendering**

### **Pre-rendering**

Por padrão, o Next.js pré-renderiza cada página. Isso significa que o Next.js gera o HTML para cada página com antecedência, em vez de ter tudo feito pelo JavaScript do lado do cliente. O pré-processamento pode resultar em melhor desempenho e SEO

### **SSR: Server-side rendering**

O Next.js irá pré-renderizar esta página em cada solicitação usando os dados retornados por getServerSideProps.

- [Server-side Doc](https://nextjs.org/docs/basic-features/data-fetching/get-server-side-props)

### **SSG: Static-site generation**

O Next.js irá pré-renderizar esta página no momento da construção usando as props retornadas por getStaticProps.

No desenvolvimento (next dev), getStaticProps será chamado em cada solicitação.

- [Static-site Doc](https://nextjs.org/docs/basic-features/data-fetching/get-static-props)

### **CSR: Client-side rendering**

Se feito no nível da página, os dados são buscados em tempo de execução, e o conteúdo da página é atualizado conforme os dados mudam. Quando usado no nível do componente, os dados são buscados no momento da montagem do componente, e o conteúdo do componente é atualizado conforme os dados mudam.

- [Client-side Doc](https://nextjs.org/docs/basic-features/data-fetching/client-side)
## **Pacotes Instalados**

1. [Axios](https://github.com/axios/axios)
3. [Tailwind](https://tailwindcss.com/)
4. [ChartJS](https://www.chartjs.org/)
5. [FlowBite](https://flowbite.com/)
6. [Eslint](https://eslint.org/)
   1. https://github.com/jsx-eslint/eslint-plugin-react