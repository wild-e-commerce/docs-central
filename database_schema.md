# Modelagem de Dados 

Descrição da estrutura de persistência do ecossistema **Wild-E-Commerce**. A modelagem prioriza a integridade dos dados e a escalabilidade, utilizando tipos de dados que evitam arredondamentos imprecisos.

## Diagrama ER (Mermaid)
```mermaid
erDiagram
    CATEGORY ||--o{ PRODUCT : "contém"
    PRODUCT {
        int id PK "Auto-incremento"
        string name "Nome do produto"
        string slug "URL amigável (único)"
        string description "Texto longo/Markdown"
        int price_cents "Preço em centavos (evita erros de float)"
        int stock "Quantidade em estoque"
        datetime created_at "Data de criação UTC"
    }
    CATEGORY {
        int id PK
        string name
        string slug "URL amigável"
    }

    style PRODUCT fill:#000,stroke:#fff,color:#fff
    style CATEGORY fill:#000,stroke:#fff,color:#fff