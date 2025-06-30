# Projeto DevOps com Vagrant e Ansible

**Administração de Sistemas Abertos** 
**Professor:** Leonidas Francisco de Lima Júnior
**Período:** 2025.1
**Instituto Federal da Paraíba – Campus João Pessoa** 

**Integrantes:**
Ana Clara Marques - 20232380021
Rebea Cabral - 20232380009


## Introdução
Este projeto tem como objetivo o desenvolvimento de competências práticas em DevOps e Infraestrutura como Código (IaC), utilizando as ferramentas Vagrant e Ansible para provisionamento e configuração automatizada de uma infraestrutura virtual composta por quatro máquinas.

O projeto simula um ambiente real de TI com servidores de arquivos, banco de dados, aplicação e cliente, utilizando automação e boas práticas de segurança. É um exemplo prático de como aplicar conceitos de DevOps em uma infraestrutura local, com foco em reprodutibilidade, escalabilidade e documentação.

## Tecnologias Utilizadas

* Vagrant
* Ansible
* VirtualBox
* Debian (box: debian/bookworm64)
* Serviços Linux: SSH, NFS, LVM, DHCP, Chrony, MariaDB, Apache2

## Estrutura da Infraestrutura

Quatro máquinas virtuais configuradas com Vagrant:

1. Servidor de Arquivos (arq)
- IP fixo: 192.168.56.1XX
- Hostname: arq.nome1.nome2.devops
- 3 discos extras de 10GB
- Serviços: DHCP, NFS, LVM

2. Servidor de Banco de Dados (db)
- IP via DHCP
- Hostname: db.nome1.nome2.devops
- Serviços: MariaDB, Autofs

3. Servidor de Aplicação (app)
- IP via DHCP
- Hostname: app.nome1.nome2.devops
- Serviços: Apache2, Autofs

4. Host Cliente (cli)
- IP via DHCP
- Hostname: cli.nome1.nome2.devops
- Memória RAM: 1024MB
- Serviços: Firefox, X11 Forwarding, Autofs

## Provisionamento

### Vagrant
- Arquivo Vagrantfile configura todas as VMs conforme especificações;
- Utiliza o provider VirtualBox.

### Ansible
- Playbooks automatizam a instalação e configuração dos serviços nas VMs.

- Tarefas aplicadas a todas as VMs:
  - Atualização do sistema
  - Configuração do chrony (NTP)
  - Criação do grupo ifpb e usuários nome1/nome2
  - Configuração segura do SSH
  - Instalação do cliente NFS
  - Permissões sudo para o grupo ifpb

## Organização do Repositório

├── ansible/
│   ├── files
│   ├── ├── clara.key.pub
│   ├── ├── rebeca.key.pub
│   ├── playbooks
│   ├── ├── app.yml
│   ├── ├── cli.yml
│   ├── ├── common.yml
│   ├── ├── db.yml
│   ├── ├── dhcp-arq.yml
│   ├── ├── lvm-arq.yml
│   ├── ├── nfs-arq.yml
│   ├── ├── site.yml
│   ├── ansible.cfg
│   ├── hosts.ini
├── README.md
├── Vagrantfile

## Como Executar o Projeto

Clone este repositório:

```
git clone https://github.com/rebecadc/Projeto-ASA.git
cd projeto-vagrant-ansible
```

Inicie as VMs com o Vagrant:

```
vagrant up
```

Execute os playbooks do Ansible (exemplo com o arq):

```
ansible-playbook -i hosts ansible/playbook-arq.yml
```