{{#title P4wnP1 - setup}}
# Setup

## 1. Accessing the Pi

### 1.1 Access via Wi-Fi

By default, the Pi creates its own Wi-Fi Access Point (AP), making it easy to connect to.

Join the new Wi-Fi network (it should be easy to identify) and enter the default password `MaMe82-P4wnP1`. The Pi's default IP address within its Wi-Fi network is `172.24.0.1`.

### 1.2 Access via USB

An alternative way to connect is by plugging the Pi in via USB. By default, the Pi emulates an Ethernet device that you can connect to.

To find the Pi's IP address, first check the IP of your Ethernet adapter:

```bash
$ ip a
```

Then replace the last octet with `.1`, since the Pi acts as the gateway in this setup.

## 2. SSH and Web UI

Once the Pi's IP address is known, there are two ways to interact with it:

- Open the web UI at `http://<ip>:8000`
- Connect via SSH:
  ```bash
  $ ssh root@172.24.0.1
  ```
  Use the default Kali password `toor`.

The P4wnP1 is now up and running. Well done!
