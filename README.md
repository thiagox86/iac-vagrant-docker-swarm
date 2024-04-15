# iac-vagrant-docker-swarm
Criando um cluster utilizando vagrant + docker swarm

O arquivo Vagrantfile é um arquivo de configuração para o Vagrant, uma ferramenta que permite criar e gerenciar ambientes de desenvolvimento virtualizados. 
Segue uma breve explicação do que cada parte faz:

Definição das Máquinas:
O dicionário machines contém informações sobre três máquinas virtuais: “main”, “node01” e “node02”.
Cada máquina tem atributos como memória, CPU, endereço IP e imagem base (no caso, “bento/ubuntu-22.04”).


Configuração do Vagrant:
- A linha Vagrant.configure("2") do |config| inicia a configuração do Vagrant.
- O loop machines.each do |name, conf| itera sobre cada máquina no dicionário.


Para cada máquina:
Define a máquina com o nome especificado (config.vm.define "#{name}").
- Define a imagem base da máquina (machine.vm.box = "#{conf["image"]}").
- Configura a rede privada com o endereço IP especificado (machine.vm.network "private_network", ip: "10.10.10.#{conf["ip"]}").
- Define as configurações do VirtualBox, como memória e CPUs (vb.name, vb.memory e vb.cpus).
- Executa um script de provisionamento chamado “installDocker.sh”.
- Se o nome da máquina for “main”, executa outro script chamado “main.sh”; caso contrário, executa “node.sh”.


Provisionamento:
Os scripts “installDocker.sh”, “main.sh” e “node.sh” são executados em cada máquina.
O script “installDocker.sh” provavelmente instala o Docker.
Os scripts “main.sh” e “node.sh” podem conter outras configurações específicas para a máquina “main” ou os nós.


Em resumo, esse código cria três máquinas virtuais usando o Vagrant, define suas configurações e provisiona-as com os scripts especificados. 
Cada máquina terá uma imagem base do Ubuntu 22.04 e será configurada de acordo com os parâmetros fornecidos. O objetivo final é criar um ambiente
de desenvolvimento virtualizado com essas máquinas interconectadas.
