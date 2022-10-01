## Send traffic to and from process and children via Mullvad VPN (Linux only)

### Dependencies
- `wireguard-tools` Used to configure the wireguard interface.
- `curl` Used to interact with Mullvad API (Not required for via-wireguard).


### via-mullvad
```
via-mullvad acccount_number [OPTIONS...] -- program [program_args]

account_number
    The Mullvad account number. This argument is required.

OPTIONS
    -h hostname
        Specifies the hostname of the Mullvad server to connect to. If no hostname is specified, the locale command is used to determine the
        country and any wireguard server in that country may be used. The value of hostname can be a location in the format {country code}-{city}
        with values used by Mullvad, for example, au-syd for Sydney, Australia.
    -r nameserver
        Uses the nameserver in the argument for DNS lookups.
    -f
        Allow the script to delete the oldest Mullvad device if the account already has the maximum number of accounts registered.
    
    Note: double dash (--) before program is NOT optional.

    EXAMPLES
        Ping github.com from Germany
        via-mullvad 123456789 -h de10-wireguard -- ping github.com

        Execute a program with networking via Singapore
        via-mullvad 123456789 -h sg4-wireguard -- /usr/local/bin/my-program arg1 arg2
```

### via-wireguard
```
via-wireguard endpoint private_key_file peer_key [OPTIONS...] [-- program [program_args...]]

endpoint
    The IP address and port of the wireguard endpoint. This is required and is always the first argument.
private_key_file
    Path to a file containing the private key for the wireguard interface. This is required and is always the second argument.
peer_key
    Base64 representation of the wireguard peer public key. This is required and is always the third argument.

OPTIONS
    -i ip_address
        IP address to assign to the wireguard link.
    -k
        Keep the namespace, wireguard link, etc after the script exits. Use this to use the same resources for a subsequent
        via-wireguard invocation. By default the namespace is deleted before the script exits.
    -r nameserver
        Use the specified nameserver for DNS. Without this argument, the network namespace will use the host's resolv.conf. If the
        host is using systemd-resolved or anything else requiring access to a DNS resolver bound to the host, DNS will not work
        because the namespace has its own routing table with a route for 127.0.0.1 so it cannot access the host at 127.0.0.1.
    -d
        Delete any resources matching the endpoint, private_key_file and peer_key. Use this to clean up after a previous via-wireguard
        invocation with the -k argument.
```