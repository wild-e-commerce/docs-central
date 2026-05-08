## Checkpoint de Engenharia: Wild-E-commerce

---

### 1. Modelagem de Dados (Database Schema)

* **[⚠️] Entidades Core (Pendente/Limpeza):** `USER`, `PRODUCT`, `CATEGORY`. Tabelas limpas, tipadas e com restrições (`PK`, `FK`, `UK`).
* **[⚠️ Lógica de Relacionamento:** Estrutura de subcategorias (`parent_id`) e vínculos entre produtos e categorias.
* **[⚠️] Entidades Transacionais (Pendente/Limpeza):** Organizar as tabelas `ORDER` (cabeçalho) e `ORDER_ITEM` (imutabilidade de preço e quantidade).
* **[⚠️] Entidades de Engajamento (Pendente/Limpeza):** Organizar a tabela `FAVORITE` (N:M entre User e Product).
* **[❌] Bancos de Dados Externos (Pendente):** Modelar a base de dados isolada para o `WILD-PAY` (Transações) e `WILD-FISCAL` (Log de Notas).

### 2. Diagramas (Mermaid / Fluxo)
A representação visual da arquitetura.

* **[⚠️] Diagrama ER Core:** Representação básica das tabelas principais.
* **[⚠️] Sincronização ER:** Atualizar o Mermaid com as tabelas de `ORDER`, `ORDER_ITEM` e `FAVORITE` após a limpeza do Markdown.
* **[❌] Diagrama de Arquitetura de Sistemas:** Desenhar o fluxo de comunicação entre as 3 APIs (Core <-> Gateway <-> NFe).
* **[❌] Diagrama de Sequência:** Mapear o caminho de uma compra (Checkout -> Gateway -> Webhook -> Core -> NFe).

### 3. Contratos de API (Docs Central)
Definição de como os sistemas se comunicam.

* **[⚠️] API Core (Em andamento):** Detalhar endpoints de negócio.
* **[❌] API de Integração (Pendente):** Criar o contrato de interface.
* **[❌] Especificação Wild-Pay (Pendente):** Documentar os endpoints do Gateway (Ex: `POST /v1/transactions`) e o formato do Webhook de retorno.
* **[❌] Especificação Wild-Fiscal (Pendente):** Documentar o endpoint de emissão de nota (Ex: `POST /v1/invoices`).
