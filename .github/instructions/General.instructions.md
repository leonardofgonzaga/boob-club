---
description: Instruções gerais para o projeto de gestão de clube do livro.
# applyTo: 'Describe when these instructions should be loaded by the agent based on task context' # when provided, instructions will automatically be added to the request context when the pattern matches an attached file
---

<!-- Tip: Use /create-instructions in chat to generate content with agent assistance -->


# Instruções do Projeto

## Stack tecnológica

Este projeto utiliza obrigatoriamente:

- PHP 8.4+
- Laravel 13
- Vue 3 com Composition API e `<script setup>`
- Inertia.js para integração entre Laravel e Vue
- Bootstrap 5 para estilização e componentes visuais
- MySQL 8.4 como banco de dados
- Docker e Docker Compose para ambiente de desenvolvimento
- Vite para gerenciamento e compilação de assets
- PHPUnit para testes automatizados

## Backend – Laravel

- Utilize os padrões e recursos nativos do Laravel.
- Mantenha Controllers enxutos.
- Utilize Form Requests para validação.
- Utilize Policies para autorização.
- Utilize Eloquent ORM para operações com banco de dados.
- Utilize migrations para alterações no banco.
- Utilize Actions e Services quando necessário para organizar regras de negócio.
- Utilize transações em operações que envolvam múltiplas alterações dependentes no banco.
- Nunca coloque regras de segurança exclusivamente no frontend.

## Frontend – Vue 3

- Utilize Composition API e `<script setup>`.
- Utilize Inertia.js para navegação e comunicação com o backend.
- Utilize componentes reutilizáveis sempre que apropriado.
- Organize as páginas em `resources/js/Pages`.
- Organize componentes em `resources/js/Components`.
- Utilize Composables para lógica reutilizável.
- Evite manipular diretamente o DOM.
- Não utilize Axios ou Fetch para substituir funcionalidades que podem ser resolvidas pelo Inertia.
- Utilize os recursos nativos do Vue para gerenciamento de estado local.

## Estilização – Bootstrap 5

- Utilize exclusivamente Bootstrap 5 como framework CSS.
- Prefira classes utilitárias e componentes nativos do Bootstrap.
- Evite criar CSS personalizado quando existir uma solução adequada no Bootstrap.
- Mantenha consistência visual entre as páginas.
- Não utilize Tailwind CSS ou outros frameworks CSS.

## Banco de dados

- Utilize migrations para criar e modificar estruturas.
- Defina relacionamentos Eloquent corretamente.
- Utilize índices quando necessário.
- Evite consultas desnecessárias e problemas de N+1.
- Utilize transações para operações que precisem de consistência.
- Nunca execute alterações estruturais diretamente no banco sem uma migration.

## Testes – PHPUnit

- Crie testes para novas funcionalidades e regras de negócio.
- Utilize Feature Tests para validar fluxos completos e requisições HTTP.
- Utilize Unit Tests para testar classes e regras isoladas.
- Teste validações, permissões, relacionamentos e cenários de erro.
- Utilize factories para gerar dados de teste.
- Não considere uma funcionalidade concluída sem executar os testes correspondentes.

## Docker

- Todos os comandos PHP, Composer, Artisan e NPM devem ser executados nos respectivos containers.
- Utilize Docker Compose para gerenciar os serviços.
- Não dependa de instalações locais de PHP, Composer ou Node.
- Preserve a compatibilidade entre os serviços e suas versões.

## Diretrizes gerais

- Siga os padrões de nomenclatura e organização do Laravel.
- Priorize código simples, legível, reutilizável e de fácil manutenção.
- Evite duplicação de código.
- Não introduza dependências ou tecnologias sem necessidade.
- Não altere funcionalidades existentes sem justificativa.
- Antes de criar novas estruturas, verifique se já existe uma solução semelhante no projeto.
- Não invente métodos, classes ou recursos de bibliotecas.
- Respeite as versões das tecnologias utilizadas.
- Prefira soluções nativas antes de adicionar pacotes externos.
- Ao implementar funcionalidades, considere segurança, desempenho e testabilidade.
- Não faça modernizações ou refatorações fora do escopo solicitado.
