## Send traffic to and from process and children via Mullvad VPN (Linux only)

### via-mullvad
```
via-mullvad [options] [executable [args]]

OPTIONS
    -c, --check
        Checks that the Mullvad VPN connection is working. If the Mullvad VPN connection cannot be confirmed, the program displays an error message,
        exits with exit code 1 and does not execute the executable.
    -C, --check-only
        Checks that the Mullvad VPN connection is working and exits. If the Mullvad VPN connection is confirmed, the program displays a success message.
        If the Mullvad VPN connection cannot be confirmed, the program displays an error message and exits with code 1.
```

### via-wireguard
```
via-wireguard executable
```