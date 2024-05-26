```mermaid
sequenceDiagram
    participant Agones
    participant EOS
    participant Player

    Agones->>Agones: Generates match private key
    Agones->>Agones: Generates match public key
    Player->>Player: Generates player public/private key pair
    Player->>EOS: Sends player public key

    Agones->>Agones: Encrypts connection details with each player's public key
    Agones->>EOS: Sends encrypted details and match public key

    EOS->>Player: Sends encrypted connection details
    EOS->>Player: Sends match public key

    Player->>Player: Decrypts connection details with private key
    Player->>Player: Uses match public key for secure communication

    Note over Agones,Player: After the match ends
    Agones->>Agones: Discards match keys
    Player->>Player: Discards player keys
