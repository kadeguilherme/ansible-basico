# Ansible
  [Ansible](https://www.redhat.com/pt-br/technologies/management/ansible/what-is-ansible) é uma ferramenta que automatiza processo de gerenciamento de configuração, implantação de aplicações, provisionamento e muitos outros processos que antes eram feitas de forma manual. <br>
 O ansible possui uma arquitetura centralizadora no qual um agente chamado "Ansible Controller" se comunicar com os nodes, ou seja, não precisamos de um agente instalado nos nodes, pois ele se comunicar diretamente com nodes através do SSH. Desta forma podemos gerenciar centenas de máquinas de um ponto qualquer atrávés de um arquivo com formato [YAML](https://pt.wikipedia.org/wiki/YAML).
 
 Para preparar o ambiente seguir as instruções em **aws-cosole.md** ou **aws-teraform.md**.

# Arquitetura do Ansible
  Fornecerei uma visão geral da arquitetura do ansible. Objetivo não é descrever cada detalhes, mas trazer de forma bem clara os compenentes da arquitetura.
  
   <img src="https://github.com/kadeguilherme/ansible-basico/blob/main/images/architecture-simple.png">
   
##  Inventário 
  
  O inventário é o arquivo em que definimos os nossos hosts, que pode ter formatos como INI, JSON ou YAML. Neste exemplo vamos usar arquivo INI, enquanto arquivo JSON são necessário quando é inventário gerado dinamicamente. Dentro do inventário podemos criar grupos que contenha varios hosts e variáveis. O inventário possui ordem de precedência quando uma opçao é fornecida em outros lugares:

  1. Definidas como -e variáveis extras na linha de comando
  2. Variáveis
  3. Playbook keywords
  4. Command-line options
  5. Configuration settings no arquivo ansible.cfg
  
  Exemplo do iventário básico com variáveis globais e grupo de hosts no formato `.ini`
  
```
[all:vars]  
ansible_python_interpreter=/usr/bin/python3

[webserver]
200.20.11.10
200.20.11.20
200.20.11.30

[loadbalancer]
200;20;11.40
host[1:3].example.com 

[webserver:vars]
versao_nginx=2.1
```
  Os `[]` representa um grupo, os grupos com sufixo `:vars` indicam variáveis para aquele grupo específico, no caso `ansible_python_interpreter=/usr/bin/python3` é passado para todos os hosts ,que é o caminho do Python3, desde o Ansible 2.8 o valor padrão ansible_python_interpreter é `auto_legacy`, ou seja, se existir o Python2 o caminho é `usr/bin/python`. Outro ponto importante é na linha 35 `host[1:3].example.com` expressa um range de numero([1:3]) e possuimos range alfabético ([a:z]).
  

## Opções de Configuração no inventário


| Opção de configuração  | Explicação |
| ------------- | ------------- |
| ansible_host  | Aliases serve para nomear servidores facilitando referência a esse servidores posteriomente.Para utilizar o alias, incluir nome do alias em seguida a variável chamada ansible_host contendo o endereço IP ou nome de host correspondente do servidor. Por exemplo, no seu arquivo de inventário: <br>server1 ansible_host=203.0.113.111 |
| ansible_user  | Usado para logar como usário remoto via SSH. <br>ansible_user=michael. |
| ansible_port  | A porta que seu SSH server está escutando. <br>ansible_port=50822 |
|ansible_ssh_private_key_file |A chave SSH usada para o log in. <br>ansible_ssh_private_key_file=/path/to/id_rsa|

  
  
  
  
  
# Comandos ad hoc
Ansible Ad Hoc são comandos da CLI usados para tarefas simples, uma tarefa simples seria verificar se os nós está conectando com o node management. O ad hoc
 e a playbook são comandos idempotente, ou seja, é verificado o estado do nó e caso o estado atual é igual ao estado da playbook ou ad hoc o comando não será executado.
 ## Sintaxe 
 ```
 ansible <hosts> -m <nome_do_modulo> -a <argumentos>
 ```
 Vamos instalar um pacote com ad-hoc
  ## Instalando um pacote httpd
 ```
ansible webservers -m ansible.builtin.yum -a "name=httpd state=installed"
 ```
 
 
 
