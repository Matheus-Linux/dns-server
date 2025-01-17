# Projeto para automação de Criação de servidores DNS

## Configurando interface de rede

```bash
#apagando configurações existentes
nmcli connection del enp1s0

#Adicionando nova conexão
nmcli connection add con-name LAN type ethernet ifname enp1s0

#Adicionando endereçamento IP
nmcli connection modify LAN ipv4.address 192.168.124.10/24 ipv4.gateway 192.168.124.1 ipv4.method manual

#Reinicializando configurações
nmcli connection down LAN && cmcli connection up LAN 
```

# Adicionar chave ssh ao servidor 

## Lembre-se que esta etapa é feita a partir do servidor Ansible

```bash
#Enviar chave para o servidor alvo
ssh-copy-id <user>@192.168.124.10
```

# Aplicando Playbook para provisionamento do DNS 

## Lembre-se que esse servidor vem com configurações padrões para o "meu domínio".Alterar para o seu caso

```bash
#Criando diretório raiz
mkdir /opt/bind9

#Acessar diretório
cd /opt/bind9

#Clonar repositório com o projeto
git clone https://github.com/Matheus-Linux/dns-server.git

#Aplicar configurações
ansible-playbook <yaml configfile>.yaml -i nodes.yaml 
```

# Topologia do ambiente

![Ansible-bind9](https://github.com/user-attachments/assets/3e533dd9-2359-4956-8d41-a22b441a42c6)


