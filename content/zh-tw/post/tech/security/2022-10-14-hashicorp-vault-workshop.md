---
title: "HashiCorp Vault 實戰工作坊 - 建構零信任安全策略"
url: hashicorp-vault-workshop
# date: 2022-10-14T14:06:16+08:00
date: 2022-10-14T15:30:16+08:00
author: androchentw
type: post
categories:
  - tech
tags:
  - security
  - sre
share_img: https://images.unsplash.com/photo-1603899122634-f086ca5f5ddd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1974&q=80
series: security
---

<img style="width:60%;" src="https://images.unsplash.com/photo-1603899122634-f086ca5f5ddd?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1974&q=80">
<p align="center"><sub><sup>
  Photo by <a href="https://unsplash.com/@franckinjapan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Franck</a> on <a href="https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
</sup></sub></p>

## Overview

### Challenges 現況 挑戰

* 隨著 Security 難度提升, DevOps 及自動化開發維運等工具漸起, API Secret Management 及 Data Security 等議題益發重要。

### Objectives 目標 效益

* [《歐立威科技 2022 研討會》10/14 | 【線上】Vault 實戰工作坊：建構零信任安全策略](https://www.accupass.com/event/2209050743003859674870): 透過實作教學，深入了解 HashiCorp 零信任安全模型，該模型基於身份的存取和安全性原則。學習到 Vault 基礎知識、並且將實際上手操作，體驗動態資料庫存取憑證、轉換和傳輸加密引擎（應用級加密）、轉換標記化加密引擎、金鑰管理加密引擎等等的 Vault 企業版的進階功能。

### KRs 成果

* [x] 2022-10-14 參與並完成 workshop 內容, 整理筆記

<!--more-->

## Materials

* [HashiCorp Vault - 集中控管身分辨識和密鑰，保障資訊安全 - omnisoftware 歐立威科技](http://www.omniwaresoft.com.tw/hashicorp_vault/)
* [零信任白皮書](https://www.datocms-assets.com/2885/1602637867-zerotrustwhitepaperv4digital.pdf)
* [介紹影片](https://www.hashicorp.com/resources/introduction-to-zero-trust-security)
* [Vault Workshop Slide](https://hashicorp.github.io/field-workshops-vault/slides/multi-cloud/vault-oss#1)
* [Screenshots](https://imgur.com/a/txQhyeZ)

## Track 1 - Vault Basics

* Learn how to setup and run a Vault server and manage its secrets.

1. The Vault CLI
2. Your First Secret
3. The Vault API
4. Run a Production Server
5. Use the KV V2 Secrets Engine
6. Use the Userpass Auth Method
7. Use Vault Policies

```sh
# Session 1. The Vault CLI
vault server -dev -dev-listen-address=0.0.0.0:8200 -dev-root-token-id=root
# Log into the Vault UI with Method set to Token and Token set to root.

# Session 2. Your First Secret
vault kv put secret/my-first-secret age=<age>

# Session 3. The Vault API
curl http://localhost:8200/v1/sys/health | jq
curl --header "X-Vault-Token: root" http://localhost:8200/v1/secret/data/my-first-secret | jq

# Session 4. Run a Production Server
vault server -config=/vault/config/vault-config.hcl
vault operator init -key-shares=1 -key-threshold=1
export VAULT_TOKEN=<root_token>
echo "export VAULT_TOKEN=$VAULT_TOKEN" >> /root/.profile
vault operator unseal
# ** copy paste your <root_token> and <unseal_key>
# Unseal Key 1: dT7573IxHbfzt6EFRR07beM2iBg1W4IRilqm/MbvV8g=
# Initial Root Token: s.ajUx80PEBeLMCMBv49FQsM6j

# Session 5. Use the KV V2 Secrets Engine
vault secrets enable -version=2 kv
vault kv put kv/a-secret value=1234

# Session 6. Use the Userpass Auth Method
vault auth enable userpass
# Be sure to specify an actual username for <name> and a password for <pwd> without the angle brackets.
vault write auth/userpass/users/<name> password=<pwd>
vault login -method=userpass username=<name> password=<pwd>
# Both of these login methods give you a Vault token with Vault's default policy that grants some very limited capabilities. A yellow warning message tells us that we currently have the VAULT_TOKEN environment variable set and that we should either unset it or set it to the new token. Let's unset it:
unset VAULT_TOKEN
vault token lookup

vault kv get kv/a-secret
# You will get an error message because your token is not authorized to read any secrets yet. That is because Vault policies are "deny by default", meaning that a token can only read or write a secret if it is explicitly given permission to do so by one of its policies.

# Session 7. Use Vault Policies
# Edit poilcy.hcl
# Now, create a second user with the same command you used before, selecting a different username and password:
vault write auth/userpass/users/<name2> password=<pwd2>
# add the policies to the Vault server:
vault policy write <user_1> /vault/policies/user-1-policy.hcl
vault policy write <user_2> /vault/policies/user-2-policy.hcl
# assign the new policies to the users:
vault write auth/userpass/users/<user_1>/policies policies=<user_1>
vault write auth/userpass/users/<user_2>/policies policies=<user_2>

# Verify with CLI
unset VAULT_TOKEN
vault login -method=userpass username=<user> password=<pwd>
vault kv get kv/<user>/age
vault kv put kv/<user>/weight weight=150
```

## Track 2 - Vault Dynamic Database Credentials

* Generate dynamic credentials for a MySQL database from Vault.

1. Enable the Database Secrets Engine
2. Configure the Database Secrets Engine
3. Generate and Use Dynamic Database Credentials
4. Renew and Revoke Database Credentials

```sh
# Session 1. Enable the Database Secrets Engine
vault secrets list
vault secrets enable -path=lob_a/workshop/database database

# Session 2. Configure the Database Secrets Engine
vault write lob_a/workshop/database/config/wsmysqldatabase \
  plugin_name=mysql-database-plugin \
  connection_url="{{username}}:{{password}}@tcp(localhost:3306)/" \
  allowed_roles="workshop-app","workshop-app-long" \
  username="hashicorp" \
  password="Password123"
# This will not return anything if successful.
vault read lob_a/workshop/database/config/wsmysqldatabase
mysql -u hashicorp -pPassword123
  \q
# force rotate
vault write -force lob_a/workshop/database/rotate-root/wsmysqldatabase
mysql -u hashicorp -pPassword123
# ERROR 1045 (28000): Access denied for user 'hashicorp'@'localhost' (using password: YES)

vault write lob_a/workshop/database/roles/workshop-app-long \
  db_name=wsmysqldatabase \
  creation_statements="CREATE USER '{{name}}'@'%' IDENTIFIED BY '{{password}}';GRANT ALL ON my_app.* TO '{{name}}'@'%';" \
  default_ttl="1h" \
  max_ttl="24h"

vault write lob_a/workshop/database/roles/workshop-app \
  db_name=wsmysqldatabase \
  creation_statements="CREATE USER '{{name}}'@'%' IDENTIFIED BY '{{password}}';GRANT ALL ON my_app.* TO '{{name}}'@'%';" \
  default_ttl="3m" \
  max_ttl="6m"
  
# Session 3. Generate and Use Dynamic Database Credentials
curl --header "X-Vault-Token: root" "http://localhost:8200/v1/lob_a/workshop/database/creds/workshop-app-long" | jq
vault read lob_a/workshop/database/creds/workshop-app-long
# Key                Value
# ---                -----
# lease_id           lob_a/workshop/database/creds/workshop-app-long/CL4J8MkxsP0wCxkWyCFzGceM
# lease_duration     1h
# lease_renewable    true
# password           BXDWdFnh8RWKyc6-hbKa
# username           v-token-workshop-a-GFDhXgXnUJxRn

vault read lob_a/workshop/database/creds/workshop-app
# Key                Value
# ---                -----
# lease_id           lob_a/workshop/database/creds/workshop-app/Jh0OfLXXcWaRWXAx66uzUiLm
# lease_duration     3m
# lease_renewable    true
# password           eeLfgAknwORHqG-9xYxk
# username           v-token-workshop-a-ADDhO0yP4nleV

# Replace <user_name> with the one generated from the previous command
mysql -u <username> -p
  show databases;
  use my_app;
  show tables;
  describe customers;
  select first_name, last_name from customers;
  \q
# At least 3 minutes after you generated the credentials, try to connect to the MySQL server again
# You should get an error like ERROR 1045 (28000): Access denied for user 'v-token-workshop-a-ADDhO0yP4nleV'@'localhost' (using password: YES)

# Session 4. Renew and Revoke Database Credentials
vault read lob_a/workshop/database/creds/workshop-app
# replace <lease_id> with the lease_id 
vault write sys/leases/renew lease_id="<lease_id>" increment="120"
vault write sys/leases/lookup lease_id="<lease_id>"
# Key             Value
# ---             -----
# expire_time     2022-10-14T08:18:39.422263354Z
# id              lob_a/workshop/database/creds/workshop-app/Ioca1iS5vjbUNnSbHgcw9m3I
# issue_time      2022-10-14T08:15:55.536316198Z
# last_renewal    2022-10-14T08:16:39.422263449Z
# renewable       true
# ttl             1m30s

vault read lob_a/workshop/database/creds/workshop-app
vault write sys/leases/revoke lease_id="<lease_id>"
mysql -u <username> -p
# ERROR 1045 (28000): Access denied for user 'v-token-workshop-a-R2025QT2Gb19a'@'localhost' (using password: YES)
```

## Track 3 - Vault Encryption as a Service

* Show how Vault's Transit secrets engine provides encryption as a service.

1. Enable the Transit Secrets Engine
   1. Enable the Transit secrets engine on the Vault server to enable Vault's Encryption-as-a-Service.
2. Create a Key for the Transit Secrets Engine
   1. Create an encryption key for the Transit secrets engine on the Vault server so that it can encrypt and decrypt data stored outside of Vault.
3. Use the Web App Without Vault
   1. Use the python web application without Vault. This will allow users to see sensitive data when looking at database rows.
4. Use the Web App With Vault
   1. Use the python web application with Vault. This will prevent users from seeing sensitive data when looking at new database rows.

```sh
# Session 1. Enable the Transit Secrets Engine
vault secrets list
vault secrets enable -path=lob_a/workshop/transit transit

# Session 2. Create a Key for the Transit Secrets Engine
vault write -f lob_a/workshop/transit/keys/customer-key

# Session 3. Use the Web App Without Vault
# Click the "Add Record" button and add a new record with some fake data. 
# Then check that the new record is not encrypted in the Database View.

# Session 4. Use the Web App With Vault
ps -ef | grep app.py | grep -v grep
kill -9 <PID>
vi /home/vault/transit-app-example/backend/config.ini
# Enabled = False to Enabled = True.
# DynamicDBCreds = False to DynamicDBCreds = True
cd /home/vault/transit-app-example/backend
python3 app.py &
```

## Murmur

* 2022-10-14 最喜歡學習怎麼設計 workshop 😍
