# AGRUPA - Sistema de Gerenciamento de Grupos

Aplicação para formação e organização de grupos em sala de aula, com área do professor (atividades, grupos, QR codes, relatórios) e área do aluno (entrar na sessão, validar identidade, escolher grupo).

- **Frontend:** Angular 21 (`Frontend-Alunos`)
- **Backend:** Java 21 + Spring Boot (`Backend-Alunos`)
- **Banco:** PostgreSQL 17 (em produção) ou HSQLDB em memória (desenvolvimento local)

## Como o front e o back se comunicam

O frontend é servido por Nginx, que encaminha tudo que começa com `/api/` para o backend (`http://backend:8080`), dentro da mesma rede do Docker Compose. O backend não precisa ser exposto publicamente.

## Rodando localmente

Com Docker:

```bash
docker compose up --build
```

Acesse `http://localhost:3011`.

Sem Docker:

```bash
# Backend (porta 8080, banco HSQLDB em memória)
cd Backend-Alunos && ./mvnw spring-boot:run

# Frontend (porta 4200)
cd Frontend-Alunos && npm install && npm start
```

## Deploy no Coolify

1. Novo recurso a partir deste repositório, branch `main`.
2. Build Pack: **Docker Compose**, Base Directory `/`, arquivo `docker-compose.yml`.
3. Opcional: definir `POSTGRES_DB`, `SERVICE_USER_POSTGRES` e `SERVICE_PASSWORD_POSTGRES`.
4. A porta publicada do frontend é `3011` (`"3011:3000"` no compose). Se ela já estiver em uso no servidor, troque o primeiro número.

## Créditos

Projeto desenvolvido pela equipe **AGRUPA2-0**. O histórico original do código-base inclui commits de YannPG, Leonardo Tubero e Kaique Souza, além de Eduardo Passarelli. A configuração de deploy (Dockerfiles, Nginx, docker-compose) foi adaptada do repositório `ADS-2026-coolify/VitorSpornraft-Agrupa`.
