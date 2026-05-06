# Architectural Decision Records (ADRs)

Este documento registra as decisões técnicas fundamentais do ecossistema Wild-E-Commerce.

---

## [ADR-001] Desacoplamento de Gateway e NFe via API
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

## [ADR-002] Representação de Valores Monetários
**Data:** 06/05/2026  
**Status:** Aprovado

### Contexto
Uso de tipos `float` ou `decimal` em bancos de dados pode causar erros de arredondamento em cálculos financeiros.

### Decisão
Todos os campos de preço (ex: `unit_price_cents`) serão armazenados como **inteiros**, representando o valor em centavos.

### Consequências
* **Positivas:** Precisão absoluta em cálculos aritméticos simples.
* **Negativas:** Exige conversão na camada de exibição (frontend).
