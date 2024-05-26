sequenceDiagram
    participant Agones
    participant EOS
    participant Player1
    participant Player2
    participant PlayerN

    Agones->>Agones: Generates match private key
    Agones->>Agones: Generates match public key
    Agones->>EOS: Shares match public key

    Player1->>Player1: Generates player1 public/private key pair
    Player2->>Player2: Generates player2 public/private key pair
    PlayerN->>PlayerN: Generates playerN public/private key pair
    Player1->>EOS: Shares player1 public key
    Player2->>EOS: Shares player2 public key
    PlayerN->>EOS: Shares playerN public key

    EOS->>Agones: Sends player public keys

    Agones->>Agones: Encrypts connection details with each player's public key
    Agones->>EOS: Sends encrypted details to EOS

    EOS->>Player1: Sends encrypted connection details and match public key
    EOS->>Player2: Sends encrypted connection details and match public key
    EOS->>PlayerN: Sends encrypted connection details and match public key

    Player1->>Player1: Decrypts connection details with private key
    Player2->>Player2: Decrypts connection details with private key
    PlayerN->>PlayerN: Decrypts connection details with private key

    Player1->>Agones: Uses match public key for secure communication
    Player2->>Agones: Uses match public key for secure communication
    PlayerN->>Agones: Uses match public key for secure communication

    Note over Agones,Player1,Player2,PlayerN: After the match ends all keys are discarded
    Agones->>Agones: Discards match keys
    Player1->>Player1: Discards player keys
    Player2->>Player2: Discards player keys
    PlayerN->>PlayerN: Discards player keys
