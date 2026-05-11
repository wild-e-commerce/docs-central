# Modelagem de Dados 

Descrição da estrutura de persistência serviço **Wild-Pay** (Gateway de Pagamento). Este serviço é responsável por processar transações financeiras de forma isolada, servindo como uma abstração para provedores de pagamento reais e seu modelo de dados serár isolado.
Diferente do Core, aqui serão usados UUIDs para os IDs das transações para aumentar a segurança e dificultar a predição de números de transação.

## Dicionário de Dados

### Tabela: PAYMENT_TRANSACTION

| Campo | Tipo | Obrigatório? | Restrição | Descrição |
| :---: |:---: |:---: |:---: | :---:
| id | UUID | Sim | PK | ID único da transação financeira |
| external_order_ref | string | Sim | Index | O ID do pedido vindo do Wild-E-commerce |
| amount_cents | integer | Sim | - |Valor total em centavos |
| currency | string | Sim | - | Código da moeda (ex: 'BRL') |
| method | string | Sim | - | "'credit_card' | 'pix', 'boleto'." |
| status | string | Sim |- | "pending, authorized, captured, failed, refunded." |
| gateway_response | JSON | Não | - | Resposta bruta do processador (mock) |
| created_at | datetime | Sim | - | Registro de criação |

## Diagrama ER (Mermaid)
```mermaid
erDiagram
    CATEGORY ||--o{ PRODUCT : "contém"
    USER ||--o{ PRODUCT : "favorita"
    PRODUCT {
        int id PK "Auto-incremento"
        string name "Nome do produto"
        string slug "URL amigável (único)"
        string sku "Código único de inventário (Obrigatório)"
        string description "Texto longo/Markdown"
        int price_cents "Preço em centavos"
        int stock_quantity "Quantidade em estoque"
        int category_id FK "Chave estrangeira para CATEGORY"
        datetime created_at "Data de criação UTC"
    }
    CATEGORY {
        int id PK
        string name
        string slug "URL amigável"
    }
    USER {
        int id PK
        string name
        string email
        string role
    }
    ORDER {
        int id PK
        int user_id FK
        string status "Ex: pending, paid, returned"
        int total_cents
        datetime created_at
    }
    ORDER_ITEM {
        int id PK
        int order_id FK
        int product_id
        int quantity
        int unit_price_cents
    }
    FAVORITE {
        int user_id FK
        int product_id FK
        datetime created_at
    }

    style PRODUCT fill:#000,stroke:#fff,color:#fff
    style CATEGORY fill:#000,stroke:#fff,color:#fff
    style USER fill:#000,stroke:#fff,color:#fff
    
