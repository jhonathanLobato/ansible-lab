# host_vars - Ansible (Guia Rápido)

## O que é

host_vars é um diretório usado no Ansible para definir variáveis específicas para hosts individuais.
Ele permite customizar o comportamento de cada servidor sem poluir o inventory ou o playbook.

## Estrutura

```
ansible/
├── inventory/
│   └── hosts.ini
├── host_vars/
│   ├── ubuntu.yml
│   └── suse.yml
```


## Como funciona

* O nome do arquivo deve ser igual ao nome do host no inventory
* O Ansible carrega automaticamente essas variáveis
* Elas são aplicadas apenas ao host correspondente


## Exemplo

### Inventory

```
[web]
ubuntu
suse
```

### host_vars/ubuntu.yml

```
nginx_port: 8080
```

### host_vars/suse.yml

```
nginx_port: 9090
```



## Prioridade

As variáveis em host_vars têm prioridade sobre:

* group_vars
* variáveis padrão



## Quando usar

Use host_vars quando:

* Um host precisa de configuração única
* Existem exceções dentro de um grupo
* Você quer evitar lógica condicional no playbook



## Boas práticas

* Use nomes claros e consistentes para hosts
* Evite duplicação de variáveis (prefira `group_vars` quando possível)
* Utilize arquivos `.yml` (YAML padrão do Ansible)


