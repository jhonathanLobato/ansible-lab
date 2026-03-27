# Desafios de Ansible — Roadmap Progressivo

Este documento contém uma sequência de desafios práticos para evolução em Ansible, organizados por nível de dificuldade.



# Nível Iniciante — Fundamentos

## Desafio 1 — Conectividade básica

* Criar inventário estático (`hosts.ini`)
* Configurar acesso SSH
* Executar:

```bash
ansible all -m ping
```

Objetivo: validar comunicação entre controller e nodes


## Desafio 2 — Comandos ad-hoc

* Instalar pacote (nginx)
* Criar usuário
* Atualizar sistema

Objetivo: executar tarefas sem playbook


## Desafio 3 — Primeiro playbook

* Criar `setup.yml`
* Atualizar sistema
* Instalar nginx

Objetivo: introdução à automação


## Desafio 4 — Idempotência

* Executar o mesmo playbook múltiplas vezes
* Garantir que não há mudanças desnecessárias

Objetivo: entender comportamento idempotente


## Desafio 5 — Uso de variáveis

* Definir variáveis no playbook:
  * porta
  * nome do pacote
* Utilizar essas variáveis nas tasks

Objetivo: parametrização básica


# Nível Intermediário — Estrutura e Organização

## Desafio 6 — Uso de Roles

* Criar role `nginx`
* Organizar:

  * tasks
  * handlers
  * templates

Objetivo: modularização do código


## Desafio 7 — Templates com Jinja2

* Criar template de configuração do nginx
* Utilizar variáveis dinâmicas

Objetivo: geração dinâmica de arquivos


## Desafio 8 — Múltiplos hosts

* Criar grupos:

  * web
  * db
* Configurar inventário com múltiplos nodes

Objetivo: simular ambiente distribuído


## Desafio 9 — Handlers

* Configurar handler para reiniciar nginx
* Garantir que só execute quando necessário

Objetivo: eficiência operacional


## Desafio 10 — Variáveis por ambiente

* Utilizar:

  * `group_vars`
  * `host_vars`

Objetivo: separação de ambientes (dev/staging/prod)


# Nível Avançado — Cenários Reais

## Desafio 11 — Deploy de aplicação

* Subir aplicação simples (Go ou Flask)
* Configurar nginx como proxy reverso

Objetivo: rodar aplicação real


## Desafio 12 — Banco de dados

* Instalar PostgreSQL
* Criar:

  * database
  * usuário
  * permissões

Objetivo: automação de backend


## Desafio 13 — Segurança com Vault

* Utilizar Ansible Vault
* Proteger:

  * senhas
  * credenciais

Objetivo: segurança de dados sensíveis


## Desafio 14 — Integração com CI/CD

* Configurar pipeline com GitHub Actions
* Executar playbooks automaticamente

Objetivo: automação contínua


## Desafio 15 — Infraestrutura completa

* Provisionar infraestrutura com Terraform
* Configurar com Ansible:

  * web
  * aplicação
  * banco de dados

Objetivo: fluxo completo de DevOps

