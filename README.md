# check_socks
Icinga / Nagios plugin to check if a SOCKS server is responsive

## Description   

## Dependencies
* openbsd netcat
* xxd
* bash 3.2

## Usage

```
Usage: check_socks -H <host> -p <port> [-t timeout]
```

### Example output

The SOCKS server responds as expected:
```
$ /usr/local/bin/check_socks -H 10.0.0.1 -p 1080
Connection to 10.0.0.1 1080 port [tcp/socks] succeeded!

echo $?
0
```

The SOCKS server is running but gives an unexpected response:
```
$ /usr/local/bin/check_socks -H 10.0.0.1 -p 1080 
Connection to 10.0.0.1 1080 port [tcp/ssh] succeeded!
WARNING unexpected result

$ echo $?
2
```

The SOCKS server is not running, or a firewall rejects the connection:
```
$ /usr/local/bin/check_socks -H 10.0.0.1 -p 1080
netcat: connect to 10.0.0.1 port 1080 (tcp) failed: Connection refused

$ echo $?
2
```

The SOCKS server has hung, or a firewall drops the connection:
```
/usr/local/bin/check_socks -H 10.0.0.1 -p 1080
netcat: connect to 10.0.0.1 port 1080 (tcp) timed out: Operation now in progress

$ echo $?
2
```
