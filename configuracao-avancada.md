# ⚙️ Configuração Avançada – Servidor de Arquivos Samba

## 📁 Criação da Estrutura de Diretórios

```bash
sudo mkdir -p /srv/samba/departamento

sudo mkdir /srv/samba/departamento/dev
sudo mkdir /srv/samba/departamento/infra
sudo mkdir /srv/samba/departamento/redes
sudo mkdir /srv/samba/departamento/operacoes
sudo mkdir /srv/samba/departamento/security
```

---

## 🔐 Configuração de Permissões

```bash
sudo chown -R root:dev /srv/samba/departamento/dev
sudo chmod -R 770 /srv/samba/departamento/dev

sudo chown -R root:infra /srv/samba/departamento/infra
sudo chmod -R 770 /srv/samba/departamento/infra

sudo chown -R root:redes /srv/samba/departamento/redes
sudo chmod -R 770 /srv/samba/departamento/redes

sudo chown -R root:operacoes /srv/samba/departamento/operacoes
sudo chmod -R 770 /srv/samba/departamento/operacoes

sudo chown -R root:security /srv/samba/departamento/security
sudo chmod -R 770 /srv/samba/departamento/security
```

---

## 👥 Criação de Grupos

```bash
sudo groupadd dev
sudo groupadd infra
sudo groupadd redes
sudo groupadd operacoes
sudo groupadd security
```

---

## 👤 Criação de Usuários

```bash
sudo useradd -m -g dev -s /sbin/nologin dev_user1
sudo useradd -m -g infra -s /sbin/nologin infra_user1
sudo useradd -m -g redes -s /sbin/nologin redes_user1
sudo useradd -m -g operacoes -s /sbin/nologin operacoes_user1
sudo useradd -m -g security -s /sbin/nologin security_user1
```

---

## 🔑 Configuração de Senhas no Samba

```bash
sudo smbpasswd -a dev_user1
sudo smbpasswd -a infra_user1
sudo smbpasswd -a redes_user1
sudo smbpasswd -a operacoes_user1
sudo smbpasswd -a security_user1
```

---

## 🔄 Associação de Usuários aos Grupos

```bash
sudo usermod -aG dev dev_user1
sudo usermod -aG infra infra_user1
sudo usermod -aG redes redes_user1
sudo usermod -aG operacoes operacoes_user1
sudo usermod -aG security security_user1
```

---

## 📦 Instalação do Samba

```bash
sudo dnf install samba samba-client samba-common
```

---

## ⚙️ Configuração do smb.conf

```ini
[global]
   workgroup = SAMBA
   security = user

[dados]
   path = /srv/samba/departamento
   valid users = @dev @infra @redes @operacoes @security
   read only = no
   browseable = yes
```

---

## 🔥 Firewall

```bash
sudo firewall-cmd --permanent --add-service=samba
sudo firewall-cmd --reload
```

---

## 🔒 Configuração do SELinux

### ✅ Ajustar contexto

```bash
sudo semanage fcontext -a -t samba_share_t "/srv/samba/departamento(/.*)?"
sudo restorecon -Rv /srv/samba/departamento
```

---

### ✅ Liberar acesso do Samba

```bash
sudo setsebool -P samba_export_all_rw 1
```

---

## 🧪 Testes de Acesso

No Windows:

```
\\servidor\pasta
```

---

## 🛑 Encerramento de Sessões (Windows)

```bash
net use
net use * /delete
```

---

## 📌 Observações

- Usuários criados sem acesso interativo ao sistema
- Controle de acesso baseado em grupos
- Permissões restritas por diretório
- Ambiente adaptado para cenário corporativo

---

## 📚 Objetivo Técnico

Este documento demonstra a implementação prática de:

- Controle de acesso em Linux
- Gerenciamento de usuários e grupos
- Configuração de servidor de arquivos com Samba
- Integração com políticas de segurança (SELinux e Firewall)

