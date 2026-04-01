# Comandos Ad-Hoc

Comando para executar o ping e verificar conexão:
- `ansible <host> -m ping`

Para ver os valores das variáveis:
- `ansible <host> -m debug -a var=nome-da-variavel`

Instalando um pacote:
- `ansible <host> -m package -a "name=nome-pacote state=present" --become`

Removendo pacote
- `ansible <host> -m package -a "name=nome-pacote state=ansent"`


O pacote pode assumir os valores:
- apt → Debian/Ubuntu
- yum / dnf → RedHat/CentOS
- zypper → SUSE
- package → genérico (melhor prática)

O state pode assumir um desses valores:
- present	instalado
- absent	removido
- latest	versão mais recente


Adicionando variavel inline
- `ansible <host> --extra-vars nome-variavel=valor-variavel -m debug -a var=nome-variavel`
- `ansible <host> --e nome-variavel=valor-variavel -m debug -a var=nome-variavel`

