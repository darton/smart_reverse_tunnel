# smart_reverse_tunnel

`smart_reverse_tunnel` is a project that simplifies the setup and management of reverse SSH tunnels. It includes a shell script and a systemd service to ensure reliable and persistent connections.

## Components

### Script: `smart_reverse_tunnel.sh`
This shell script automates the process of establishing a reverse SSH tunnel. It ensures that the tunnel remains active and automatically reconnects if the connection drops.

### Systemd Service: `smart_reverse_tunnel.service`
The systemd service file configures and manages the `smart_reverse_tunnel` script, ensuring it starts at boot and keeps running continuously.

## Features

- **Automatic Reconnection**: Ensures that the reverse SSH tunnel is always active.
- **Easy to Configure**: Simple setup with minimal configuration.
- **Systemd Integration**: Seamless integration with systemd for automatic startup and monitoring.

## Variables
The script `smart_reverse_tunnel.sh` includes several variables that need to be configured according to your environment:

```sh
REMOTE_HOST="10.10.10.10"
REMOTE_PORT=22
REMOTE_USER="remoteuser"
REVERSE_TUNNEL_PORT=2221
LOCAL_TUNNEL_PORT=222
PRIVATE_KEY_PATH=""
PING_TIMEOUT=2
```

- **REMOTE_HOST**: The IP address or hostname of the remote server.
- **REMOTE_PORT**: The SSH port on the remote server.
- **REMOTE_USER**: The username to use for the SSH connection.
- **REVERSE_TUNNEL_PORT**: The port on the remote server for the reverse tunnel.
- **LOCAL_TUNNEL_PORT**: The local port to forward.
- **PRIVATE_KEY_PATH**: Path to the SSH private key (if applicable).
- **PING_TIMEOUT**: Timeout for the ping check to ensure the tunnel is active.

## Usage

### Running as Root

1. Copy the `smart_reverse_tunnel.sh` script to your desired location (e.g., `/home/localuser/scripts/`).
2. Adjust the script and service file as needed.
3. Enable and start the systemd service:
   ```sh
   sudo systemctl enable smart_reverse_tunnel.service
   sudo systemctl start smart_reverse_tunnel.service
   ```

### Running as a Regular User

1. Copy the `smart_reverse_tunnel.sh` script to your desired location (e.g., `/home/localuser/scripts/`).
2. Adjust the script and service file to match the user's environment.
3. Move the `smart_reverse_tunnel.service` file to the user's systemd directory:
   ```sh
   mkdir -p ~/.config/systemd/user
   cp smart_reverse_tunnel.service ~/.config/systemd/user/
   ```
4. Enable and start the systemd service for the user:
   ```sh
   systemctl --user enable smart_reverse_tunnel.service
   systemctl --user start smart_reverse_tunnel.service
   ```
5. Make sure the user services are started at login:
   ```sh
   loginctl enable-linger $(whoami)
   ```
   
