# Servidor de Arquivos Corporativo com Samba em Linux

## 📌 Descrição
Implementação de servidor de arquivos em ambiente corporativo utilizando Linux e Samba, com controle de acesso baseado em grupos.

## 🎯 Objetivo
Centralizar arquivos e garantir controle de acesso por setores de forma segura e organizada.

## 🏗️ Infraestrutura

- Virtualização: VMware vSphere
- Sistema Operacional: Oracle Linux 9
- CPU: 4 vCPUs
- Memória: 4GB
- Disco:
  - 40GB (sistema)
  - 500GB (dados)

 ## 💽 Configuração de Disco

```bash
sudo fdisk /dev/sdb
mkfs.ext4 /dev/sdb1
mount /dev/sdb1 /srv/samba
```

## 📁 Estrutura de Diretórios

```
/srv/samba/departamento
├── dev
├── infra
├── redes
├── operacoes
├── security
```

## 🔐 Controle de Acesso

- Permissões 770
- Acesso baseado em grupos
- Isolamento por setor

## 👥 Gerenciamento de Usuários

- Usuários criados sem login interativo
- Associação com grupos específicos
- Controle de acesso via credenciais Samba

## 📦 Instalação do Samba

```bash
sudo dnf install samba samba-client samba-common
```

## 🔥 Firewall

```bash
sudo firewall-cmd --permanent --add-service=samba
sudo firewall-cmd --reload
```

## 🔒 Segurança

- Controle de permissões Linux
- Configuração de SELinux
- Autenticação por usuário e grupo

## 🧪 Testes

Acesso via cliente Windows:

\\servidor\pasta

## 📚 Aprendizados

- Administração de servidores Linux
- Gerenciamento de permissões
- Configuração do Samba
- Segurança em ambientes corporativos
  

## 🚀 Projeto

Este projeto demonstra a implementação de um servidor de arquivos em ambiente corporativo real, incluindo controle de acesso por grupos, segurança e gerenciamento de usuários.

## 👨‍💻 Autor

Desenvolvido por Anderson Gomes Meireles

