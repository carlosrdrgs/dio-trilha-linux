# 🐧 Infraestrutura como Código: Script de Provisionamento

Este projeto faz parte do desafio da **DIO - Trilha Linux**. O objetivo é criar um script em Bash para automatizar a criação de diretórios, grupos de usuários e a definição de permissões e donos de forma massiva.

## 📋 Descrição do Projeto

O script realiza as seguintes tarefas automaticamente:
1. Cria diretórios para departamentos (`/publico`, `/adm`, `/ven`, `/sec`).
2. Cria grupos de usuários para cada departamento.
3. Cria usuários e os adiciona aos grupos específicos.
4. Define as permissões de leitura, escrita e execução para cada diretório.

## 📂 Estrutura de Diretórios e Permissões

| Diretório | Grupo Dono | Permissões | Descrição |
| :--- | :--- | :--- | :--- |
| `/publico` | `root` | **777** | Acesso total para todos os usuários. |
| `/adm` | `GRP_ADM` | **770** | Leitura/Escrita/Execução para o grupo ADM. |
| `/ven` | `GRP_VEN` | **770** | Leitura/Escrita/Execução para o grupo VEN. |
| `/sec` | `GRP_SEC` | **770** | Leitura/Escrita/Execução para o grupo SEC. |

## 👥 Usuários e Grupos

O script provisiona os seguintes usuários e os aloca em seus respectivos grupos:

* **GRP_ADM (Administração):** `carlos`, `maria`, `joao`
* **GRP_VEN (Vendas):** `debora`, `sebastiana`, `roberto`
* **GRP_SEC (Secretariado):** `josefina`, `amanda`, `rogerio`

## 🛠️ Script

```bash
#!/bin/bash

echo "Criando diretórios..."

mkdir /publico
mkdir /adm
mkdir /ven
mkdir /sec

echo "Criando grupos de usuários..."

groupadd GRP_ADM
groupadd GRP_VEN
groupadd GRP_SEC

echo "Criando usuários..."

useradd carlos -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd maria -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM
useradd joao -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_ADM

useradd debora -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd sebastiana -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN
useradd roberto -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_VEN

useradd josefina -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd amanda -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC
useradd rogerio -m -s /bin/bash -p $(openssl passwd -crypt Senha123) -G GRP_SEC

echo "Especificando permissões dos diretórios..."

chown root:GRP_ADM /adm
chown root:GRP_VEN /ven
chown root:GRP_SEC /sec

chmod 770 /adm
chmod 770 /ven
chmod 770 /sec
chmod 777 /publico

echo "Fim....."
