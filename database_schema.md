# Modelagem de Dados 

Descrição da estrutura de persistência do ecossistema **Wild-E-Commerce**. A modelagem prioriza a integridade dos dados e a escalabilidade, utilizando tipos de dados que evitam arredondamentos imprecisos.

## Dicionário de Dados

### Tabela: PRODUCT

| Campo | Tipo | Descrição |
| :---: | :---: | :---: |
|id | Integer | Chave primária (Primary Key) |
| name | String | Nome do produto (Obrigatório conforme contrato)
| sku | String | Stock Keeping Unit. Identificador único para logística (Obrigatório) |
| slug | String | Identificador para URLs amigáveis (Ex: produto-x) |
| price_cents | Integer | Valor em centavos. Regra: Proibido usar Float
| stock_quantity | Integer | Saldo de estoque conforme definido no contrato da API
| category_id | Integer | Chave Estrangeira (FK) conectando à tabela CATEGORY

## Diagrama ER (Mermaid)
```mermaid
erDiagram
    CATEGORY ||--o{ PRODUCT : "contém"
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

    style PRODUCT fill:#000,stroke:#fff,color:#fff
    style CATEGORY fill:#000,stroke:#fff,color:#fff

    