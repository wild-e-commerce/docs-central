# Architectural Decision Records 

Este documento registra as decisões técnicas fundamentais do ecossistema Wild-E-Commerce.

## [ADR-001] Representação de Valores Monetários
**Data:** 06/05/2026  
**Status:** Aprovado

### Contexto
Uso de tipos `float` ou `decimal` em bancos de dados pode causar erros de arredondamento em cálculos financeiros.

### Decisão
Todos os campos de preço (ex: `unit_price_cents`) serão armazenados como **inteiros**, representando o valor em centavos.

### Consequências
* **Positivas:** Precisão absoluta em cálculos aritméticos simples.
* **Negativas:** Exige conversão na camada de exibição (frontend).

---

## [ADR-002] Desacoplamento de Gateway e NFe via API
**Data:** 06/05/2026  
**Status:** Aprovado

### Contexto
O sistema precisa processar pagamentos e emitir documentos fiscais. Inicialmente, cogitou-se integrar essas funções diretamente no Core (Monólito).

### Decisão
Separar o **Wild-Pay** (Gateway) e o **Wild-Fiscal** (NFe) em serviços independentes que se comunicam via API REST.

### Consequências
* **Positivas:** Isolamento de falhas, facilidade em trocar de provedor de pagamento, maior segurança de dados.
* **Negativas:** Aumento na complexidade de infraestrutura e necessidade de lidar com consistência eventual.

---

### [ADR-003] Segregação de Documentação e Esquemas de Dados por Subsistema

**Data:** 11/05/2026

**Status:** Aprovado

#### Contexto

Com a decisão de adotar uma arquitetura de microsserviços poliglotas (ADR-002), surgiu a necessidade de definir como os bancos de dados e contratos de cada serviço seriam documentados. Manter tudo em um único dicionário de dados poderia induzir ao erro de acoplamento direto entre as bases (compartilhamento de tabelas).

### Decisão

Cada subsistema (**Wild-Pay**, **Wild-Fiscal**) terá sua própria especificação técnica em arquivos separados no `docs-central`.

* O `database_schema.md` principal será exclusivo para o **Core E-commerce**.
* A comunicação entre os sistemas será documentada via **Contratos de API (JSON)** e não por compartilhamento de banco de dados.
* O Core persistirá apenas metadados de integração e logs de rastreabilidade (ex: `external_id`, `status_code`).

#### Consequências

* **Positivas:** Reforça o conceito de "Bases de Dados Privadas" (Database per Service); evita confusão sobre quais tabelas pertencem a qual domínio; facilita a migração de um serviço específico para outra stack sem impactar a documentação global.
* **Negativas:** Requer navegação entre múltiplos arquivos para ter a visão completa do ecossistema.

---

