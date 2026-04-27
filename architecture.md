```mermaid
graph TD
    %% 사용자 영역
    User([사용자/클라이언트]) -- HTTPS --> CloudFlare[CDN / DNS]

    %% 인프라 영역
    subgraph Public_Subnet [Public Subnet]
        CloudFlare --> ALB[Application Load Balancer]
    end

    subgraph Private_Subnet [Private Subnet]
        ALB --> WebServer1[Web Application Server 1]
        ALB --> WebServer2[Web Application Server 2]
        
        WebServer1 & WebServer2 --> SharedCache[(Redis Cache)]
    end

    %% 데이터 영역
    subgraph Data_Layer [Database Layer]
        WebServer1 & WebServer2 --> PrimaryDB[(Main DB - Write)]
        PrimaryDB --> ReplicaDB[(Replica DB - Read)]
    end

    %% 외부 서비스
    WebServer1 & WebServer2 --> PaymentAPI{외부 결제 API}
    WebServer1 & WebServer2 --> S3[AWS S3 - Static Files]

    %% 스타일링 (시각화 강조)
    style User fill:#f9f,stroke:#333,stroke-width:2px
    style PrimaryDB fill:#f96,stroke:#333,stroke-width:2px
    style ReplicaDB fill:#f96,stroke:#333,stroke-width:2px