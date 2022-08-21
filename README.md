# Ansible
  [Ansible](https://www.redhat.com/pt-br/technologies/management/ansible/what-is-ansible) é uma ferramenta que automatiza processo de gerenciamento de configuração, implantação de aplicações, provisionamento e muitos outros processos que antes eram feitas de forma manual. <br>
 O ansible possui uma arquitetura centralizadora no qual um agente chamado "Ansible Controller" se comunicar com os nodes, ou seja, o não precisamos de um agente instalado nos nodes, pois o ele se comunicar diretamente com nodes através do SSH. Desta forma podemos gerenciar centenas de máquinas de um ponto qualquer atrávés de um arquivo com formato [YAML](https://pt.wikipedia.org/wiki/YAML).

# Arquitetura do Ansible
  Fornecerei uma visão geral da arquitetura do ansible. Objetivo não é descrever cada detalhes, mas trazer de forma bem clara os compenentes da arquitetura.
