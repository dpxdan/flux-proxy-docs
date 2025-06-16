
# VoIP Sync — Documentação Técnica

**Autor:** Daniel Paixão — Flux Telecom  
**Framework:** CodeIgniter 2.x  
**Linguagem:** PHP 7.3  

---

## 🎯 Descrição do Módulo

O módulo **VoIP Sync** tem como objetivo realizar a integração entre o sistema interno da Flux Telecom e APIs de parceiros, permitindo a sincronização de dados de VoIP, como SIP Peers e registros de chamadas (CDRs). Este módulo é responsável por garantir a consistência dos dados, facilitar o monitoramento das conexões e manter o ambiente VoIP atualizado.

---

## 🏗️ Estrutura dos Arquivos

```
/application/controllers/VoipSync.php
/application/models/Api_model.php
/application/models/Voip_model.php
```

---

## 🔹 Controller: VoipSync

**Responsável por:**  
Orquestrar as rotinas de sincronização entre o sistema interno e APIs externas, além de disponibilizar ações manuais, automáticas e de consulta.

### Funcionalidades:

- 🔄 **Sincronização de CDRs (Call Detail Records)**
- 🔄 **Sincronização de SIP Peers**
- ✅ **Verificação de status das APIs**
- 🗒️ **Gerenciamento de logs de sincronização**
- 🔧 **Execução manual das rotinas de sincronização**
- ⏰ **Execução agendada via Cronjob**
- 🔍 **Validação e tratamento de dados durante a sincronização**

---

## 🔸 Model: Api_model

**Responsável por:**  
Gerenciar a comunicação direta com as APIs dos parceiros, lidando com autenticação, requisições HTTP e tratamento de respostas.

### Funcionalidades:

- 🔐 **Autenticação (Token, Basic, OAuth ou personalizada)**
- 🌐 **Requisições HTTP (GET, POST, PUT, DELETE)**
- 📡 **Obtenção de CDRs e SIP Peers de APIs externas**
- ✅ **Validação e parsing das respostas**
- 🔧 **Gerenciamento dos dados de conexão dos parceiros**
- 🗒️ **Registro de logs de chamadas às APIs**

---

## 🔸 Model: Voip_model

**Responsável por:**  
Gerenciar os dados VoIP locais, como SIP Peers, CDRs, e vínculos com clientes.

### Funcionalidades:

- 📑 **Gerenciamento de SIP Peers (inserção, atualização e remoção)**
- 🔗 **Vinculação de SIP Peers aos clientes**
- 📞 **Consulta de registros de chamadas (CDRs)**
- ⚙️ **Atualização e consulta do status dos SIP Peers (ativo/inativo)**
- 📜 **Manutenção de contratos vinculados aos SIP Peers**
- 🗒️ **Logs e histórico de alterações dos dados VoIP**

---

## ⚙️ Requisitos Técnicos

- PHP 7.3  
- CodeIgniter 2.x  
- Banco de Dados MySQL/MariaDB  
- Extensões PHP habilitadas:
  - cURL
  - mbstring
  - json

---

## 🔥 Observações

- Este módulo é preparado para ser executado tanto manualmente via interface (se aplicável) quanto automaticamente via cronjob.
- Toda a comunicação com APIs externas é registrada para fins de auditoria e troubleshooting.
- A modelagem segue o padrão tradicional de desenvolvimento da Flux Telecom, priorizando estabilidade, desempenho e legibilidade.

---

## 📧 Suporte

**Desenvolvedor:** Daniel Paixão  
**Empresa:** Flux Telecom  
**Contato:** (inserir e-mail interno ou canal da empresa)

---

## 🏛️ Direitos

Este projeto é parte integrante dos sistemas proprietários da Flux Telecom. Seu uso, reprodução ou distribuição estão sujeitos às normas internas da empresa.

---

## 🏗️ Status do Projeto

🚧 Em desenvolvimento | 🔄 Em testes | ✅ Estável  
(Selecionar conforme o status atual)

---

## 📌 Histórico de Atualizações

| Data       | Versão | Descrição                      |
| ----------- | ------ | ------------------------------ |
| 15/06/2025 | 1.0    | Documento inicial de funcionalidades |
