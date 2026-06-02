# Command and Control (C2) – Overview

A Command and Control (C2) framework acts as the centralized management hub for red teaming and penetration testing operations. It allows operators to coordinate, monitor, and persistently control compromised devices (so-called *implants*) within a target network.

For this lab environment, the modern open-source framework **Sliver** by Bishop Fox is utilized. 

### Architecture Concept
To ensure maximum isolation and operational security within the lab, the infrastructure is split into three distinct logical and physical entities:

1. **Sliver Server:** The central brain of the framework. It runs isolated inside a Docker container on a dedicated home server, managing active sessions and generating malicious payloads.
2. **Sliver Client:** The interactive command-line interface (CLI) frontend installed on the analyst's laptop. All administrative commands are executed from here.
3. **Implant (Target):** The actual payload/agent executed on the target system (victim VM), which connects back to the server to receive commands and return results.

Administrative control is strictly isolated through a private **Tailscale P2P VPN**, while incoming victim connections are handled and routed by a **Traefik reverse proxy**.