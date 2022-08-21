# Ansible
  [Ansible](https://www.redhat.com/pt-br/technologies/management/ansible/what-is-ansible) é uma ferramenta que automatiza processo de gerenciamento de configuração, implantação de aplicações, provisionamento e muitos outros processos que antes eram feitas de forma manual. <br>
 O ansible possui uma arquitetura centralizadora no qual um agente chamado "Ansible Controller" se comunicar com os nodes, ou seja, o não precisamos de um agente instalado nos nodes, pois o ele se comunicar diretamente com nodes através do SSH. Desta forma podemos gerenciar centenas de máquinas de um ponto qualquer atrávés de um arquivo com formato [YAML](https://pt.wikipedia.org/wiki/YAML).

# Arquitetura do Ansible
  Fornecerei uma visão geral da arquitetura do ansible. Objetivo não é descrever cada detalhes, mas trazer de forma bem clara os compenentes da arquitetura.
  
   <img src="https://github.com/kadeguilherme/ansible-basico/blob/main/images/architecture-simple.png">
   
##  Inventário 
  
  O inventário é o arquivo em que definimos as nossos hosts, que pode ter formatos como INI, JSON ou YAML. Dentro do inventário podemos criar grupos que contenha varios hosts e variáveis. O inventário possui ordem de precedência quando uma opçao é fornecida em outros lugares:

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

[webserver:vars]
versao_nginx=2.1
```
