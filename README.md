```mermaid
erDiagram
    PROFILES {
        string student_id PK
        string full_name
        string email
        string role
        string avatar_url
        string department
        string created_at
    }

    USERS {
        string student_id PK
        string full_name
        string email
        string role
        string avatar_url
        string created_at
    }

    PRODUCTS {
        string product_id PK
        string student_id FK
        string title
        string description
        string price
        string category_id FK
        string image_url
        string status
        string stock
        string created_at
    }

    ORDERS {
        string order_id PK
        string product_id FK
        string buyer_id FK
        string rider_id FK
        string status
        string needs_delivery
        string seller_accepted
        string delivery_image_url
        string seller_proof_image
        string delivery_address
        string delivery_location
        string delivery_fee
        string created_at
    }

    RIDERS {
        string student_id PK
        string vehicle_type
        string license_plate
        string is_active
        string rating
        string created_at
    }

    CATEGORIES {
        string id PK
        string name
    }

    PRODUCT_REPORTS {
        string id PK
        string student_id FK
        string product_id FK
        string issue_type
        string description
        string image_url
        string status
        string admin_reply
        string admin_notes
        string created_at
    }

    REFUND_REQUESTS {
        string refund_id PK
        string order_id FK
        string student_id FK
        string reason
        string evidence_url
        string status
        string admin_notes
        string created_at
    }

    MESSAGES {
        string id PK
        string sender_id FK
        string receiver_id FK
        string product_id FK
        string content
        string is_read
        string created_at
    }

    NOTIFICATIONS {
        string id PK
        string student_id FK
        string title
        string message
        string link
        string is_read
        string created_at
    }

    PROFILES ||--o{ PRODUCTS : "sells"
    PROFILES ||--o{ ORDERS : "buys"
    PROFILES ||--o{ MESSAGES : "sends_receives"
    PROFILES ||--o{ NOTIFICATIONS : "receives"
    PROFILES ||--o{ REFUND_REQUESTS : "requests"
    PROFILES ||--o{ PRODUCT_REPORTS : "reports"
    PROFILES ||--|| RIDERS : "is_rider"
    PROFILES ||--|| USERS : "has_account"
    
    CATEGORIES ||--o{ PRODUCTS : "categorizes"
    PRODUCTS ||--o{ ORDERS : "included_in"
    PRODUCTS ||--o{ MESSAGES : "discussed_in"
    PRODUCTS ||--o{ PRODUCT_REPORTS : "has_issues"
    
    ORDERS ||--o{ REFUND_REQUESTS : "may_have"
    RIDERS ||--o{ ORDERS : "delivers"
