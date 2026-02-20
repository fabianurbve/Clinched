🛡️ Clinched v1.0 - Secure Password Vault
=========================================

Clinched is a high-security desktop password manager built on a Zero-Knowledge Architecture. Beyond simple credential storage, this project implements industry-standard cryptographic protocols and optimized resource management for production-grade software deployment.

🛠️ Technical & Cryptographic Specifications

- Key Derivation Function (KDF): Implements PBKDF2-HMAC-SHA256 with 480,000 iterations. This configuration exceeds OWASP’s standard recommendations, providing superior resistance against dictionary attacks and GPU-accelerated brute-force attempts.

- Symmetric Encryption: Utilizes the Fernet specification, ensuring that encrypted data cannot be read or manipulated without the correct key. It employs AES-128 in CBC mode with an HMAC for message authentication.

- Dynamic Path Management: The software is context-aware; it detects its execution state through sys.frozen inspection. When running as a binary (.exe), it dynamically re-points the BASE_DIR to sys.executable. This prevents data loss by ensuring the database remains in the user's directory rather than in volatile Windows temporary folders (_MEIPASS).

- Data Integrity Protocol: Features a Shadow Copying system that generates a vault_backup.db upon every successful session termination. The system performs a physical validation of the database file before initialization, triggering automatic recovery protocols if the primary file is missing or corrupted.

📖 Responsible Use Manual (Security Protocols)

1. Master Password Hygiene

  Entropy: A passphrase of at least 16 characters is highly recommended.

  Irrecoverability: By design (Zero-Knowledge), the master password is never stored. If forgotten, your data is mathematically inaccessible. There is no "backdoor" or "reset" function.

2. Clipboard Security

  When viewing a password, it can be copied to the clipboard.

  Software Safeguard: Clinched implements an automated cleanup protocol that wipes the system clipboard upon closing the application to mitigate risks from "Clipboard Sniffing" malware.

3. Professional Deployment

  Run create_shortcut.py for a clean deployment on your workstation. This script links the binary with the Clinched.ico asset and sets the correct working directory for persistent database access.

⚠️ Limited Liability & Safety Warnings

1. Compromised Environments: Clinched does not protect against active Keyloggers or Screen-scrapers on a compromised OS. Always run this software on a clean, trusted system.

2. External Manipulation: Manually modifying entries within vault.db using external SQLite editors may corrupt the encryption schema, leading to permanent data loss for those entries.

3. External Backups: While the program creates a local shadow copy (vault_backup.db), it is the user's responsibility to periodically back up the vault.db file to a separate physical medium or encrypted cloud storage.

📂 Project Module Structure

- main.py: The orchestrator. Manages the Tkinter UI state, session lifecycle, and clipboard security.

- crypto_utils.py: The cryptographic abstraction layer (PBKDF2, AES, Fernet).

- database_manager.py: The persistence layer. Manages SQLite transactions, path resolution, and disaster recovery.

- create_shortcut.py: Deployment automation script using WSH Shell for Windows integration.

Developed by Fabian

February, 2026
