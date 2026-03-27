# 🚀 Ansible Lab — Automação de Infraestrutura

## 📌 Visão Geral

Este repositório contém um ambiente prático de estudos e experimentação com **Ansible**, focado em automação de infraestrutura moderna.

O projeto simula cenários reais de provisionamento e configuração de servidores, utilizando tanto:

* ☁️ **AWS (ambiente principal)**
* 🖥️ **Ambiente local (Docker ou VMs)**

O objetivo é construir domínio sólido em automação, boas práticas e arquitetura de infraestrutura como código (IaC).

---

## 🏗️ Arquitetura

O ambiente segue o modelo clássico de automação com Ansible:

* **1 Controller (máquina de controle)**
* **N Nodes (instâncias gerenciadas)**

### 🔹 Componentes

* **Controller**

  * Executa playbooks
  * Centraliza inventário, roles e configurações
  * Pode rodar localmente ou em uma EC2

* **Managed Nodes**

  * Instâncias EC2 ou containers locais
  * Configuradas via SSH
  * Representam serviços reais (web, banco, etc.)

---

## 🌐 Topologia

```
                +----------------------+
                |  Ansible Controller  |
                |----------------------|
                |  Inventory           |
                |  Playbooks           |
                |  Roles               |
                +----------+-----------+
                           |
        -----------------------------------------
        |                   |                   |
+---------------+  +---------------+  +---------------+
|   Web Node    |  |   App Node    |  |   DB Node     |
|---------------|  |---------------|  |---------------|
|   Nginx       |  |   Backend     |  | PostgreSQL    |
+---------------+  +---------------+  +---------------+
```

---

## 🧱 Tecnologias Utilizadas

* Ansible
* AWS EC2
* SSH
* Linux (Ubuntu)
* Docker *(ambiente local opcional)*
* Vagrant *(opcional para simulação com VMs)*

---

## 📂 Estrutura do Repositório

```
ansible-lab/
├── inventory/
│   ├── aws.ini
│   └── local.ini
├── playbooks/
│   ├── setup.yml
│   ├── web.yml
│   ├── app.yml
│   └── db.yml
├── roles/
│   ├── common/
│   ├── nginx/
│   ├── app/
│   └── postgres/
├── group_vars/
├── host_vars/
├── ansible.cfg
└── README.md
```

---

## ⚙️ Configuração do Ambiente

### 🔹 Pré-requisitos

* Ansible instalado
* Conta na AWS configurada
* Acesso SSH às instâncias

---

### ☁️ Ambiente AWS

1. Criar instâncias EC2 (Ubuntu recomendado)

2. Configurar acesso SSH:

```
chmod 400 sua-chave.pem
ssh -i sua-chave.pem ubuntu@IP_PUBLICO
```

3. Atualizar inventário:

```
[web]
IP_WEB ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/sua-chave.pem

[app]
IP_APP ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/sua-chave.pem

[db]
IP_DB ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/sua-chave.pem
```

---

### 🖥️ Ambiente Local (Opcional)

Utilize containers ou VMs para simular infraestrutura:

#### Exemplo com Docker:

```
docker run -dit --name node1 ubuntu
docker run -dit --name node2 ubuntu
```

Atualize o inventário local:

```
[local]
node1 ansible_connection=docker
node2 ansible_connection=docker
```

---

## 🧪 Execução

### Testar conectividade

```
ansible all -m ping -i inventory/aws.ini
```

### Executar playbook base

```
ansible-playbook -i inventory/aws.ini playbooks/setup.yml
```

### Executar roles específicas

```
ansible-playbook -i inventory/aws.ini playbooks/web.yml
```

---

## 📘 Objetivos de Aprendizado

* Automação de provisionamento
* Organização com roles reutilizáveis
* Gerenciamento de múltiplos ambientes
* Idempotência e boas práticas
* Uso de variáveis e templates (Jinja2)
* Deploy automatizado de aplicações

---

## 🔐 Boas Práticas

* Uso de Ansible Vault para segredos
* Separação de ambientes (dev/staging/prod)
* Playbooks idempotentes
* Estrutura modular com roles
* Versionamento completo no Git

---

## 💡 Proposta do Projeto

Este repositório é apenas um laboratório, mas serve como base evolutiva para:

* Simular ambientes reais de produção
* Validar estratégias de automação
* Construir portfólio DevOps sólido
