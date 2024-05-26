flowchart TD
    A[Agones] -->|Generates match private key| B[Match Private Key]
    A -->|Generates match public key| C[Match Public Key]

    E[Player] -->|Generates player public/private key pair| F[Player Public Key]
    E --> G[Player Private Key]

    subgraph Key Exchange
        B -->|Encrypts connection details with each player's public key| H[Encrypted Connection Details]
        H -->|Sends encrypted details and match public key to| I[EOS]
    end

    subgraph EOS Distribution
        I -->|Sends encrypted details to| J[Player 1]
        I -->|Sends encrypted details to| K[Player 2]
        I -->|Sends encrypted details to| L[Player N]
        I -->|Sends match public key to| J
        I -->|Sends match public key to| K
        I -->|Sends match public key to| L
    end

    subgraph Player Decryption
        J -->|Decrypts connection details with| G
        K -->|Decrypts connection details with| G
        L -->|Decrypts connection details with| G
        J --> M[Decrypted Connection Details]
        K --> M
        L --> M
    end

    subgraph Secure Communication
        M -->|Uses match public key in headers for| N[Secure Communication]
    end

    subgraph Post-Match Cleanup
        A -->|Discards| B
        A -->|Discards| C
        J -->|Discards| G
        K -->|Discards| G
        L -->|Discards| G
    end
