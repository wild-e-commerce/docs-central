# Modelagem de Dados 

Descrição da estrutura de persistência serviço **Wild-Pay** (Gateway de Pagamento). Este serviço é responsável por processar transações financeiras de forma isolada, servindo como uma abstração para provedores de pagamento reais e seu modelo de dados serár isolado.
Diferente do Core, aqui serão usados UUIDs para os IDs das transações para aumentar a segurança e dificultar a predição de números de transação.

## Dicionário de Dados

### Tabela: PAYMENT_TRANSACTION

| Campo | Tipo | Obrigatório? | Restrição | Descrição |
| :---: |:---: |:---: |:---: | :---:
| id | UUID | Sim | PK | ID único da transação financeira |
| external_order_ref | string | Sim | Index | O ID do pedido vindo do Wild-E-commerce |
| amount_cents | integer | Sim | - | Valor total em centavos |
| currency | string | Sim | - | Código da moeda (ex: 'BRL') |
| method | string | Sim | - | "'credit_card' | 'pix', 'boleto'." |
| status | string | Sim |- | "pending, authorized, captured, failed, refunded." |
| gateway_response | JSON | Não | - | Resposta bruta do processador (mock) |
| created_at | datetime | Sim | - | Registro de criação |

Campo,Tipo,Obrigatório?,Restrição,Descrição
id,integer,Sim,PK,Identificador interno.
order_id,integer,Sim,Index/UK,Referência do Core.
invoice_number,string,Não,Unique,Gerado após emissão.
access_key,string,Não,Unique,Chave de 44 dígitos (mock).
xml_content,text,Não,-,Conteúdo da nota (mock).
status,string,Sim,-,"processing, issued, error."
issued_at,datetime,Não,-,Data da autorização.

## Diagrama ER 
```mermaid
erDiagram
    PAYMENT_TRANSACTION {
        int uuid PK "Auto-incremento"
        string external_order_ref "ID do pedido vindo do Wild-E-commerce"
        int amount_cents "Valor total em centavos"
        string currency  "Código da moeda (ex: 'BRL')"
        string method "'credit_card' | 'pix', 'boleto'."
        string status "pending, authorized, captured, failed, refunded." 
        json gateway_response "Resposta bruta do processador (mock)"
        datetime created_at "Registro de criação"
        
        }
    style PAYMENT_TRANSACTION fill:#000,stroke:#fff,color:#fff
    
