# Book Club

Aplicação de gestão de clube do livro, construída com Laravel 13, Inertia.js, Vue 3, Bootstrap 5 e Vite.

## Visão geral

Este projeto já está estruturado para desenvolvimento local com Docker Compose. A base do app usa Laravel para o backend, Vue + Inertia para o frontend e SQLite por padrão no arquivo `.env`, com um serviço MySQL também configurado em `compose.yaml` para uso futuro.

Principais pontos da estrutura:

- Backend: `app/`, `routes/`, `database/migrations/`
- Frontend: `resources/js/`, `resources/css/`
- Build do frontend: `vite.config.js`
- Infra: `compose.yaml`, `docker/php/Dockerfile`

## Stack

- PHP 8.3+
- Laravel 13
- Inertia.js
- Vue 3 + Composition API
- Bootstrap 5
- Vite
- Docker Compose
- MySQL 8.4 (serviço opcional no ambiente Docker)

## Requisitos

Antes de começar, garanta que o Docker e o Docker Compose estejam instalados:

- Docker
- Docker Compose

Se for rodar fora do Docker, também será necessário:

- PHP 8.3+
- Composer
- Node.js 22+
- npm

## Passo a passo para rodar

### 1) Acesse a pasta do projeto

```bash
cd /home/[seu_nome]/workspace/book-club
```

### 2) Verifique o ambiente

O projeto já contém um arquivo `.env` e também um `.env.example`. O ambiente atual está configurado com SQLite por padrão.

Se você estiver começando do zero e não tiver o arquivo `.env`, rode:

```bash
cp .env.example .env
```

### 3) Suba os containers do Docker

```bash
docker compose up -d --build
```

Esse comando inicia os serviços:

- `app` → Laravel + PHP
- `node` → Vite + frontend
- `mysql` → banco MySQL

### 4) Instale as dependências do backend

```bash
docker compose exec app composer install
```

### 5) Gere a chave da aplicação

```bash
docker compose exec app php artisan key:generate
```

### 6) Rode as migrations

```bash
docker compose exec app php artisan migrate
```

Se estiver usando o SQLite padrão, o arquivo do banco será criado em:

```bash
database/database.sqlite
```

### 7) Instale as dependências do frontend

```bash
docker compose exec node npm install
```

### 8) Inicie o Vite para o frontend

O serviço `node` já tenta iniciar o Vite automaticamente quando o container sobe, mas se quiser iniciar manualmente:

```bash
docker compose exec node npm run dev -- --host 0.0.0.0
```

### 9) Acesse a aplicação

- Backend/Laravel: http://localhost:8000
- Frontend/Vite: http://localhost:5173

## Uso do banco de dados

Por padrão, o projeto está com SQLite ativo no `.env`:

```env
DB_CONNECTION=sqlite
```

Se quiser usar o MySQL do Docker Compose, ajuste o `.env` para algo como:

```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=bookclub
DB_USERNAME=bookclub
DB_PASSWORD=bookclub123
```

Depois disso, execute:

```bash
docker compose exec app php artisan migrate
```

## Comandos úteis

### Rodar testes

```bash
docker compose exec app php artisan test
```

### Limpar cache do Laravel

```bash
docker compose exec app php artisan cache:clear
docker compose exec app php artisan config:clear
docker compose exec app php artisan route:clear
```

### Ver logs

```bash
docker compose logs -f app
```

### Parar a stack

```bash
docker compose down
```

### Remover volumes do banco

```bash
docker compose down -v
```

## Estrutura relevante

```text
.
├── app/
├── config/
├── database/
├── docker/
├── public/
├── resources/
├── routes/
├── storage/
├── tests/
├── compose.yaml
├── composer.json
├── package.json
├── vite.config.js
├── .env
├── .env.example
└── artisan
```

## Observações importantes

- Os comandos de PHP, Composer, Artisan e npm devem preferencialmente ser executados dentro dos containers Docker do projeto.
- O projeto usa Inertia.js para renderização das páginas Vue.
- O `node` service do Docker já faz o setup do frontend para desenvolvimento local.
- Antes de continuar com novas implementações, valide que a aplicação subiu corretamente e que as migrations foram executadas com sucesso.

## Próximo passo recomendado

Após a aplicação estar funcionando, o próximo passo é revisar as rotas e as páginas em `routes/web.php` e `resources/js/Pages/` para continuar o desenvolvimento do projeto.
