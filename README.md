# Amex Fraud & Analytics Microservice

Enterprise backend microservice built with Java 25, Spring Boot 3, Hexagonal Architecture, and Kafka, designed for real-time fraud detection and high-performance financial data analysis.

## Database Architecture (3NF Normalized)
Designed to securely handle transactions, customer profiles, merchants, and fraud rules without data redundancy.

```mermaid
erDiagram
    CUSTOMERS ||--o{ CARDS : owns
    CUSTOMERS ||--o{ TRANSACTIONS : makes
    MERCHANTS ||--o{ TRANSACTIONS : receives
    TRANSACTIONS ||--|{ FRAUD_ALERTS : triggers

    CUSTOMERS {
        long id PK
        string full_name
        string email
        string risk_level
    }

    CARDS {
        long id PK
        long customer_id FK
        string card_hash
        string status
    }

    MERCHANTS {
        long id PK
        string name
        string category
        boolean is_trusted
    }

    TRANSACTIONS {
        long id PK
        long card_id FK
        long merchant_id FK
        decimal amount
        string currency
        string ip_address
        timestamp created_at
    }

    FRAUD_ALERTS {
        long id PK
        long transaction_id FK
        string rule_triggered
        string status
    }
