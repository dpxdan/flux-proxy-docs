
# 📄 Documento de Alterações SQL  
**Data:** 15/06/2025  
**Versão:** 1.0  
**Projeto:** Proxy API - FluxSBC  
**Responsável:** Daniel Paixão - Flux Telecom  

---

## 🔧 Alterações nas Tabelas Existentes

### 🏛️ Tabela `accounts`
- Adicionado campo `int_balance` (`DECIMAL(20,5)`, **NOT NULL**, Default: `0.00000`)  
- Adicionado campo `int_credit_limit` (`DECIMAL(20,5)`, **NOT NULL**, Default: `0.00000`)  
- Adicionado campo `domain_id` (`INT`, **NOT NULL**, Default: `0`)  
- Adicionado campo `id_external` (`INT`, **NOT NULL**, Default: `0`)  

---

### 🏛️ Tabela `cdrs`
- Alterado tipo do campo `uniqueid` para `VARCHAR(255)` **NOT NULL** com Default `''`  
- Removido índice `uniqueid_UNIQUE`  
- Adicionados novos índices para otimização de consultas:  
  - `index_billseconds` sobre o campo `billseconds`  
  - `index_callerid` sobre o campo `callerid`  
  - `index_callednum` sobre o campo `callednum`  
  - `index_disposition` sobre o campo `disposition`  
  - `index_callstart` sobre o campo `callstart`  

---

### 🏛️ Tabela `cdrs_staging`
- Adicionado campo `id` (`INT`, **AUTO_INCREMENT**, **PRIMARY KEY**)  
- Alterado campo `carrier_id` para **NOT NULL** Default `0`  
- Alterado campo `call_id_cadup` para `VARCHAR(120)` **NOT NULL**  

---

### 🏛️ Tabela `sip_devices`
- Alterado campo `id_sip_external` para aceitar **NULL** com Default `NULL`  

---

## 🏗️ Criação de Novas Tabelas

- `api_endpoints`  
- `api_logs`  
- `api_partners`  
- `cdr`  
- `cidade`  
- `cliente_contrato`  
- `clientes`  
- `endpoints`  
- `planos_voip_externos`  
- `uf`  
- `voip_sippeers`  

> As tabelas foram criadas utilizando o engine **InnoDB**, charset `utf8mb3` ou `utf8mb4`, priorizando integridade transacional e suporte a índices relacionais.

---

## ⚙️ Criação de Triggers

- 🔸 `after_insert_cdrs`  
  ➝ Após inserção na tabela `cdrs`, insere registros processados na tabela `cdr`.

- 🔸 `activity_reports`  
  ➝ Gera relatórios de atividades com base nas chamadas do tipo `DID` (entrante) e `outbound` (sainte).

- 🔸 `cdr_records`  
  ➝ Insere registros completos na tabela `cdrs_staging` após cada inserção na tabela `cdrs`.

- 🔸 `clientes_to_accounts`  
  ➝ Insere automaticamente registros na tabela `accounts` quando um novo `cliente` é cadastrado na tabela `clientes`.

---

## 🛠️ Criação de Procedures

- 🔹 `gen_random_uuid()`  
  ➝ Gera um UUID aleatório.

- 🔹 `sincronizar_cdrs_para_cdr()`  
  ➝ Sincroniza registros da tabela `cdrs` para a tabela `cdr` caso não existam.

---

## 🔍 Criação de Views

- 🔸 `view_api_partners`  
  ➝ Consolida dados das tabelas `api_endpoints` e `api_partners` para simplificação de consultas.

---

## 🚫 Remoção de Triggers e Tabelas (Pré-existentes)

- Remoção das triggers:
  - `activity_reports`
  - `cdr_records`

- Drop das tabelas:
  - `api_endpoints` (recriada)
  - `api_logs` (recriada)
  - `api_partners` (recriada)
  - `cdr` (recriada)
  - `cidade` (recriada)
  - `cliente_contrato` (recriada)
  - `clientes` (recriada)
  - `endpoints` (recriada)
  - `planos_voip_externos` (recriada)
  - `uf` (recriada)
  - `voip_sippeers` (recriada)

---

## 🏛️ Considerações Técnicas
- Foi desativado temporariamente o `FOREIGN_KEY_CHECKS` durante a execução do script para evitar conflitos nas dependências relacionais.  
- Recomenda-se revisar os dados após a aplicação deste script, especialmente nas tabelas `cdr`, `cdrs_staging` e `accounts`.  
- As triggers e procedures foram projetadas para manter a consistência entre os dados das tabelas legadas e as novas tabelas operacionais.  

---

## 📌 Histórico de Alterações

| Data       | Versão | Responsável       | Descrição                          |
|-------------|--------|-------------------|-------------------------------------|
| 15/06/2025  | 1.0    | Daniel Paixão     | Criação do schema inicial e ajustes|

---
