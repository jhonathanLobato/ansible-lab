# Inventário Dinâmico no Ansible (Guia Rápido)


## O que é

O inventário dinâmico permite que o Ansible descubra automaticamente os hosts, sem precisar definir manualmente IPs ou nomes no arquivo `hosts.ini`.
Em vez de um inventário estático, o Ansible consulta uma fonte externa (como AWS, Azure, etc.) e gera a lista de servidores em tempo real.



## Como funciona

* Utiliza plugins de inventário (ex: `aws_ec2`)
* Consulta APIs externas (ex: AWS EC2)
* Retorna hosts dinamicamente com base em filtros



## Estrutura básica

```id="n4jq0u"
ansible/
├── inventory/
│   ├── hosts.ini
│   └── aws_ec2.yml
```


## Exemplo (AWS EC2)

Arquivo: `inventory/aws_ec2.yml`

```yaml id="v7r4ti"
plugin: aws_ec2
regions:
  - sa-east-1

filters:
  instance-state-name: running
```


## Como usar

Listar hosts dinamicamente:

```bash id="p7iklr"
ansible-inventory -i inventory/aws_ec2.yml --list
```

Executar comandos:

```bash id="g2mjfq"
ansible -i inventory/aws_ec2.yml all -m ping
```


## Recursos avançados

### Agrupar automaticamente por tags

```yaml id="2y4snb"
keyed_groups:
  - key: tags.Name
  - key: tags.Environment
```


## Vantagens

* Elimina manutenção manual de inventário
* Escala automaticamente com a infraestrutura
* Integra com ambientes em nuvem
* Reduz erros humanos


## Pré-requisitos

* Collection `amazon.aws` instalada
* Bibliotecas Python (`boto3`, `botocore`)
* Credenciais AWS configuradas (`aws configure`)



## Quando usar

* Ambientes em nuvem (AWS, Azure, GCP)
* Infraestrutura dinâmica (auto scaling)
* Projetos DevOps com múltiplos servidores


## Resumo
O inventário dinâmico transforma o Ansible em uma ferramenta adaptável à infraestrutura moderna, permitindo automação baseada no estado real dos ambientes, sem dependência de listas estáticas de servidores.
