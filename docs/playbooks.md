# Documentação Completa sobre Playbooks no Ansible


# O que é um Playbook?

Um playbook é um arquivo em YAML que define um conjunto de instruções (tarefas) que o Ansible executa em um ou mais hosts.

> Ele descreve o estado desejado do sistema.


# Estrutura básica de um Playbook

```yaml
- name: Nome do play
  hosts: web
  become: true

  tasks:
    - name: Instalar nginx
      package:
        name: nginx
        state: present
```



# Componentes principais

## 1. Play

Um play é um bloco que define:

* quais hosts serão afetados
* quais tarefas serão executadas

```yaml
- name: Meu play
  hosts: all
```



## 2. Hosts

Define onde o play será executado:

```yaml
hosts: web
hosts: db
hosts: all
```



## 3. Become (elevação de privilégio)

Permite executar como root:

```yaml
become: true
```


## 4. Tasks

Lista de ações executadas em ordem:

```yaml
tasks:
  - name: Instalar pacote
    package:
      name: nginx
      state: present
```


# Módulos dentro de Tasks

Cada task usa um módulo:

```yaml
- name: Criar arquivo
  file:
    path: /tmp/teste.txt
    state: touch
```



# Execução

Executar playbook:

```bash
ansible-playbook playbook.yml
```



# Variáveis em Playbooks

## Definição direta

```yaml
vars:
  porta: 80
```



## Uso

```yaml
msg: "Porta: {{ porta }}"
```



## Variáveis externas

```bash
ansible-playbook playbook.yml -e "porta=8080"
```



# Precedência de variáveis (resumo)

1. extra-vars (`-e`)
2. host_vars
3. group_vars
4. vars no playbook



# Condições (`when`)

Permite executar tarefas condicionalmente:

```yaml
- name: Instalar nginx apenas no Ubuntu
  apt:
    name: nginx
    state: present
  when: ansible_os_family == "Debian"
```



# Loops

Executar repetição:

```yaml
- name: Instalar pacotes
  package:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - git
    - curl
```



# Register (capturar saída)

Captura resultado de uma task:

```yaml
- name: Verificar serviço
  command: systemctl status nginx
  register: resultado
```

Uso:

```yaml
msg: "{{ resultado.stdout }}"
```



# Controle de erro

## Ignorar erro

```yaml
ignore_errors: true
```



## Condição de falha

```yaml
failed_when: resultado.rc != 0
```



## Forçar mudança

```yaml
changed_when: false
```



# Handlers

Executam ações quando notificados:

```yaml
tasks:
  - name: Alterar config
    template:
      src: nginx.conf.j2
      dest: /etc/nginx/nginx.conf
    notify: Reiniciar nginx

handlers:
  - name: Reiniciar nginx
    service:
      name: nginx
      state: restarted
```



# Templates (Jinja2)

Permite criar arquivos dinâmicos:

```yaml
- name: Aplicar template
  template:
    src: arquivo.j2
    dest: /etc/app.conf
```



# Tags

Executar partes específicas:

```yaml
- name: Instalar nginx
  package:
    name: nginx
    state: present
  tags: nginx
```

Execução:

```bash
ansible-playbook play.yml --tags nginx
```



# Includes e Imports

## include_tasks

```yaml
- include_tasks: tarefas.yml
```



## import_tasks

```yaml
- import_tasks: tarefas.yml
```



## include_role

```yaml
- include_role:
    name: nginx
```



# Facts

Informações automáticas do sistema:

```yaml
- name: Mostrar OS
  debug:
    var: ansible_os_family
```

---

# Estratégias de execução

## Execução padrão

```yaml
strategy: linear
```



## Execução paralela

```yaml
strategy: free
```



## Rolling update

```yaml
serial: 2
```



# Ansible Vault

Criptografar variáveis:

```bash
ansible-vault encrypt secrets.yml
```



# Boas práticas

* Sempre usar `name` nas tasks
* Manter playbooks simples
* Evitar lógica complexa (use roles)
* Separar variáveis por ambiente
* Usar templates para configs



# Erros comuns

* YAML mal indentado
* Variáveis mal definidas
* Não usar `become`
* Misturar lógica demais no playbook



# Mentalidade correta

Playbooks devem ser:

* Declarativos
* Idempotentes
* Reutilizáveis
* Previsíveis



# Exemplo completo

```yaml
- name: Setup Web Server
  hosts: web
  become: true

  vars:
    porta: 80

  tasks:
    - name: Instalar nginx
      package:
        name: nginx
        state: present

    - name: Aplicar configuração
      template:
        src: nginx.conf.j2
        dest: /etc/nginx/nginx.conf
      notify: Reiniciar nginx

  handlers:
    - name: Reiniciar nginx
      service:
        name: nginx
        state: restarted
```

