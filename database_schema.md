# Modelagem de Dados 

Descrição da estrutura de persistência do ecossistema **Wild-E-Commerce**. A modelagem prioriza a integridade dos dados e a escalabilidade, utilizando tipos de dados que evitam arredondamentos imprecisos.

## Dicionário de Dados

### Tabela: PRODUCT

| Campo | Tipo | Obrigatório? | Restrição | Descrição |
| :---: | :---: | :---: | :---: | :---: |
| id | Integer | Sim | Primary key | Chave primária (Primary Key) |
| name | String | Sim | | Nome do produto (Obrigatório conforme contrato)
| description | String | Não | | Detalhes do Produto (Markdown)
| price_cents | Integer | Sim | | Valor em centavos. Regra: Proibido usar Float
| stock_quantity | Integer | Sim | | Saldo de estoque conforme definido no contrato da API
| category_id | Integer | Sim | Foreign Key | Chave Estrangeira (FK) conectando à tabela CATEGORY
| sku | String | Sim | Unique | Stock Keeping Unit. Identificador único para logística (Obrigatório) |
| slug | String | Sim | Unique | Identificador para URLs amigáveis (Ex: produto-x) |

:warning: Tenho que consertar o diagrama antes de adicionar mais tabelas!

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

    style PRODUCT fill:#000,stroke:#fff,color:#fff
    style CATEGORY fill:#000,stroke:#fff,color:#fff
    style USER fill:#000,stroke:#fff,color:#fff
    
