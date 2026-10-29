3983 - Integração Contínua

Este repositório contém uma API em Go para gerenciamento de alunos, desenvolvida com Gin, GORM e PostgreSQL. O projeto também inclui testes automatizados e uma pipeline de CI no GitHub Actions.
Objetivo

A aplicação expõe endpoints para:

    listar alunos
    buscar aluno por ID
    buscar aluno por CPF
    criar novo aluno
    atualizar aluno
    remover aluno
    renderizar página HTML simples de listagem

Stack utilizada

    Go 1.22
    Gin
    GORM
    PostgreSQL
    Docker Compose
    GitHub Actions

Estrutura do projeto
Text

.
├── .github/
│   └── workflows/
│       └── go.yml
├── assets/
├── controllers/
│   └── controller.go
├── database/
│   └── db.go
├── models/
│   └── alunos.go
├── routes/
│   └── route.go
├── templates/
│   ├── 404.html
│   └── index.html
├── .gitignore
├── docker-compose.yml
├── go.mod
├── go.sum
├── main.go
├── main_test.go
├── Makefile
└── README.md

Funcionalidades

A API permite operações CRUD para a entidade Aluno, com os campos:

    Nome
    CPF
    RG

Também há validação dos dados antes de persistir no banco.
Endpoints
Método	Rota	Descrição
GET	/:nome	Retorna mensagem de saudação com o parâmetro informado
GET	/alunos	Lista todos os alunos
GET	/alunos/:id	Busca aluno por ID
POST	/alunos	Cria um novo aluno
DELETE	/alunos/:id	Deleta um aluno
PATCH	/alunos/:id	Edita um aluno
GET	/alunos/cpf/:cpf	Busca aluno por CPF
GET	/index	Exibe página HTML com a listagem de alunos
Requisitos

    Docker
    Docker Compose
    Go 1.22 (opcional, se você quiser rodar localmente sem container)

Configuração do ambiente

O projeto usa as seguintes variáveis de ambiente para conexão com o PostgreSQL:
bash

DB_HOST=postgres
DB_USER=root
DB_PASSWORD=root
DB_NAME=root
DB_PORT=5432

Essas variáveis já são configuradas no arquivo docker-compose.yml.
Como executar
Usando Docker Compose
bash

docker compose up -d

Isso inicia:

    o banco PostgreSQL
    a aplicação Go

A API ficará disponível em:
bash

http://localhost:8080

Como rodar os testes
bash

go test -v main_test.go

Se preferir rodar via Makefile:
bash

make test

Lint
bash

make lint

Pipeline de CI

O repositório possui um workflow de Integração Contínua em .github/workflows/go.yml, que executa:

    inicialização do banco
    lint
    testes
    build
    upload do artefato compilado

Exemplos de uso
Criar aluno
bash

curl -X POST http://localhost:8080/alunos \
  -H "Content-Type: application/json" \
  -d '{
    "nome": "Maria da Silva",
    "cpf": "12345678901",
    "rg": "123456789"
  }'

Listar alunos
bash

curl http://localhost:8080/alunos

Buscar aluno por CPF
bash

curl http://localhost:8080/alunos/cpf/12345678901

Observações

    O banco é migrado automaticamente com AutoMigrate na inicialização da aplicação.
    A aplicação também serve arquivos estáticos em /assets e templates HTML em templates/.

Se quiser, posso também adaptar este README para um formato mais profissional, com badges, seção de “Getting Started” e exemplos de respostas JSON em português.
