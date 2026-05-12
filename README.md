# 8583_20022_UPS
A system using a custom intermediate data format allowing for interchangeability of both financial message standards.
flowchart LR
    subgraph Ingress Layer
        A[ISO 8583 TCP/IP] -->|Raw Bytes| C(Legacy Translator)
        B[ISO 20022 REST] -->|XML Payload| D(Modern Translator)
    end
    
    subgraph Core Switch
        C -->|ISF POJO| E{ISF Routing Engine}
        D -->|ISF POJO| E
    end
    
    subgraph Egress Layer
        E -->|ISF POJO| F(Legacy Translator)
        E -->|ISF POJO| G(Modern Translator)
        F -->|Raw Bytes| H[ISO 8583 TCP/IP]
        G -->|XML Payload| I[ISO 20022 REST]
    end
