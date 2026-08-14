erDiagram
    %% --- ความสัมพันธ์หลัก (Parent -> Child) ---
    profiles ||--o{ products : "sells"
    profiles ||--o{ orders : "buys"
    profiles ||--o{ messages : "sends_receives"
    profiles ||--o{ notifications : "receives"
    profiles ||--o{ refund_requests : "requests"
    profiles ||--o{ product_reports : "reports"
    profiles ||--|| riders : "is_rider"
    profiles ||--|| users : "has_account"
    
    %% --- ความสัมพันธ์เพิ่มเติม ---
    categories ||--o{ products : "categorizes"
    products ||--o{ orders : "included_in"
    products ||--o{ messages : "discussed_in"
    products ||--o{ product_reports : "has_issues"
    
    orders ||--o{ refund_requests : "may_have"
    riders ||--o{ orders : "delivers"

    %% --- คำจำกัดความตารางและโครงสร้างข้อมูล ---

    profiles {
        string student_id PK
        string full_name
        string email
        string role
        string avatar_url
        string department
        timestamp created_at
    }

    users {
        string student_id PK
        string full_name
        string email
        string role
        string avatar_url
        timestamp created_at
    }

    products {
        string product_id PK
        string student_id FK
        string title
        string description
        float price
        string category_id FK
        string image_url
        string status
        int stock
        timestamp created_at
    }

    orders {
        string order_id PK
        string product_id FK
        string buyer_id FK
        string rider_id FK
        string status
        boolean needs_delivery
        boolean seller_accepted
        string delivery_image_url
        string seller_proof_image
        string delivery_address
        string delivery_location
        float delivery_fee
        timestamp created_at
    }

    riders {
        string student_id PK_FK
        string vehicle_type
        string license_plate
        boolean is_active
        float rating
        timestamp created_at
    }

    categories {
        string id PK
        string name
    }

    product_reports {
        string id PK
        string student_id FK
        string product_id FK
        string issue_type
        string description
        string image_url
        string status
        string admin_reply
        string admin_notes
        timestamp created_at
    }

    refund_requests {
        string refund_id PK
        string order_id FK
        string student_id FK
        string reason
        string evidence_url
        string status
        string admin_notes
        timestamp created_at
    }

    messages {
        string id PK
        string sender_id FK
        string receiver_id FK
        string product_id FK
        string content
        boolean is_read
        timestamp created_at
    }

    notifications {
        string id PK
        string student_id FK
        string title
        string message
        string link
        boolean is_read
        timestamp created_at
    }
