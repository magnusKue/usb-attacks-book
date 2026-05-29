# C2 server

## Overview

The second half of this project contains a C2 server which allows payloads to open a reverse shell for the attacker to use.  
We chose [Sliver](https://sliver.sh/) which is a powerful command and control (C2) framework with a ton of features like for example Secure C2 over mTLS, WireGuard, HTTP(S), and DNS. This will easily do for our usecase.
