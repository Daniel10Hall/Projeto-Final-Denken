# OrbitBoard - Integração Full Stack

**Capacitação em IA e Transformação Digital | Módulo 5 - Trabalho Final**

Este repositório contém a entrega do projeto final do Módulo 5, focado na orquestração e integração de uma aplicação Full Stack utilizando Docker, Docker Compose, e integração contínua (CI/CD) com GitHub Actions.

## Equipe e Contribuições

Conforme as instruções do trabalho, todos os membros contribuíram ativamente na configuração e integração do projeto:

* **Daniel Hall** (@Daniel10Hall): Responsável pelo **Back-end**. Criou o `Dockerfile` da API, configurou a exposição da porta e ajustou o ambiente .NET para a conteinerização.
* **Lucas Neves** (@lucasneves20031711): Responsável pelo **Front-end**. Criou o `Dockerfile` do front-end, lidando com a configuração do Nginx e a comunicação com a API.
* **Renan Almeida** (@RenanATeixeira): Responsável pelo **Docker Compose**. Elaborou o arquivo `docker-compose.yml`, configurando os serviços, as redes internas isoladas e o mapeamento das portas entre os containers e o host local.
* **Caio Costa** (@alkk-costa): Responsável pela **Pipeline de CI/CD**. Configurou o GitHub Actions (na pasta `.github/workflows`) para automatizar a validação, build e testes da aplicação a cada novo Pull Request na branch `develop`.

## Objetivo do Trabalho
O objetivo didático deste repositório é demonstrar a compreensão prática da arquitetura de uma aplicação full stack e o papel de cada camada. O foco da entrega está na infraestrutura, garantindo a execução isolada em containers, a comunicação fluida em rede virtual do Docker e a validação automatizada.

## Arquitetura Resumida
A aplicação segue uma estrutura client-server conteinerizada:
* **Front-end:** Interface do usuário (servida via Nginx) rodando no container isolado e exposta na porta `5173`.
* **Back-end / API:** Aplicação em .NET (C#) rodando no container do backend, fornecendo endpoints RESTful e operando na porta `5200`.
* **Infraestrutura:** Os containers conversam através de uma rede interna do Docker (bridge) definida no `docker-compose.yml`.
* **CI/CD:** O repositório utiliza Actions para testar os pacotes (como `.csproj`) antes da integração oficial na branch principal.

## Como executar a aplicação localmente

Para rodar este projeto na sua máquina, você precisa ter o **Git** e o **Docker (com Docker Compose)** instalados.

1. **Clone este repositório:**
   ```bash
   git clone https://github.com/Daniel10Hall/Projeto-Final-Denken.git
   cd Projeto-Final-Denken
   ```

2. **Inicie os containers:**
   Na raiz do projeto (onde está o arquivo `docker-compose.yml`), execute o comando:
   ```bash
   docker-compose up -d --build
   ```
   *O parâmetro `-d` roda o processo em segundo plano (detached), e o `--build` garante que as imagens mais recentes dos Dockerfiles sejam construídas.*

3. **Para desligar a aplicação:**
   Quando terminar de usar, limpe os processos e redes executando:
   ```bash
   docker-compose down
   ```

## URLs de Acesso

Após os containers subirem com sucesso, a aplicação estará disponível nos seguintes endereços locais:

* **Interface Front-end:** [http://localhost:5173](http://localhost:5173)
* **Back-end API Base:** [http://localhost:5200](http://localhost:5200)
* **Documentação Swagger (API):** [http://localhost:5200/swagger](http://localhost:5200/swagger)

## Endpoints Principais da API

* `GET /api/...` - (Retorna os dados cadastrados em formato JSON)
* `POST /api/...` - (Recebe os dados do front-end para gravação)
*(Verifique o Swagger no link acima para a lista completa e interativa de rotas).*

## Variáveis de Ambiente Necessárias
As configurações foram definidas para rodar de imediato via Docker. Caso seja necessário alterar variáveis, você pode consultar o arquivo `.env.example` na raiz ou as chaves `environment` dentro do `docker-compose.yml` (como `ASPNETCORE_ENVIRONMENT=Development`).

## Evidências e Documentação Adicional
Todas as evidências exigidas pelo trabalho (prints de funcionamento do Front-end, Swagger da API, logs de erro, comandos executados e o roteiro da apresentação final) estão organizados e disponíveis dentro da pasta `docs/` na raiz deste repositório.
