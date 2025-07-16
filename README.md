# OpenVPN Connect Windows

A GitHub Action to establish OpenVPN connections on Windows runners. This action fills the gap for Windows-based OpenVPN connectivity in GitHub Actions workflows.

## Features

- ✅ Windows-only OpenVPN connection setup
- ✅ Automatic OpenVPN installation via Chocolatey
- ✅ Username/password authentication
- ✅ Optional connection testing
- ✅ Configurable timeouts and retry logic
- ✅ Clean, production-ready logging
- ✅ Automatic cleanup of OpenVPN processes and temporary files
- ✅ Process tracking for reliable cleanup

## Usage

```yaml
- name: Connect to VPN
  uses: jworford/github-openvpn-windows-action@v1
  with:
    config: ${{ secrets.OPENVPN_CONFIG }}
    username: ${{ secrets.OPENVPN_USERNAME }}
    password: ${{ secrets.OPENVPN_PASSWORD }}
    test-connection: '10.10.10.101:443'  # Optional (IP and port to test connection)
    connection-timeout: '45'              # Optional (seconds)
    max-test-attempts: '10'               # Optional
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `config` | OpenVPN configuration file content (.ovpn) | Yes | |
| `username` | OpenVPN username | Yes | |
| `password` | OpenVPN password | Yes | |
| `test-connection` | Test connection to specific host:port | No | '' |
| `connection-timeout` | Timeout in seconds to wait for VPN connection | No | '45' |
| `max-test-attempts` | Maximum connection test attempts | No | '10' |

## Requirements

- Windows runner (`runs-on: windows-latest`)
- Chocolatey (pre-installed on GitHub Actions Windows runners)

## Example Workflow

```yaml
name: Deploy with VPN

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Connect to VPN
        uses: jworford/github-openvpn-windows-action@v1
        with:
          config: ${{ secrets.OPENVPN_CONFIG }}
          username: ${{ secrets.OPENVPN_USERNAME }}
          password: ${{ secrets.OPENVPN_PASSWORD }}
          test-connection: 'internal-server.company.com:443'
      
      - name: Deploy Application
        run: |
          # Your deployment steps here
          # VPN connection is now established
          
      # Optional: Explicit cleanup (automatic cleanup also runs)
      - name: Cleanup VPN Connection
        if: always()
        uses: jworford/github-openvpn-windows-action/cleanup@v1
```

## Secrets Setup

Add these secrets to your repository:

- `OPENVPN_CONFIG`: Your complete OpenVPN configuration file content
- `OPENVPN_USERNAME`: OpenVPN username
- `OPENVPN_PASSWORD`: OpenVPN password

## Cleanup

This action automatically handles cleanup of OpenVPN processes and temporary files. The cleanup runs in two ways:

### Automatic Cleanup
- Runs automatically at the end of the action using `if: always()`
- Terminates OpenVPN processes using stored process IDs
- Removes temporary files (client.ovpn, auth.txt, openvpn.log)
- Runs even if the workflow fails

### Manual Cleanup
For explicit control, you can use the separate cleanup action:

```yaml
- name: Cleanup VPN Connection
  if: always()
  uses: jworford/github-openvpn-windows-action/cleanup@v1
```

### Cleanup Process
1. **Process Termination**: Finds and terminates OpenVPN processes by stored PID
2. **Fallback Search**: If no stored PID, searches for any OpenVPN processes
3. **File Cleanup**: Removes temporary configuration and log files
4. **Environment Cleanup**: Clears stored process IDs from environment

## License

MIT License